---
title: Configuración del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo configurar el SDK web de Adobe Experience Platform.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configurar;configuración;SDK;edge;Web SDK;configurar;edgeConfigId;contexto;web;dispositivo;entorno;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;configuración del sdk web;preoculhideStyle;opacidad;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled third;PartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: c0e2d01bd21405f07f4857e1ccf45dd0e4d0f414
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 15%

---

# Configuración del SDK web de Platform

La configuración del SDK se realiza con el comando `configure`.

>[!IMPORTANT]
>
>`configure` es  ** siempre el primer comando llamado .

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
>**Las configuraciones de Edge se han cambiado a Datastreams. Un ID de conjunto de datos es igual que un ID de configuración.**

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | Ninguna |

{style=&quot;table-layout:auto&quot;}

Su ID de configuración asignado, que vincula el SDK a las cuentas y la configuración adecuadas. Al configurar varias instancias dentro de una sola página, debe configurar un `edgeConfigId` diferente para cada instancia.

### `context`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadenas | No | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Indica las categorías de contexto que se recopilarán automáticamente tal como se describe en [Información automática](../data-collection/automatic-information.md). Si no se especifica esta configuración, todas las categorías se utilizan de forma predeterminada.

### `debugEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

{style=&quot;table-layout:auto&quot;}

Indica si la depuración está habilitada. Al establecer esta configuración en `true` se habilitarán las siguientes funciones:

| **Función** | **Función** |
| ---------------------- | ------------------ |
| Registro de consola | Habilita la visualización de mensajes de depuración en la consola JavaScript del explorador |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Rellene este campo con el dominio de origen. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=es).

El dominio es similar a `data.{customerdomain.com}` para un sitio web en www.{customerdomain.com}.

### `orgId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | Ninguna |

{style=&quot;table-layout:auto&quot;}

Su ID de organización [!DNL Experience Cloud] asignado. Al configurar varias instancias dentro de una página, debe configurar un `orgId` diferente para cada instancia.

## Recopilación de datos

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Indica si los datos asociados con clics en vínculos se recopilan automáticamente. Consulte [Seguimiento automático de vínculos](../data-collection/track-links.md#automaticLinkTracking) para obtener más información. Los vínculos también se etiquetan como vínculos de descarga si incluyen un atributo de descarga o si el vínculo termina con una extensión de archivo. Los calificadores del vínculo de descarga se pueden configurar con una expresión regular. El valor predeterminado es `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Función | No | () => sin definir |

{style=&quot;table-layout:auto&quot;}

Configure una llamada de retorno que se llame para cada evento justo antes de enviarla. Se envía un objeto con el campo `xdm` a la rellamada. Para cambiar lo que se envía, modifique el objeto `xdm`. Dentro de la rellamada, el objeto `xdm` ya tiene los datos pasados en el comando event y la información recopilada automáticamente. Para obtener más información sobre la temporización de esta llamada de retorno y un ejemplo, consulte [Modificación global de eventos](tracking-events.md#modifying-events-globally).

## Opciones de privacidad

### `defaultConsent` {#default-consent}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Objeto | No | `"in"` |

{style=&quot;table-layout:auto&quot;}

Establece el consentimiento predeterminado del usuario. Utilice esta configuración cuando no haya preferencias de consentimiento guardadas para el usuario. Los demás valores válidos son `"pending"` y `"out"`. Este valor predeterminado no se mantiene en el perfil del usuario. El perfil del usuario solo se actualiza cuando se llama a `setConsent`.
* `"in"`: Cuando se establece esta configuración o no se proporciona ningún valor, el trabajo continúa sin las preferencias de consentimiento del usuario.
* `"pending"`: Cuando se establece esta configuración, el trabajo se pone en cola hasta que el usuario proporcione las preferencias de consentimiento.
* `"out"`: Cuando se establece esta configuración, el trabajo se descarta hasta que el usuario proporcione las preferencias de consentimiento.
Una vez proporcionadas las preferencias del usuario, el trabajo continúa o se interrumpe en función de sus preferencias. Consulte [Consentimiento de soporte](../consent/supporting-consent.md) para obtener más información.

## Opciones de personalización

### `prehidingStyle`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | No | Ninguna |

{style=&quot;table-layout:auto&quot;}

Se utiliza para crear una definición de estilo CSS que oculte áreas de contenido de su página web mientras se carga contenido personalizado desde el servidor. Si no se proporciona esta opción, el SDK no intenta ocultar ninguna área de contenido mientras se carga el contenido personalizado, lo que potencialmente resulta en un &quot;parpadeo&quot;.

Por ejemplo, si un elemento de la página web tiene un ID de `container`, cuyo contenido predeterminado desea ocultar mientras se carga contenido personalizado desde el servidor, utilice el siguiente estilo de preocultación:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opciones de audiencias

### `cookieDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Habilita [!DNL Audience Manager] destinos de cookies, lo que permite configurar cookies en función de la calificación de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Habilita [!DNL Audience Manager] destinos de URL, lo que permite activar direcciones URL en función de la calificación de segmentos.

## Opciones de identidad

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Si es true, el SDK lee y establece cookies AMCV antiguas. Esta opción ayuda con la transición al uso del SDK web de Adobe Experience Platform, mientras que algunas partes del sitio pueden seguir utilizando Visitor.js. Si la API de visitante está definida en la página, el SDK consulta la API de visitante para el ECID. Esta opción le permite etiquetar páginas con el SDK web de Adobe Experience Platform y seguir teniendo el mismo ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Habilita la configuración de cookies de terceros de Adobe. El SDK puede mantener el ID de visitante en un contexto de terceros para permitir que se use el mismo ID de visitante en todos los sitios. Utilice esta opción si tiene varios sitios o si desea compartir datos con socios; sin embargo, a veces esta opción no es deseada por motivos de privacidad.
