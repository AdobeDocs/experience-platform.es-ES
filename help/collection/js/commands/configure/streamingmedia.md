---
title: streamingMedia
description: Configure Web SDK para recopilar datos relacionados con el uso de los medios en las propiedades web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 8%

---

# `streamingMedia`

El componente `streamingMedia` le ayuda a recopilar datos relacionados con las sesiones de contenido del sitio web.

Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

## Requisitos previos

Para utilizar el componente `streamingMedia` de Web SDK, debe cumplir los siguientes requisitos previos:

* Asegúrese de tener acceso a Adobe Experience Platform o Adobe Analytics.
* Debe utilizar Web SDK versión 2.20.0 o posterior. Consulte la [descripción general de la instalación de Web SDK](../../install/overview.md) para obtener información sobre cómo instalar la versión más reciente.
* Habilite la opción **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** para el conjunto de datos que esté utilizando.
* Asegúrese de que el esquema utilizado por el conjunto de datos incluya los campos de esquema de recopilación de contenido.
* Configure la función Streaming Media en Web SDK, como se muestra en esta página.

Al llamar al comando `configure`, agregue el objeto `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Propiedad | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| **`channel`** | Cadena | Sí | Nombre del canal en el que se produce la recopilación de medios de streaming. Ejemplo: `Video channel`. |
| **`playerName`** | Cadena | Sí | Nombre del reproductor de contenidos. |
| **`appVersion`** | Cadena | No | La versión de la aplicación del reproductor de contenidos. |
| **`mainPingInterval`** | Entero | No | Frecuencia de pings para el contenido principal, en segundos. El valor predeterminado es `10`. Los valores pueden oscilar entre `10` y `50` segundos.  Si no se especifica ningún valor, se usa el valor predeterminado al usar [sesiones con seguimiento automático](../createmediasession.md#automatic). |
| **`adPingInterval`** | Entero | No | Frecuencia de pings para el contenido del anuncio, en segundos. El valor predeterminado es `10`. Los valores pueden oscilar entre `1` y `10` segundos. Si no se especifica ningún valor, se usa el valor predeterminado al usar [sesiones con seguimiento automático](../createmediasession.md#automatic). |

## Configuración de medios de streaming mediante la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [opciones de configuración de medios de streaming](/help/tags/extensions/client/web-sdk/configure/streaming-media.md).
