---
title: el contexto
description: Recopilar automáticamente datos de dispositivos, entornos o ubicaciones.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 5%

---

# `context`

La propiedad `context` es una matriz de cadenas que determina lo que Web SDK puede recopilar automáticamente. Aunque estos datos pueden proporcionar un gran valor, omitir algunos de estos datos puede ser beneficioso para que pueda cumplir con la política de privacidad de su organización.

## Palabras clave de contexto y elementos XDM

Si se incluye una palabra clave de contexto determinada, Web SDK rellena automáticamente todos sus elementos XDM asociados. Si desea omitir un elemento XDM específico y permitir otros, puede borrar valores con [`onBeforeEventSend`](onbeforeeventsend.md). Si envía varios eventos en una página, Web SDK incluye estos campos en cada llamada de `SendEvent`.

### Web

La palabra clave `"web"` recopila información sobre la página actual.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| URL de página | Dirección URL de la página actual. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL de referente | La URL de la página anterior visitada. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

### Device

La palabra clave `"device"` recopila información sobre el dispositivo del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Altura de pantalla | Altura de la pantalla en píxeles. | `xdm.device.screenHeight` | `900` |
| Anchura de pantalla | Ancho de la pantalla en píxeles. | `xdm.device.screenWidth` | `1440` |
| Orientación de pantalla | La orientación de la pantalla. | `xdm.device.screenOrientation` | `landscape` o `portrait` |

### Entorno

La palabra clave `"environment"` recopila información acerca del explorador del usuario.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Tipo de entorno | El tipo de entorno a través del cual surgió la experiencia. Web SDK siempre establece este campo en `browser`. | `xdm.environment.type` | `browser` |
| Altura de ventanilla | Altura del área de contenido del explorador en píxeles. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Anchura de ventanilla | Anchura del área de contenido del explorador en píxeles. | `xdm.environment.browserDetails.viewportWidth` | `642` |

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

### Marca de tiempo

