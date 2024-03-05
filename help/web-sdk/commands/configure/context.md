---
title: contexto
description: Recopilar automáticamente datos de dispositivos, entornos o ubicaciones.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 5%

---

# `context`

El `context` es una matriz de cadenas que determina lo que el SDK web puede recopilar automáticamente. Aunque estos datos pueden proporcionar un gran valor, omitir algunos de estos datos puede ser beneficioso para que pueda cumplir con la política de privacidad de su organización.

## Palabras clave de contexto y elementos XDM

Si se incluye una palabra clave de contexto determinada, el SDK web rellena automáticamente todos sus elementos XDM asociados. Si desea omitir un elemento XDM específico y permitir otros, puede borrar valores mediante [`onBeforeEventSend`](onbeforeeventsend.md). Si envía varios eventos en una página, el SDK web incluye estos campos en cada `SendEvent` llamada.

### Web

El `"web"` keyword recopila información sobre la página actual.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| URL de página | Dirección URL de la página actual. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL de referente | La URL de la página anterior visitada. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Device

El `"device"` keyword recopila información sobre el dispositivo del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Altura de pantalla | Altura de la pantalla en píxeles. | `xdm.device.screenHeight` | `900` |
| Anchura de pantalla | Ancho de la pantalla en píxeles. | `xdm.device.screenWidth` | `1440` |
| Orientación de pantalla | La orientación de la pantalla. | `xdm.device.screenOrientation` | `landscape` o `portrait` |

{style="table-layout:auto"}

### Entorno

El `"environment"` keyword recopila información sobre el explorador del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Tipo de entorno | El tipo de entorno a través del cual surgió la experiencia. El SDK web siempre establece este campo como `browser`. | `xdm.environment.type` | `browser` |
| Altura de ventanilla | Altura del área de contenido del explorador en píxeles. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Anchura de ventanilla | Anchura del área de contenido del explorador en píxeles. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contexto del lugar

El `"placeContext"` keyword recopila información sobre la ubicación del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Hora local | Marca de tiempo local para el usuario final en [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) formato. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Desplazamiento de zona horaria local | El número de minutos que el usuario está desfasado de GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### Sugerencias de cliente de alta entropía

El `"highEntropyUserAgentHints"` La palabra clave recopila información detallada sobre el dispositivo del usuario. Estos datos se incluyen en el encabezado HTTP de la solicitud enviada al Adobe. Una vez que los datos han llegado a la red de Edge, el objeto XDM rellena su ruta XDM correspondiente. Si establece la ruta XDM correspondiente en su `sendEvent` , tiene prioridad sobre el valor del encabezado HTTP.

Si usa búsquedas de dispositivos cuando [configuración de la secuencia de datos](/help/datastreams/configure.md), los datos se pueden borrar en favor de los valores de búsqueda de dispositivos. Algunos campos de sugerencias del cliente y de búsqueda de dispositivos no pueden existir en la misma visita.

| Dimensión | Descripción | Encabezado HTTP | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- | --- |
| Versión del sistema operativo | La versión del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Arquitectura | Arquitectura de CPU subyacente. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Modelo de dispositivo | Nombre del dispositivo utilizado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Tasa de bits | Número de bits que admite la arquitectura de CPU subyacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Proveedor del explorador | Compañía que creó el explorador. La sugerencia de baja entropía `Sec-CH-UA` también registra este elemento. | `Sec-CH-UA-Full-Version-List` | | |
| Nombre del explorador | El explorador utilizado. La sugerencia de baja entropía `Sec-CH-UA` también registra este elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Versión del explorador | La versión significativa del explorador. La sugerencia de baja entropía `Sec-CH-UA` también registra este elemento. La versión exacta del explorador no se recopila automáticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Recopilación de información contextual mediante la extensión de etiqueta del SDK web

La configuración de información contextual es una combinación de botones de opción y casillas de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Cada casilla se asigna a una palabra clave de contexto.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] y, a continuación, seleccione **[!UICONTROL Toda la información de contexto predeterminada]** o **[!UICONTROL Información de contexto específica]**.
1. Si selecciona **[!UICONTROL Información de contexto específica]**, active la casilla de verificación situada junto a cada elemento de información contextual deseado.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Recopilación de información contextual mediante la biblioteca JavaScript del SDK web

Configure las variables `context` matriz de cadenas al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK, toda la información contextual excepto `"highEntropyUserAgentHints"` se recopila de forma predeterminada. Establezca esta propiedad si desea recopilar sugerencias de cliente de alta entropía o si desea omitir otra información de contexto de la recopilación de datos. Las cadenas se pueden incluir en cualquier orden.

>[!NOTE]
>
>Si desea recopilar toda la información de contexto, incluidas las sugerencias del cliente de alta entropía, debe incluir todos los valores en la variable `context` cadena de matriz. El valor predeterminado `context` el valor omite `highEntropyUserAgentHints`y si establece la variable `context` , los valores omitidos no recopilarán datos.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
