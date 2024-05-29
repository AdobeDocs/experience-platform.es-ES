---
title: sendMediaEvent
description: Aprenda a utilizar el comando sendMediaEvent para realizar un seguimiento de sesiones de contenido en el SDK web.
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# `sendMediaEvent`

El `sendMediaEvent` forma parte del SDK web `streamingMedia` componente. Puede utilizar este componente para recopilar datos relacionados con las sesiones de contenido en el sitio web. Consulte la `streamingMedia` [documentación](configure/streamingmedia.md) para obtener información sobre cómo configurar este componente.

Utilice el `sendMediaEvent` para realizar un seguimiento de reproducciones de contenido, pausas, finalizaciones, actualizaciones de estado del reproductor y otros eventos relacionados.

El SDK web puede gestionar eventos de medios en función del tipo de seguimiento de sesión de medios:

* **Gestión de eventos para sesiones rastreadas automáticamente**. En este modo no es necesario pasar el `sessionID` al evento de medios o al valor del cabezal de reproducción. El SDK web se encargará de esto, en función del ID de reproductor proporcionado y el `getPlayerDetails` función de llamada de retorno proporcionada al iniciar la sesión de contenido.
* **Gestión de eventos para sesiones rastreadas manualmente**. En este modo, debe pasar el `sessionID` al evento de medios, junto con el valor del cabezal de reproducción (valor entero). También puede pasar los detalles de calidad de los datos de experiencia, si es necesario.

## Administrar eventos de medios por tipo {#handle-by-type}

Seleccione las pestañas siguientes para ver ejemplos de control de tipo de evento para cada tipo de evento y método de seguimiento de sesión (automático o manual).


### Reproducir {#play}

El `media.play` el tipo de evento se utiliza para rastrear cuándo se inicia la reproducción de contenido. Este evento debe enviarse cuando el reproductor cambia de estado a &quot;reproduciendo&quot;. Otros estados desde los que el reproductor pasa a &quot;reproduciendo&quot; incluyen &quot;almacenamiento en búfer&quot;, reanudación de &quot;pausa&quot; por parte del usuario, recuperación de un error o reproducción automática.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Pausar {#pause}

El `media.pauseStart` El tipo de evento se utiliza para rastrear cuándo se pone en pausa una reproducción de contenido. Este evento debe enviarse cuando el usuario pulse **[!UICONTROL Pausar]**. No hay ningún tipo de evento de reanudación. Se infiere un currículum al enviar una `media.play` evento después de un `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Error {#error}

El `media.error` el tipo de evento se utiliza para realizar un seguimiento de cuándo se produce un error durante la reproducción de contenido. Este evento debe enviarse cuando se produce un error.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Inicio de pausa publicitaria {#ad-break-start}

El `media.adBreakStart` el tipo de evento se utiliza para rastrear cuándo se inicia una pausa publicitaria. Este evento debe enviarse cuando se inicie una pausa publicitaria.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Pausa publicitaria completa {#ad-break-complete}

El `media.adBreakComplete` El tipo de evento se utiliza para realizar un seguimiento del momento en el que finaliza una pausa publicitaria. Este evento debe enviarse cuando se complete una pausa publicitaria.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Inicio del anuncio {#ad-start}

El `media.adStart` el tipo de evento se utiliza para rastrear cuándo se inicia un anuncio. Este evento debe enviarse cuando se inicie un anuncio.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### Anuncio completado {#ad-complete}

El `media.adComplete` el tipo de evento se utiliza para rastrear cuándo se completa un anuncio. Este evento debe enviarse cuando se complete un anuncio.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Omisión de publicidad {#ad-skip}

El `media.adSkip` el tipo de evento se utiliza para rastrear cuándo se omite un anuncio. Este evento debe enviarse cuando se omite un anuncio.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Inicio del capítulo {#chapter-start}

El `media.chapterStart` el tipo de evento se utiliza para realizar un seguimiento del inicio de un capítulo. Este evento debe enviarse cuando comience un capítulo.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### Capítulo completado {#chapter-complete}

El `media.chapterComplete` El tipo de evento se utiliza para realizar un seguimiento del momento en el que finaliza un capítulo. Este evento debe enviarse cuando se complete un capítulo.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Omisión de capítulo {#chapter-skip}

El `media.chapterSkip` el tipo de evento se utiliza para rastrear cuándo se omite un capítulo. Este evento debe enviarse cuando se omita un capítulo.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Inicio del búfer {#buffer-start}

El `media.bufferStart` el tipo de evento se utiliza para rastrear cuándo se inicia el almacenamiento en búfer. Este evento debe enviarse cuando se inicie el almacenamiento en búfer. No hay ninguna `bufferResume` tipo de evento. A `bufferResume` se infiere al enviar un evento de reproducción después de que `bufferStart`.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Cambio de velocidad de bits {#bitrate-change}

El `media.bitrateChange` El tipo de evento se utiliza para rastrear cuándo cambia la velocidad de bits. Este evento debe enviarse cuando cambie la velocidad de bits.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Actualizaciones de estado {#state-updates}

El `media.stateUpdate` el tipo de evento se utiliza para rastrear cuándo cambia el estado del reproductor. Este evento debe enviarse cuando cambie el estado del reproductor.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### Fin de sesión {#session-end}

El `media.sessionEnd` El tipo de evento se utiliza para notificar al backend de Media Analytics que cierre inmediatamente la sesión cuando el usuario ha abandonado el contenido y es poco probable que vuelva.

Si no envía una `sessionEnd` evento, una sesión abandonada agotará el tiempo de espera después de que no se reciba ningún evento durante 10 minutos o cuando no se produzca ningún movimiento del cabezal de reproducción durante 30 minutos. La sesión se elimina automáticamente.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Sesión completa {#session-complete}

El `media.sessionComplete` el tipo de evento se utiliza para rastrear cuándo se completa una sesión de contenido. Este evento debe enviarse cuando se llegue al final del contenido principal.

>[!BEGINTABS]

>[!TAB Seguimiento automático de sesiones]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Seguimiento manual de sesión]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]