La palabra clave `"timestamp"` recopila información sobre la marca de tiempo del evento. Este contexto siempre se incluye y no se puede eliminar.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Marca de tiempo del evento | Marca de tiempo UTC para el usuario final en formato extendido simplificado [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |

### Detalles de implementación

La palabra clave `implementationDetails` recopila información sobre la versión de SDK utilizada para recopilar el evento.

| Dimensión | Descripción | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- |
| Nombre | Identificador del kit de desarrollo de software (SDK). Este campo utiliza un URI para mejorar la exclusividad entre los identificadores proporcionados por diferentes bibliotecas de software. | `xdm.implementationDetails.name` | Cuando se utiliza la biblioteca independiente, el valor es `https://ns.adobe.com/experience/alloy`. Cuando la biblioteca se utiliza como parte de la extensión de etiqueta, el valor es `https://ns.adobe.com/experience/alloy+reactor`. |
| Versión | La versión del kit de desarrollo de software (SDK). | `xdm.implementationDetails.version` | Cuando se utiliza la biblioteca independiente, el valor es la versión de la biblioteca. Cuando la biblioteca se usa como parte de la extensión de etiqueta, el valor es la versión de la biblioteca y la versión de la extensión de etiqueta unidas con un `+`. Por ejemplo, si la versión de la biblioteca es `2.1.0` y la versión de la extensión de la etiqueta es `2.1.3`, el valor sería `2.1.0+2.1.3`. |
| Entorno | Entorno donde se recopilaron los datos. Este campo siempre se establece en `browser` al usar la biblioteca JavaScript. | `xdm.implementationDetails.environment` | `browser` |

### Sugerencias de cliente de alta entropía {#high-entropy-client-hints}

La palabra clave `"highEntropyUserAgentHints"` recopila información detallada acerca del dispositivo del usuario. Estos datos se incluyen en el encabezado HTTP de la solicitud enviada a Adobe. Una vez que los datos han llegado a la red de Edge, el objeto XDM rellena su ruta XDM correspondiente. Si establece la ruta XDM correspondiente en la llamada a `sendEvent`, tiene prioridad sobre el valor del encabezado HTTP.

Si usa búsquedas de dispositivos al [configurar su secuencia de datos](/help/datastreams/configure.md), los datos se pueden borrar en favor de los valores de búsqueda de dispositivos. Algunos campos de sugerencias del cliente y de búsqueda de dispositivos no pueden existir en la misma visita.

| Propiedad | Descripción | Encabezado HTTP | Ruta de XDM | Ejemplo |
| --- | --- | --- | --- | --- |
| Versión de sistema operativo | La versión del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Arquitectura | La arquitectura de CPU subyacente. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Modelo de dispositivo | Nombre del dispositivo utilizado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Tasa de bits | El número de bits que admite la arquitectura de CPU subyacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Proveedor del explorador | Compañía que creó el explorador. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Nombre del explorador | El explorador utilizado. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Versión del explorador | La versión significativa del explorador. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. La versión exacta del explorador no se recopila automáticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

Consulte [Sugerencias del cliente del agente de usuario](/help/collection/use-cases/client-hints.md) para obtener más información.

### Referente de Analytics único {#one-time-analytics-referrer}

La palabra clave `"oneTimeAnalyticsReferrer"` envía un valor de referente a Adobe Analytics solamente en la primera llamada sin toma de decisiones `sendEvent` para una página. El caso de uso principal de esta palabra clave de contexto es evitar que la dimensión [Referente](https://experienceleague.adobe.com/es/docs/analytics/components/dimensions/referrer) de Adobe Analytics se vea inflada por las visitas que se usan principalmente en integraciones de Analytics y Target.

Si un comando `sendEvent` determinado usa un tipo de evento de toma de decisiones (`decisioning.propositionFetch`, `decisioning.propositionDisplay`, `decisioning.propositionInteract`), se omitirá al calcular el primer `sendEvent` de una página. Si el valor del referente cambia en la página y se activa otro `sendEvent`, el nuevo valor del referente se incluye en la carga útil. Esta condición permite utilizar la función con aplicaciones de una sola página.

Cuando se detecta un valor de referente duplicado, la biblioteca establece `data.__adobe.analytics.referrer` en una cadena vacía (`""`).
Si se establece este campo de objeto de datos en una cadena vacía, se borra el valor cuando una visita llega a Adobe Analytics, ya que el objeto de datos sobrescribe cualquier campo equivalente de objeto XDM. Esto no afecta al objeto XDM, lo que permite que los datos se sigan enviando a un conjunto de datos de Experience Platform si se incluyen varios servicios en un conjunto de datos.

## Implementación

Establezca la matriz de cadenas `context` al ejecutar el comando `configure`. Si omite esta propiedad al configurar SDK, toda la información de contexto excepto `"highEntropyUserAgentHints"` y `"oneTimeAnalyticsReferrer"` se recopilará de forma predeterminada. Establezca esta propiedad si desea recopilar sugerencias de cliente de alta entropía o si desea omitir otra información de contexto de la recopilación de datos. Las cadenas se pueden incluir en cualquier orden.

>[!TIP]
>
>Si desea recopilar toda la información de contexto, incluidas las sugerencias de cliente de alta entropía, debe incluir todos los valores de la cadena de matriz `context`. El valor predeterminado `context` omite `"highEntropyUserAgentHints"` y `"oneTimeAnalyticsReferrer"`; si establece la propiedad `context`, los valores omitidos no recopilarán datos.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"]
});
```

## Recopilación de información contextual mediante la extensión de etiquetas Web SDK

Consulte [Configuración de contexto](/help/tags/extensions/client/web-sdk/configure/data-collection.md#context-settings) en Configuración de recopilación de datos en la documentación de la extensión de etiquetas de Web SDK.
