---
title: Uso de identityMap en la recopilación de datos
description: Aprenda a construir y enviar cargas útiles de identityMap para identificar visitantes conocidos en todas las áreas de nombres de la implementación de Web SDK.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Uso de identityMap en la recopilación de datos

El objeto de carga útil `identityMap` le indica al Edge Network quién es el visitante que está más allá de su [ECID](./overview.md) de nivel de dispositivo. Cuando un visitante inicia sesión, completa una compra o se da a conocer de otro modo, puede enviar identificadores de nivel de persona (ID de CRM, correo electrónico con hash, ID de fidelidad, etc.) junto con el ECID. Estos identificadores de nivel de persona proporcionan información valiosa a los servicios descendentes para que puedan:

* **Vincular actividad a una persona entre dispositivos y canales.** [Servicio de identidad](/help/identity-service/home.md) vincula las identidades que envía a un [gráfico de identidad](/help/identity-service/features/identity-graph-viewer.md), conectando el comportamiento anónimo en el nivel de dispositivo con una persona conocida.
* **Generar perfiles de cliente unificados.** [Perfil del cliente en tiempo real](/help/profile/home.md) utiliza la identidad principal que configuró para anclar eventos y atributos a un único perfil, lo que permite la segmentación en el nivel de persona y la creación de audiencias.
* **Activar audiencias en destinos de flujo descendente.** Muchos [destinos](/help/destinations/home.md) requieren identidades resueltas a nivel de persona (correos electrónicos con hash, números de teléfono, etc.) para hacer coincidir sus audiencias con sus bases de usuarios.
* **Organizar recorridos entre canales.** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) utiliza identidades resueltas para almacenar en déclencheur y personalizar recorridos en los canales de correo electrónico, push y en la aplicación en función del comportamiento autenticado de un visitante.

Esta página cubre cómo construir `identityMap` cargas útiles, elegir la configuración correcta para cada identidad y manejar escenarios de implementación comunes.

## Estructura de carga útil {#structure}

