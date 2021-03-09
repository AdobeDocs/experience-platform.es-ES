---
title: Configuración del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo configurar el SDK web de Adobe Experience Platform.
seo-description: Obtenga información sobre cómo configurar el SDK web de Experience Platform
keywords: configurar;configuración;SDK;edge;Web SDK;configurar;edgeConfigId;contexto;web;dispositivo;entorno;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;configuración del sdk web;preoculhideStyle;opacidad;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled third;PartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: f78da58ba7a593d9c161030833d9b69e2ba57c9a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 10%

---


# Configuración del SDK web de Platform

La configuración del SDK se realiza con el comando `configure`.

>[!IMPORTANT]
>
>`configure` siempre debe  ** ser el primer comando llamado.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Hay muchas opciones que se pueden configurar durante la configuración. Todas las opciones se encuentran a continuación, agrupadas por categoría.

## Opciones generales

### `edgeConfigId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | ninguna |

Su ID de configuración asignado, que vincula el SDK a las cuentas y la configuración adecuadas.  Al configurar varias instancias dentro de una sola página, debe configurar un `edgeConfigId` diferente para cada instancia.

### `context`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadenas | No | `["web", "device", "environment", "placeContext"]` |

Indica las categorías de contexto que se recopilarán automáticamente tal como se describe en [Información automática](../data-collection/automatic-information.md).  Si no se especifica esta configuración, todas las categorías se utilizan de forma predeterminada.

### `debugEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

Indica si la depuración debe estar habilitada. Al establecer esta configuración en `true` se habilitarán las siguientes funciones:

| **Función** | **Función** |
| ---------------------- | ------------------ |
| Validación sincrónica | Valida los datos que se recopilan con el esquema y devuelve un error en la respuesta con la siguiente etiqueta: `collect:error OR success` |
| Registro de consola | Habilita la visualización de mensajes de depuración en la consola JavaScript del explorador |

### `edgeDomain` {#edge-domain}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ------------------ |
| Cadena | No | `beta.adobedc.net` |
| Cadena | No | `omtrdc.net` |

Dominio utilizado para interactuar con los servicios de Adobe. Solo se utiliza si tiene un dominio de origen (CNAME) que proxie solicitudes a la infraestructura perimetral de Adobe.

### `orgId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | ninguna |

Su ID de organización [!DNL Experience Cloud] asignado.  Al configurar varias instancias dentro de una página, debe configurar un `orgId` diferente para cada instancia.

## Recopilación de datos

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Indica si los datos asociados con los clics en vínculos se deben recopilar automáticamente. Consulte [Seguimiento automático de vínculos](../data-collection/track-links.md#automaticLinkTracking) para obtener más información.

### `onBeforeEventSend`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Función | No | () => sin definir |

Configúrelo para configurar una llamada de retorno que se llame para cada evento justo antes de enviarse.  Se envía un objeto con el campo `xdm` a la rellamada.  Modifique el objeto `xdm` para cambiar lo que se envía.  Dentro de la rellamada, el objeto `xdm` ya tendrá los datos pasados en el comando event y la información recopilada automáticamente. Para obtener más información sobre la temporización de esta llamada de retorno y un ejemplo, consulte [Modificación global de eventos](tracking-events.md#modifying-events-globally).

## Opciones de privacidad

### `defaultConsent` {#default-consent}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Objeto | No | `"in"` |

Establece el consentimiento predeterminado del usuario. Se utiliza cuando no hay preferencias de consentimiento ya guardadas para el usuario. Los demás valores válidos son `"pending"` y `"out"`. Este valor predeterminado no se mantiene en el perfil del usuario. Solo se actualiza el perfil del usuario cuando se llama a setConsent .
* `"in"`: Cuando se establece o no se proporciona ningún valor, el trabajo continúa sin las preferencias de consentimiento del usuario.
* `"pending"`: Cuando esto está establecido, el trabajo se pondrá en cola hasta que el usuario proporcione las preferencias de consentimiento.
* `"out"`: Cuando esto está establecido, el trabajo se descartará hasta que el usuario proporcione las preferencias de consentimiento.
Una vez proporcionadas las preferencias del usuario, el trabajo continúa o se interrumpe en función de sus preferencias. Consulte [Consentimiento de soporte](../consent/supporting-consent.md) para obtener más información.

## Opciones de personalización

### `prehidingStyle`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | No | ninguna |

Se utiliza para crear una definición de estilo CSS que oculte áreas de contenido de su página web mientras se carga contenido personalizado desde el servidor. Si no se proporciona esta opción, el SDK no intenta ocultar ninguna área de contenido mientras se carga el contenido personalizado, lo que potencialmente resulta en un &quot;parpadeo&quot;.

Por ejemplo, si tiene un elemento en la página web con un ID de `container` cuyo contenido predeterminado desea ocultar mientras se carga contenido personalizado desde el servidor, un ejemplo de estilo de preocultación sería el siguiente:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opciones de audiencias

### `cookieDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita [!DNL Audience Manager] destinos de cookies, lo que permite configurar cookies en función de la calificación de segmentos.

### `urlDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita [!DNL Audience Manager] destinos de URL, lo que permite activar direcciones URL en función de la calificación de segmentos.

## Opciones de identidad

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Si es true, el SDK leerá y establecerá cookies AMCV antiguas. Esto ayuda con la transición al uso del SDK web de Adobe Experience Platform, mientras que algunas partes del sitio pueden seguir utilizando Visitor.js. Además, si la API de visitante está definida en la página, el SDK consultará la API de visitante para el ECID. Esto le permite etiquetar páginas con el SDK web de Adobe Experience Platform y seguir teniendo el mismo ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Habilita la configuración de cookies de terceros de Adobe. El SDK puede mantener el ID de visitante en un contexto de terceros para permitir que se use el mismo ID de visitante en todos los sitios. Esto resulta útil si tiene varios sitios o si desea compartir datos con socios; sin embargo, a veces esto no es deseable por motivos de privacidad.
