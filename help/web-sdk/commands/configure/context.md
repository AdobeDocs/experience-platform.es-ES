---
title: contexto
description: Recopilar automáticamente datos de dispositivos, entornos o ubicaciones.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: dc2a2ecf7b602d2fcfd3b6c93cecdb6f3368a3f9
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 7%

---

# `context`

La propiedad `context` es una matriz de cadenas que determina lo que el SDK web puede recopilar automáticamente. Aunque estos datos pueden proporcionar un gran valor, omitir algunos de estos datos puede ser beneficioso para que pueda cumplir con la política de privacidad de su organización.

## Palabras clave de contexto y elementos XDM

Si se incluye una palabra clave de contexto determinada, el SDK web rellena automáticamente todos sus elementos XDM asociados. Si desea omitir un elemento XDM específico y permitir otros, puede borrar valores con [`onBeforeEventSend`](onbeforeeventsend.md). Si envía varios eventos en una página, el SDK web incluye estos campos en cada llamada de `SendEvent`.

### Web

La palabra clave `"web"` recopila información sobre la página actual.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| URL de página | Dirección URL de la página actual. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL de referente | La URL de la página anterior visitada. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Device

La palabra clave `"device"` recopila información sobre el dispositivo del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Altura de la pantalla | Altura de la pantalla en píxeles. | `xdm.device.screenHeight` | `900` |
| Anchura de la pantalla | Ancho de la pantalla en píxeles. | `xdm.device.screenWidth` | `1440` |
| Orientación de la pantalla | La orientación de la pantalla. | `xdm.device.screenOrientation` | `landscape` o `portrait` |

{style="table-layout:auto"}

### Entorno

La palabra clave `"environment"` recopila información acerca del explorador del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Tipo de entorno | El tipo de entorno a través del cual surgió la experiencia. El SDK web siempre establece este campo en `browser`. | `xdm.environment.type` | `browser` |
| Altura de la ventanilla | Altura del área de contenido del explorador en píxeles. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Anchura de la ventanilla | Anchura del área de contenido del explorador en píxeles. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contexto del lugar

La palabra clave `"placeContext"` recopila información sobre la ubicación del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Hora local | Marca de tiempo local para el usuario final en formato extendido simplificado [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Desplazamiento de zona horaria local | El número de minutos que el usuario está desfasado de GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Código de país | El código de país del usuario final. | `xdm.placeContext.geo.countryCode` | `US` |
| Provincia del estado | El código de provincia de estado del usuario final. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Latitud | Latitud de la ubicación del usuario final. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Longitud | Longitud de la ubicación del usuario final. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### Marca de tiempo

La palabra clave `timestamp` recopila información sobre la marca de tiempo del evento. Esta parte del contexto no se puede eliminar.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Marca de tiempo del evento | Marca de tiempo UTC para el usuario final en formato extendido simplificado [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### Detalles de implementación

La palabra clave `implementationDetails` recopila información sobre la versión del SDK utilizada para recopilar el evento.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Nombre | Identificador del kit de desarrollo de software (SDK). Este campo utiliza un URI para mejorar la exclusividad entre los identificadores proporcionados por diferentes bibliotecas de software. | `xdm.implementationDetails.name` | Cuando se utiliza la biblioteca independiente, el valor es `https://ns.adobe.com/experience/alloy`. Cuando la biblioteca se utiliza como parte de la extensión de etiqueta, el valor es `https://ns.adobe.com/experience/alloy+reactor`. |
| Versión | La versión del kit de desarrollo de software (SDK). | `xdm.implementationDetails.version` | Cuando se utiliza la biblioteca independiente, el valor es la versión de la biblioteca. Cuando la biblioteca se usa como parte de la extensión de etiqueta, el valor es la versión de la biblioteca y la versión de la extensión de etiqueta unidas con un `+`. Por ejemplo, si la versión de la biblioteca es `2.1.0` y la versión de la extensión de la etiqueta es `2.1.3`, el valor sería `2.1.0+2.1.3`. |
| Entorno | Entorno donde se recopilaron los datos. Siempre se establece en `browser`. | `xdm.implementationDetails.environment` | `browser` |


### Sugerencias de cliente de alta entropía

La palabra clave `"highEntropyUserAgentHints"` recopila información detallada acerca del dispositivo del usuario. Estos datos se incluyen en el encabezado HTTP de la solicitud enviada al Adobe. Una vez que los datos han llegado a la red de Edge, el objeto XDM rellena su ruta XDM correspondiente. Si establece la ruta XDM correspondiente en la llamada a `sendEvent`, tiene prioridad sobre el valor del encabezado HTTP.

Si usa búsquedas de dispositivos al [configurar su secuencia de datos](/help/datastreams/configure.md), los datos se pueden borrar en favor de los valores de búsqueda de dispositivos. Algunos campos de sugerencias del cliente y de búsqueda de dispositivos no pueden existir en la misma visita.

| Dimensión | Descripción | Encabezado HTTP | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- | --- |
| Versión de sistema operativo | La versión del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Arquitectura | Arquitectura de CPU subyacente. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Modelo de dispositivo | Nombre del dispositivo utilizado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Mordacidad | Número de bits que admite la arquitectura de CPU subyacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Proveedor del explorador | Compañía que creó el explorador. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. | `Sec-CH-UA-Full-Version-List` | | |
| Nombre del explorador | El explorador utilizado. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Versión del explorador | La versión significativa del explorador. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. La versión exacta del explorador no se recopila automáticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Recopilación de información contextual mediante la extensión de etiqueta del SDK web

La configuración de información contextual es una combinación de botones de opción y casillas de verificación al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Cada casilla se asigna a una palabra clave de contexto.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Recopilación de datos] y, a continuación, seleccione **[!UICONTROL Toda la información de contexto predeterminada]** o **[!UICONTROL Información de contexto específica]**.
1. Si selecciona **[!UICONTROL Información de contexto específica]**, active la casilla de verificación situada junto a cada elemento de información de contexto que desee.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Recopilar información contextual mediante la biblioteca JavaScript del SDK web

Establezca la matriz de cadenas `context` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK, toda la información de contexto excepto `"highEntropyUserAgentHints"` se recopilará de forma predeterminada. Establezca esta propiedad si desea recopilar sugerencias de cliente de alta entropía o si desea omitir otra información de contexto de la recopilación de datos. Las cadenas se pueden incluir en cualquier orden.

>[!NOTE]
>
>Si desea recopilar toda la información de contexto, incluidas las sugerencias de cliente de alta entropía, debe incluir todos los valores de la cadena de matriz `context`. El valor predeterminado `context` omite `highEntropyUserAgentHints` y, si establece la propiedad `context`, los valores omitidos no recopilarán datos.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