`identityMap` es un objeto JSON donde cada clave de nivel superior es un área de nombres y el valor es una matriz de descriptores de identidad. Puede incluir una o más áreas de nombres en una sola carga útil, y cada descriptor contiene tres campos: `id`, `authenticatedState` y `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Campo | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `id` | Cadena | Sí | El valor del identificador (por ejemplo, `user@example.com` o `ABC123`). |
| `authenticatedState` | Cadena | Sí | La confianza con la que sabe que esta identidad pertenece al visitante. Los valores válidos incluyen `ambiguous`, `authenticated` y `loggedOut`. |
| `primary` | Booleano | Sí | Si esta identidad debe ser el identificador principal del evento. Exactamente una identidad en todas las áreas de nombres debe estar marcada `primary: true`. |

Las secciones siguientes abarcan cada parte de la carga útil en detalle.

### Claves de área de nombres {#namespace-keys}

Cada clave de nivel superior de `identityMap` es un [área de nombres de identidad](/help/identity-service/features/namespaces.md), una cadena que clasifica el tipo de identificador (por ejemplo, `CRMID`, `Email`, `Phone` o `LoyaltyId`). Deben existir áreas de nombres en el servicio de identidad antes de hacer referencia a ellas en una carga útil. Puede incluir varias claves de área de nombres en el mismo evento cuando tenga más de un identificador para el visitante.

No es necesario incluir el ECID como clave de área de nombres. Edge Network agrega automáticamente el ECID a la carga útil de identidad. Si incluye el ECID explícitamente, no lo marque como `primary` cuando también haya una identidad de nivel de persona.

### `id` {#id}

El campo `id` es la propia cadena de identificador, es decir, el valor que indica a Experience Platform a qué persona o dispositivo específico representa esta identidad. Cada [área de nombres de identidad](/help/identity-service/features/namespaces.md) espera un formato de valor específico, y al enviar un valor en un formato incorrecto se crea una identidad distinta que no se puede combinar con la versión con formato correcto, lo que da como resultado perfiles fragmentados.

Antes de incluir un valor en `identityMap`, prepárelo según el formato que espera el área de nombres de destino:

| Tipos de área de nombres comunes | Cómo preparar el valor | Ejemplo |
| --- | --- | --- |
| **CRM / ID interno** | Utilice el identificador exacto que asigna el sistema de registro. Mantenga el formato coherente en todos los eventos (mayúsculas y minúsculas, ceros a la izquierda y prefijos). | `ABC-12345`, `00098765` |
| **Correo electrónico (sin procesar)** | Ponga en minúsculas la dirección de correo electrónico completa y recorte los espacios iniciales y finales. | `user@example.com` |
| **Correo electrónico (con hash)** | Primero ponga en minúsculas y recorte la dirección de correo electrónico, luego use hash con SHA-256. Envíe la cadena hexadecimal de 64 caracteres resultante. No agregue una sal a menos que la definición del área de nombres requiera una. | `a1b2c3d4e5f6a7b8c9...` |
| **Teléfono (E.164)** | Dé formato al número en [E.164](https://en.wikipedia.org/wiki/E.164): `+` a la izquierda, el código de país y el número del suscriptor sin espacios ni puntuación. | `+15551234567` |
| **FPID** | Generar una cadena [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Consulte [ID de dispositivos de origen](./fpid.md) para conocer los requisitos de generación. | `123e4567-e89b-42d3-9456-426614174000` |

Para obtener la lista completa de áreas de nombres estándar y sus definiciones, vea [Descripción general del área de nombres de identidad](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>El valor `id` distingue entre mayúsculas y minúsculas. `User@Example.com` y `user@example.com` se tratan como dos identidades independientes. Normalice el uso de mayúsculas y minúsculas antes de enviar el valor (normalmente reduciendo el correo electrónico y recortando el espacio en blanco) para evitar la creación de identidades duplicadas en el gráfico.

#### Recopilando `id` durante la ejecución {#collect-id}

El identificador que necesita rara vez está disponible directamente en la página. Las estrategias de recopilación comunes incluyen:

* **Capa de datos**: lea el identificador de la capa de datos del sitio después de que el visitante inicie sesión. Esta ubicación es el método más fiable, ya que la capa de datos se rellena mediante el servidor de la aplicación y refleja el estado de sesión autenticado.
* **Token de autenticación o cookie de sesión**: descodifica o busca el identificador de una cookie JWT o de sesión que establezca su sistema de autenticación. Compruebe que el token sigue activo antes de utilizar el valor.
* **Enriquecimiento del lado del servidor**: use [Preparación de datos para la recopilación de datos](/help/datastreams/data-prep.md) o una [regla de reenvío de eventos](/help/tags/ui/event-forwarding/overview.md) para asignar o transformar el identificador en Edge antes de que llegue a los servicios descendentes. Esta ubicación resulta útil cuando el cliente solo tiene un token de sesión opaco que se asigna a un ID interno en el servidor.

>[!TIP]
>
>Si un valor de `id` determinado se resuelve en una cadena vacía, `null` o `undefined`, no incluya el espacio de nombres en `identityMap`. Al enviar un(a) `id` vacío, se crea un registro de identidad roto. Proteja su implementación con un cheque antes de crear la carga útil.

### `authenticatedState` {#authenticated-state}

El campo `authenticatedState` indica a los servicios descendentes cuánta confianza depositar en una identidad determinada. Los siguientes valores son válidos para este campo:

| Valor | Cuándo usar |
| --- | --- |
| **`authenticated`** | El visitante ha demostrado activamente su identidad durante la sesión actual (por ejemplo, iniciando sesión con credenciales, completando MFA o una verificación similar). |
| **`loggedOut`** | El visitante se ha autenticado anteriormente, pero desde entonces ha cerrado la sesión. La identidad sigue asociada al dispositivo, pero la sesión ya no está activa. |
| **`ambiguous`** | No se puede confirmar que la identidad pertenezca al visitante actual. Utilice este valor para identificadores de nivel de dispositivo como FPID o cualquier identificador donde la autenticación aún no se haya realizado. |

>[!TIP]
>
>El valor `authenticatedState` afecta a la forma en que el servicio de identidad de Adobe Experience Platform crea y combina gráficos de identidad. Si se envía `authenticated` para una identidad que no se ha verificado, se pueden crear vínculos entre dispositivos incorrectos que son difíciles de deshacer.

### `primary` {#primary-identity}

Cada carga de `identityMap` debe tener exactamente una identidad marcada como `primary: true`. La identidad principal determina qué identidad se utiliza como anclaje para el evento en Experience Platform.

Siga estas directrices al configurar la identidad principal:

* **Cuando haya disponible una identidad de nivel de persona** (el visitante ha iniciado sesión), marque el área de nombres de nivel de persona como principal y el ECID como no principal. Esto indica a Experience Platform que vincule el evento a la persona en lugar de al dispositivo.
* **Cuando solo están disponibles las identidades de nivel de dispositivo** (el visitante es anónimo), el ECID se utiliza automáticamente como identidad principal. No necesita incluir el ECID en su `identityMap`, ya que Edge Network lo agrega automáticamente.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Envío de identityMap en la implementación {#send-identity}

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

Pasar `identityMap` en el objeto `xdm` de una llamada a [`sendEvent`](/help/collection/js/commands/sendevent/overview.md):

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Extensión de etiqueta Web SDK]

Utilice el tipo de elemento de datos [mapa de identidad](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) para generar su carga útil de identidad en la interfaz de usuario de etiquetas:

1. Crear un elemento de datos con la extensión **[!UICONTROL Adobe Experience Platform Web SDK]** y el tipo de elemento de datos **[!UICONTROL Identity map]**.
2. Agregue identidades especificando el área de nombres, el elemento de datos o valor que se resuelve en el identificador y el estado autenticado.
3. Marcar una identidad como principal.
4. Hacer referencia a este elemento de datos en la acción **[!UICONTROL Send event]** en **[!UICONTROL Identity map]**.

>[!ENDTABS]

## Casos comunes {#common-scenarios}

+++**Iniciar sesión**

Cuando un visitante inicie sesión, envíe su identificador de nivel de persona con `authenticatedState: "authenticated"` y `primary: true`. Incluya esta identidad en el primer evento después de la autenticación y en todos los eventos posteriores de la sesión.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Cerrar sesión**

Cuando un visitante cierre la sesión, actualice `authenticatedState` a `loggedOut` y mantenga el mismo identificador. Esto preserva la asociación entre el dispositivo y la persona, a la vez que indica que la sesión ya no está activa.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Después de cerrar la sesión, el ECID vuelve a ser la identidad principal efectiva (Edge Network la aplica automáticamente). No marque una identidad de nivel de persona diferente como principal a menos que el visitante inicie sesión con una cuenta diferente.

>[!IMPORTANT]
>
>No deje de enviar el identificador por completo después de cerrar la sesión. Cambiar de `authenticated` a `loggedOut` indica a los servicios posteriores que la sesión finalizó. Si se omite el identificador, se deja un espacio en el gráfico de identidades que puede causar perfiles fragmentados.

+++

+++**Áreas de nombres múltiples**

Puede enviar varias áreas de nombres de identidad en el mismo evento. Este escenario es común cuando un visitante está registrado y tiene varios identificadores disponibles (por ejemplo, un ID de CRM, correo electrónico con hash e ID de fidelidad). Incluya todos los identificadores conocidos, marque solo uno como principal y establezca los demás en `primary: false`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>Al enviar varias áreas de nombres con el mismo `authenticatedState` en el mismo evento, el servicio de identidad recibe la señal más sólida para vincular esas identidades. Incluya todos los identificadores disponibles en el punto de autenticación en lugar de distribuirlos en eventos independientes.

+++

+++**Visitantes anónimos**

Para los visitantes anónimos, normalmente no necesita enviar ningún(a) `identityMap`. Edge Network asigna automáticamente un ECID y lo utiliza como identidad principal. Si usa [ID de dispositivos de origen](./fpid.md), el FPID es la única identidad que necesita incluir para los visitantes anónimos.

+++

## Cómo afecta identityMap al gráfico de identidad {#identity-graph}

Cada carga útil de `identityMap` que llega a Experience Platform la procesa [Identity Service](/help/identity-service/home.md), que vincula las identidades que envía a un [gráfico de identidades](/help/identity-service/features/identity-graph-viewer.md). Las áreas de nombres que incluya, la forma en que establezca `authenticatedState` y la identidad que marque como `primary` dan forma directamente a la forma en que el servicio de identidad crea y combina esos gráficos.

Comportamientos clave que hay que tener en cuenta:

* **Las identidades enviadas en el mismo evento están vinculadas.** Si incluye un CRMID y un área de nombres de correo electrónico en la misma llamada de `sendEvent`, el servicio de identidad creará un vínculo entre esas dos identidades. La propagación de identificadores en eventos independientes produce vínculos más débiles y puede generar gráficos fragmentados.
* **La identidad `primary` ancla el evento en el Perfil del cliente en tiempo real.El perfil** utiliza la identidad principal para determinar a qué perfil pertenece el evento. Marcar la identidad incorrecta como principal (por ejemplo, configurar ECID como principal cuando un ID de nivel de persona está disponible) puede hacer que los eventos se almacenen en perfiles de nivel de dispositivo en lugar de perfiles de nivel de persona.
* **El `authenticatedState` influye en la confianza de gráficos.** Al enviar `authenticated` para una identidad que no se ha verificado realmente, se pueden crear vínculos entre dispositivos incorrectos que son difíciles de deshacer. Use `authenticated` solo cuando el visitante haya demostrado activamente su identidad durante la sesión actual.

Si su implementación usa [reglas de vinculación de gráficos de identidad](/help/identity-service/identity-graph-linking-rules/overview.md) (como la prioridad de área de nombres o el algoritmo de optimización de identidad), revise la [guía de implementación](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) para comprender cómo esas reglas interactúan con las identidades que envía a través de `identityMap`.

>[!NOTE]
>
>El objeto `identityMap` solo se envía cuando Web SDK realiza una solicitud a Edge Network, que depende del estado de consentimiento del visitante. Si su implementación utiliza `defaultConsent: "pending"`, las identidades no se enviarán hasta que se conceda el consentimiento. Consulte [Consentimiento e identidad](./consent.md) para obtener más información.
