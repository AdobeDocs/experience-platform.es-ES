---
title: createMediaSession
description: Obtenga información sobre cómo configurar el SDK web para administrar sesiones de contenido automáticamente
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

El `createMediaSession` forma parte del SDK web `streamingMedia` componente. Puede utilizar este componente para recopilar datos relacionados con las sesiones de contenido en el sitio web. Consulte la `streamingMedia` [documentación](configure/streamingmedia.md) para obtener información sobre cómo configurar este componente.

Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/es/docs/media-analytics/using/media-overview), para agregar métricas. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

Puede crear sesiones de contenido en el SDK web de dos formas:

* [Sesiones de medios seguidas automáticamente](#automatic) permitir que el SDK web administre el envío de eventos ping de medios a [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/es/docs/media-analytics/using/media-overview). La frecuencia de estos pings está determinada por los ajustes de configuración del [streamingMedia](configure/streamingmedia.md) componente.
* [Sesiones de medios seguidas manualmente](#manual) le proporciona más control sobre el envío de eventos ping de sesión a [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/es/docs/media-analytics/using/media-overview). Además, tiene la capacidad de almacenar `sessionID` para sesiones de contenido.

## Crear una sesión multimedia rastreada automáticamente {#automatic}

Para iniciar el seguimiento de una sesión multimedia automáticamente, llame al método `createMediaSession` con las opciones descritas a continuación:

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
| `getPlayerDetails` | Función | Sí | Una función que devuelve los detalles del reproductor. El SDK web llamará a esta función de llamada de retorno antes de cada evento multimedia para `playerId` siempre. |
| `xdm.eventType ` | Objeto | No | El tipo de evento de medios. Si no se proporciona, se establece automáticamente como `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sí | El objeto de detalles de sesión. El `sessionDetails` debe contener las propiedades de detalles de la sesión. Consulte la [Esquema de recopilación de medios](../../xdm/data-types/media-collection-details.md) para obtener más información. |


## Creación de una sesión multimedia rastreada manualmente {#manual}

Para iniciar el seguimiento de una sesión de contenido manualmente, llame al método `createMediaSession` con las opciones descritas a continuación:

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
| `xdm.eventType` | Objeto | No | El tipo de evento de medios. Si no se proporciona, se establece automáticamente como `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sí | El objeto de detalles de sesión. El `sessionDetails` debe contener las propiedades de detalles de la sesión. Consulte la [Esquema de recopilación de medios](../../xdm/data-types/media-collection-details.md) para obtener más información. |
| `xdm.mediaCollection.playhead` | Entero | Sí | El cabezal de reproducción actual. |
| `xdm.mediaCollection.qoeDataDetails` | Objeto | No | La calidad de los detalles de los datos de experiencia. Consulte la [Esquema de recopilación de medios](../../xdm/data-types/media-collection-details.md) para obtener más información. |
