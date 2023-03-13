---
title: Configuración del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo configurar el SDK web de Adobe Experience Platform.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configurar;configuración;SDK;edge;SDK web;configurar;edgeConfigId;contexto;web;dispositivo;entorno;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;preocultandoStyle;opacidad;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: ed39d782ba6991a00a31b48abb9d143e15e6d89e
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 10%

---

# Configuración del SDK web de Platform

La configuración del SDK se realiza con `configure` comando.

>[!IMPORTANT]
>
>`configure` es *siempre* el primer comando llamado.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Hay muchas opciones que se pueden configurar durante la configuración. Todas las opciones se encuentran a continuación, agrupadas por categoría.

## Opciones generales

### `edgeConfigId`

>[!NOTE]
>
>**Las configuraciones de Edge se han cambiado a Datastreams. Un ID de flujo de datos es lo mismo que un ID de configuración.**

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | Ninguna |

{style="table-layout:auto"}

Su ID de configuración asignado, que vincula el SDK con las cuentas y la configuración adecuadas. Al configurar varias instancias dentro de una sola página, debe configurar una diferente `edgeConfigId` para cada instancia.

### `context` {#context}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadenas | No | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Indica las categorías de contexto que se recopilarán automáticamente según se describe en [Información automática](../data-collection/automatic-information.md). Si no se especifica esta configuración, se utilizan todas las categorías de forma predeterminada.

>[!IMPORTANT]
>
>Todas las propiedades de contexto, excepto `highEntropyUserAgentHints`, están activadas de forma predeterminada. Si ha especificado las propiedades de contexto manualmente en la configuración del SDK web, debe habilitar todas las propiedades de contexto para seguir recopilando la información necesaria.

Para habilitar [sugerencias de cliente de alta entropía](user-agent-client-hints.md#enabling-high-entropy-client-hints) en la implementación del SDK web, debe incluir los `highEntropyUserAgentHints` opción de contexto, junto con la configuración existente.

Por ejemplo, para recuperar sugerencias de cliente de alta entropía de las propiedades web, la configuración tendría este aspecto:

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

{style="table-layout:auto"}

Indica si la depuración está habilitada. Estableciendo esta configuración en `true` habilita las siguientes funciones:

| **Función** | **Función** |
| ---------------------- | ------------------ |
| Registro de consola | Permite mostrar mensajes de depuración en la consola JavaScript del explorador |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Rellene este campo con el dominio de origen. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=es).

El dominio es similar a `data.{customerdomain.com}` para un sitio web en www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Ruta después del edgeDomain utilizado para comunicarse e interactuar con los servicios de Adobe.  A menudo, esto solo cambiaría al no utilizar el entorno de producción predeterminado.

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | No | ee |

{style="table-layout:auto"}

### `orgId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | Ninguna |

{style="table-layout:auto"}

Su asignado [!DNL Experience Cloud] ID de organización. Al configurar varias instancias dentro de una página, debe configurar un `orgId` para cada instancia.

## Recopilación de datos

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Indica si los datos asociados con los clics en vínculos se recopilan automáticamente. Consulte [Seguimiento automático de vínculos](../data-collection/track-links.md#automaticLinkTracking) para obtener más información. Los vínculos también se etiquetan como vínculos de descarga si incluyen un atributo de descarga o si el vínculo termina con una extensión de archivo. Los calificadores de vínculos de descarga se pueden configurar con una expresión regular. El valor predeterminado es `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Función | No | () => sin definir |

{style="table-layout:auto"}

Configure una llamada de retorno a la que se llame para cada evento justo antes de enviarlo. Un objeto con el campo `xdm` se envía a la llamada de retorno. Para cambiar lo que se envía, modifique la `xdm` objeto. Dentro de la llamada de retorno, la variable `xdm` ya tiene los datos pasados en el comando de evento y la información recopilada automáticamente. Para obtener más información sobre la temporización de esta llamada de retorno y ver un ejemplo, consulte [Modificación global de eventos](tracking-events.md#modifying-events-globally).

## Opciones de privacidad

### `defaultConsent` {#default-consent}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Objeto | No | `"in"` |

{style="table-layout:auto"}

Establece el consentimiento predeterminado del usuario. Utilice esta configuración cuando no haya ninguna preferencia de consentimiento ya guardada para el usuario. Los otros valores válidos son `"pending"` y `"out"`. Este valor predeterminado no se mantiene en el perfil del usuario. El perfil del usuario se actualiza solo cuando `setConsent` se llama.
* `"in"`: cuando se establece esta configuración o no se proporciona ningún valor, el trabajo se realiza sin preferencias de consentimiento del usuario.
* `"pending"`: cuando se establece esta configuración, el trabajo se pone en cola hasta que el usuario proporciona las preferencias de consentimiento.
* `"out"`: cuando se establece esta configuración, el trabajo se descarta hasta que el usuario proporcione las preferencias de consentimiento.
Una vez proporcionadas las preferencias del usuario, el trabajo continúa o se interrumpe según las preferencias del usuario. Consulte [Consentimiento de apoyo](../consent/supporting-consent.md) para obtener más información.

## Opciones de personalización {#personalization}

### `prehidingStyle` {#prehidingStyle}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | No | Ninguna |

{style="table-layout:auto"}

Se utiliza para crear una definición de estilo CSS que oculta las áreas de contenido de la página web mientras se carga contenido personalizado desde el servidor. Si no se proporciona esta opción, el SDK no intenta ocultar ninguna área de contenido mientras se carga el contenido personalizado, lo que podría provocar un &quot;parpadeo&quot;.

Por ejemplo, si un elemento de la página web tiene un ID de `container`, cuyo contenido predeterminado desea ocultar mientras se carga contenido personalizado desde el servidor, utilice el siguiente estilo de ocultamiento previo:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Esta opción debe utilizarse al migrar páginas individuales desde [!DNL at.js] al SDK web.

Utilice esta opción para permitir que el SDK web lea y escriba el archivo heredado `mbox` y `mboxEdgeCluster` cookies que utilizan los [!DNL at.js]. Esto le ayuda a mantener el perfil del visitante mientras se desplaza de una página que utiliza el SDK web a una página que utiliza el [!DNL at.js] y viceversa.

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

## Opciones de audiencias

### `cookieDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Habilita [!DNL Audience Manager] destinos de cookies, lo que permite configurar las cookies en función de la calificación de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Habilita [!DNL Audience Manager] Destinos URL, que permite activar direcciones URL basadas en la calificación de segmentos.

## Opciones de identidad

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Si el valor es True, el SDK lee y establece cookies AMCV antiguas. Esta opción ayuda a realizar la transición al uso del SDK web de Adobe Experience Platform, mientras que algunas partes del sitio pueden seguir utilizando Visitor.js.

Si la API de visitante se define en la página, el SDK consulta la API de visitante para el ECID. Esta opción le permite etiquetar páginas con el SDK web de Adobe Experience Platform y seguir teniendo el mismo ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Habilita la configuración de cookies de terceros de Adobe. El SDK puede mantener el ID de visitante en un contexto de terceros para permitir que se utilice el mismo ID de visitante en todos los sitios. Utilice esta opción si tiene varios sitios o si desea compartir datos con socios; sin embargo, a veces esta opción no se desea por motivos de privacidad.
