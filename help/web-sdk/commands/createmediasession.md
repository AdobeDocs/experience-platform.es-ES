---
title: createMediaSession
description: Obtenga información sobre cómo configurar Web SDK para que administre sesiones de contenido automáticamente
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---

# `createMediaSession`

El comando `createMediaSession` forma parte del componente `streamingMedia` de Web SDK. Puede utilizar este componente para recopilar datos relacionados con las sesiones de contenido en el sitio web. Consulte la `streamingMedia` [documentación](configure/streamingmedia.md) para obtener información sobre cómo configurar este componente.

Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a [Adobe Analytics para medios de streaming](https://experienceleague.adobe.com/es/docs/media-analytics/using/media-overview) para agregar métricas. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

Puede crear sesiones de contenido en Web SDK de dos formas:

* [Las sesiones multimedia rastreadas automáticamente](#automatic) permiten que Web SDK administre el envío de eventos de ping de medios a [Adobe Analytics para medios de streaming](https://experienceleague.adobe.com/es/docs/media-analytics/using/media-overview). La frecuencia de estos pings está determinada por la configuración del componente [streamingMedia](configure/streamingmedia.md).
* [Las sesiones de medios rastreadas manualmente](#manual) le proporcionan más control sobre el envío de eventos de ping de sesión a [Adobe Analytics para medios de streaming](https://experienceleague.adobe.com/es/docs/media-analytics/using/media-overview). Además, tiene la capacidad de almacenar `sessionID` para sesiones multimedia.

## Crear una sesión multimedia rastreada automáticamente {#automatic}

Para iniciar el seguimiento de una sesión multimedia automáticamente, llame al método `createMediaSession` con las opciones que se describen a continuación:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Propiedad | Tipo | Requerido | Descripción |
|---------|----------|---------|---------|
| `playerId` | Cadena | Sí | El ID del reproductor, un identificador único que representa la sesión de contenido. |
| `getPlayerDetails` | Función | Sí | Una función que devuelve los detalles del reproductor. Web SDK llamará a esta función de devolución de llamada antes de cada evento multimedia para `playerId` proporcionado. |
| `xdm.eventType` | Objeto | No | El tipo de evento de medios. Si no se proporciona, se establece automáticamente en `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sí | El objeto de detalles de sesión. El objeto `sessionDetails` debe contener las propiedades de los detalles de la sesión. Consulte la documentación del [esquema de recopilación de medios](../../xdm/data-types/media-collection-details.md) para obtener más información. |


## Creación de una sesión multimedia rastreada manualmente {#manual}

Para iniciar el seguimiento de una sesión multimedia manualmente, llame al método `createMediaSession` con las opciones que se describen a continuación:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Propiedad | Tipo | Obligatorio | Descripción |
|---------|----------|---------|---------|
| `xdm.eventType` | Objeto | No | El tipo de evento de medios. Si no se proporciona, se establece automáticamente en `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sí | El objeto de detalles de sesión. El objeto `sessionDetails` debe contener las propiedades de los detalles de la sesión. Consulte la documentación del [esquema de recopilación de medios](../../xdm/data-types/media-collection-details.md) para obtener más información. |
| `xdm.mediaCollection.playhead` | Entero | Sí | El cabezal de reproducción actual. |
| `xdm.mediaCollection.qoeDataDetails` | Objeto | No | La calidad de los detalles de los datos de experiencia. Consulte la documentación del [esquema de recopilación de medios](../../xdm/data-types/media-collection-details.md) para obtener más información. |
