---
title: Configuración del SDK
seo-title: Configuración del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo configurar el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo configurar el SDK web de Experience Platform
keywords: configuración;configuración;SDK;edge;Web SDK;configuración;edgeConfigId;contexto;web;dispositivo;entorno;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehideStyle;opacity;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: 3ac00fda2c0a43437fb212dcba7e98c63503b9c4
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 10%

---


# Configuración del SDK

La configuración del SDK se realiza con el comando `configure`.

>[!IMPORTANT]
>
>`configure` debe  ** ser siempre el primer comando llamado.

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

El ID de configuración asignado, que vincula el SDK con las cuentas y la configuración correspondientes.  Al configurar varias instancias dentro de una sola página, debe configurar un `edgeConfigId` diferente para cada instancia.

### `context`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadenas | No | `["web", "device", "environment", "placeContext"]` |

Indica qué categorías de contexto se recopilarán automáticamente, tal como se describe en [Información automática](../data-collection/automatic-information.md).  Si no se especifica esta configuración, se utilizan todas las categorías de forma predeterminada.

### `debugEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

Indica si se debe habilitar la depuración. Al establecer esta configuración en `true` se habilitan las siguientes características:

| **Función** | **Función** |
| ---------------------- | ------------------ |
| Validación sincrónica | Valida los datos que se recopilan con el esquema y devuelve un error en la respuesta bajo la siguiente etiqueta: `collect:error OR success` |
| Registro de la consola | Permite que los mensajes de depuración se muestren en la consola JavaScript del explorador |

### `edgeDomain`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ------------------ |
| Cadena | No | `beta.adobedc.net` |
| Cadena | No | `omtrdc.net` |

Dominio utilizado para interactuar con servicios de Adobe. Solo se utiliza si tiene un dominio de origen (CNAME) que proxies solicitudes a la infraestructura perimetral de Adobe.

### `orgId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | ninguna |

Su identificador de organización [!DNL Experience Cloud] asignado.  Al configurar varias instancias dentro de una página, debe configurar un `orgId` diferente para cada instancia.

## Recopilación de datos

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Indica si los datos asociados con los clics en vínculos se deben recopilar automáticamente. Consulte [Seguimiento automático de vínculos](../data-collection/track-links.md#automaticLinkTracking) para obtener más información.

### `onBeforeEventSend`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Función | No | () => undefined |

Configure esta opción para configurar una llamada de retorno que se llame para cada evento justo antes de que se envíe.  Se envía un objeto con el campo `xdm` a la llamada de retorno.  Modifique el objeto `xdm` para cambiar lo que se envía.  Dentro de la llamada de retorno, el objeto `xdm` ya tendrá los datos pasados en el comando evento y la información recopilada automáticamente. Para obtener más información sobre la temporización de esta llamada de retorno y un ejemplo, consulte [Modificación global de Eventos](tracking-events.md#modifying-events-globally).

## Opciones de privacidad

### `defaultConsent` {#default-consent}

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Objeto | No | `"in"` |

Establece el consentimiento predeterminado del usuario. Se utiliza cuando no hay ninguna preferencia de consentimiento ya guardada para el usuario. El otro valor válido es `"pending"`. Cuando se establece, el trabajo se pone en cola hasta que el usuario proporciona las preferencias de consentimiento. Una vez proporcionadas las preferencias del usuario, el trabajo continúa o se anula según sus preferencias. Consulte [Consentimiento de soporte](../consent/supporting-consent.md) para obtener más información.

## Opciones de personalización

### `prehidingStyle`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | No | ninguna |

Se utiliza para crear una definición de estilo CSS que oculta las áreas de contenido de la página web mientras se carga contenido personalizado desde el servidor. Si no se proporciona esta opción, el SDK no intenta ocultar ninguna área de contenido mientras se carga el contenido personalizado, lo que podría dar como resultado un &quot;parpadeo&quot;.

Por ejemplo, si tiene un elemento en la página web con un ID de `container` cuyo contenido predeterminado desea ocultar mientras se carga contenido personalizado desde el servidor, un ejemplo de un estilo de ocultamiento previo sería el siguiente:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opciones de audiencias

### `cookieDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita [!DNL Audience Manager] destinos de cookies, lo que permite la configuración de cookies según la calificación del segmento.

### `urlDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita [!DNL Audience Manager] destinos de URL, lo que permite activar direcciones URL en función de la calificación del segmento.

## Opciones de identidad

### `idMigrationEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Si el valor es true, el SDK leerá y configurará las cookies AMCV antiguas. Esto ayuda con la transición al uso del SDK web de Adobe Experience Platform, mientras que algunas partes del sitio pueden seguir utilizando Visitante.js. Además, si la API de Visitante está definida en la página, el SDK consulta la API de Visitante para el ECID. Esto le permite dualizar las páginas de etiquetas con el SDK web de AEP y seguir teniendo el mismo ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Habilita la configuración de cookies de terceros de Adobe. El SDK puede mantener el ID de visitante en un contexto de terceros para permitir que se utilice el mismo ID de visitante en todos los sitios. Esto resulta útil si tiene varios sitios o desea compartir datos con socios; sin embargo, a veces esto no es deseable por razones de privacidad.
