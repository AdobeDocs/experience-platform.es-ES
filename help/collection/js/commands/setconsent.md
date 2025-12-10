---
title: setConsent
description: Se utiliza en cada página para rastrear las preferencias de consentimiento de los usuarios.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 2%

---


# `setConsent`

El comando `setConsent` indica a Web SDK si debe enviar datos (adhesión), descartar datos (exclusión) o utilizar [`defaultConsent`](configure/defaultconsent.md) (consentimiento desconocido).

Web SDK admite los siguientes estándares:

* **[estándar Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Se admiten los estándares 1.0 y 2.0.
* **[Marco de transparencia y consentimiento IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Si usa este estándar, el Perfil del cliente en tiempo real del visitante se actualiza con la información de consentimiento si la implementación está configurada correctamente:
   1. El esquema de perfil individual de XDM contiene el [grupo de campos de consentimiento TCF de IAB 2.0](/help/xdm/field-groups/profile/iab.md).
   1. El esquema Experience Event contiene el [grupo de campos de consentimiento TCF 2.0 de IAB](/help/xdm/field-groups/event/iab.md).
   1. Incluya la información de consentimiento de IAB en el evento [objeto XDM](sendevent/xdm.md). Web SDK no incluye automáticamente la información de consentimiento al enviar datos de evento.

Al utilizar este comando, Web SDK escribe las preferencias del usuario en la cookie [`kndctr_<orgId>_consent`](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk). Esta cookie se establece independientemente de las preferencias de consentimiento del visitante, porque almacena las preferencias de consentimiento de ese visitante. La próxima vez que el usuario cargue el sitio web en el explorador, SDK recuperará estas preferencias persistentes para determinar si los eventos se pueden enviar a Adobe.

Adobe recomienda almacenar todas las preferencias del cuadro de diálogo de consentimiento por separado del consentimiento de Web SDK. Web SDK no ofrece una forma de obtener el consentimiento. Para asegurarse de que las preferencias del usuario permanecen sincronizadas con SDK, puede llamar al comando `setConsent` en cada carga de página. Web SDK solo realiza una llamada al servidor cuando cambia el consentimiento.

## Consideraciones de sincronización de identidad {#identity-considerations}

El comando `setConsent` solo usa `ECID` del mapa de identidad, ya que el comando funciona en el nivel de dispositivo. El comando `setConsent` no tiene en cuenta otras identidades del mapa de identidad.

## Usando `defaultConsent` junto con `setConsent` {#using-consent}

Web SDK ofrece dos comandos de configuración de consentimiento complementarios:

* [`defaultConsent`](configure/defaultconsent.md): este comando establece automáticamente la preferencia de consentimiento predeterminada del visitante antes de llamar a `setConsent`.
* `setConsent` (página actual): este comando establece explícitamente la preferencia de consentimiento del visitante.

Cuando se utilizan juntos, esta configuración puede llevar a diferentes resultados de recopilación de datos y configuración de cookies, según sus valores configurados:

| `defaultConsent` | `setConsent` | Se produce la recopilación de datos | Web SDK establece cookies de explorador |
| --- | --- | --- | --- |
| `in` | `in` | Sí | Sí |
| `in` | `out` | No | Sí |
| `in` | Sin configurar | Sí | Sí |
| `pending` | `in` | Sí | Sí |
| `pending` | `out` | No | Sí |
| `pending` | Sin configurar | No | No |
| `out` | `in` | Sí | Sí |
| `out` | `out` | No | Sí |
| `out` | Sin configurar | No | No |

Consulte [Cookies de Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) en la guía de servicios principales para obtener una lista completa de las cookies que se pueden configurar.

## Usando el comando `setConsent`

Ejecute el comando `setConsent` al llamar a la instancia configurada de Web SDK. Puede incluir los siguientes objetos en este comando:

* **`consent[]`**: una matriz de `consent` objetos. El objeto de consentimiento tiene un formato diferente en función del estándar y la versión que elija. Consulte las pestañas siguientes para ver ejemplos de cada objeto de consentimiento, según el estándar de consentimiento.
* **`identityMap`**: un objeto que controla cómo se genera un ECID y a qué ID está asociada la información de consentimiento. Adobe recomienda incluir este objeto cuando `setConsent` se ejecute antes que otros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: un objeto que contiene [anulaciones de configuración de secuencia de datos](configure/edgeconfigoverrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Objeto `consent` estándar de Adobe 2.0

Si envía datos a Adobe Experience Platform, querrá incluir un grupo de campos de esquema de privacidad en el esquema de perfil. Consulte [Gobernanza, privacidad y seguridad en Adobe Experience Platform](/help/landing/governance-privacy-security/overview.md) para obtener más información sobre el estándar Adobe 2.0. Puede agregar datos dentro del objeto de valor siguiente correspondiente al esquema del campo `consents` del grupo de campos de perfil [!UICONTROL Consents and Preferences].

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad en `"Adobe"` para el estándar Adobe 2.0.
* **`version`**: cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad en `"2.0"` para el estándar Adobe 2.0.
* **`value`**: un objeto que contiene valores de consentimiento.
   * **`value.collect.val`**: el valor de consentimiento. Establezca esto en `"y"` cuando los usuarios acepten la inclusión y en `"n"` cuando los usuarios acepten la exclusión.
   * **`value.metadata.time`**: marca de tiempo de la última vez que los usuarios actualizaron su configuración de consentimiento.

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### Objeto `consent` estándar de IAB TCF 2.0

Para registrar las preferencias de consentimiento del usuario proporcionadas mediante el estándar del marco de transparencia y consentimiento (TCF) de Advertising Bureau Europe (IAB) interactivo, establezca la cadena de consentimiento como se muestra a continuación.

Cuando el consentimiento se establece de esta manera, el Perfil del cliente en tiempo real se actualiza con la información de consentimiento. Para que esto funcione, el esquema XDM de perfil debe contener el [grupo de campos del esquema de privacidad del perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Al enviar eventos, la información de consentimiento de IAB debe añadirse manualmente al objeto XDM de evento. Web SDK no incluye automáticamente la información de consentimiento en los eventos.

Para enviar la información de consentimiento en eventos, debe agregar el grupo de campos Privacidad de Experience Event al esquema [!DNL Profile] habilitado para [!DNL XDM ExperienceEvent]. Consulte la sección sobre [actualización del esquema de ExperienceEvent](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema) en la guía de preparación de conjuntos de datos para ver los pasos sobre cómo configurarlo.

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad en `"IAB TCF"` para el estándar IAB TCF 2.0.
* **`version`**: cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad en `"2.0"` para el estándar IAB TCF 2.0.
* **`value`**: cadena que contiene el valor de consentimiento.
* **`gdprApplies`**: Un booleano que determina si el RGPD se aplica a este valor de consentimiento. Su valor predeterminado es `true`.
* **`gdprContainsPersonalData`**: un booleano que determina si los datos de evento asociados con este usuario contienen datos personales. Su valor predeterminado es `false`.

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

La API IAB TCF 2.0 proporciona un evento para el momento en que el cliente actualiza el consentimiento. Esto ocurre cuando el cliente establece inicialmente sus preferencias y cuando el cliente actualiza sus preferencias. Puede agregar un detector de eventos para ejecutar el comando `setConsent`:

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

El bloque de código anterior escucha el evento `useractioncomplete` y, a continuación, establece el consentimiento, pasando la cadena de consentimiento y la marca `gdprApplies`. Si tiene identidades personalizadas para sus clientes, asegúrese de rellenar la variable `identityMap`.

>[!TAB Adobe 1.0]

### Objeto `consent` estándar de Adobe 1.0

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad en `"Adobe"` para el estándar Adobe 1.0.
* **`version`**: cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad en `"1.0"` para el estándar Adobe 1.0.
* **`value.general`**: el valor de consentimiento. Establezca esto en `"in"` cuando los usuarios acepten la inclusión y en `"out"` cuando los usuarios acepten la exclusión.

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### Envío de varios estándares en una solicitud {#multiple-standards}

Web SDK también admite el envío de más de un objeto de consentimiento en una solicitud, como se muestra en el ejemplo siguiente.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## Persistencia de las preferencias de consentimiento {#persistence}

Una vez que haya comunicado las preferencias de usuario a Web SDK mediante el comando `setConsent`, SDK conserva las preferencias de usuario respecto a una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, Web SDK recuperará y utilizará estas preferencias persistentes para determinar si se pueden enviar o no eventos a Adobe.

Almacena las preferencias del usuario de forma independiente para que pueda mostrar el cuadro de diálogo de consentimiento con las preferencias actuales. No hay forma de recuperar las preferencias de usuario de Web SDK. Para asegurarse de que las preferencias del usuario permanecen sincronizadas con SDK, puede llamar al comando `setConsent` en cada carga de página. Web SDK solo realiza una llamada al servidor si cambian las preferencias.

## Definición del consentimiento mediante la extensión de etiqueta Web SDK

La extensión de etiquetas Web SDK equivalente a este comando es la acción [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md).
