---
title: sendMediaEvent
description: Aprenda a utilizar el comando sendMediaEvent para realizar un seguimiento de sesiones de contenido en el SDK web.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# `sendMediaEvent`

El comando `sendMediaEvent` forma parte del componente `streamingMedia` del SDK web. Puede utilizar este componente para recopilar datos relacionados con las sesiones de contenido en el sitio web. Consulte la `streamingMedia` [documentación](configure/streamingmedia.md) para obtener información sobre cómo configurar este componente.

Utilice el comando `sendMediaEvent` para rastrear reproducciones de contenido, pausas, finalizaciones, actualizaciones de estado del reproductor y otros eventos relacionados.

El SDK web puede gestionar eventos de medios en función del tipo de seguimiento de sesión de medios:

* **Control de eventos para sesiones con seguimiento automático**. En este modo no necesita pasar `sessionID` al evento de medios o al valor del cabezal de reproducción. El SDK web se encargará de esto, según el ID del reproductor proporcionado y la función de devolución de llamada `getPlayerDetails` proporcionada al iniciar la sesión de contenido.
* **Control de eventos para sesiones con seguimiento manual**. En este modo necesita pasar `sessionID` al evento multimedia, junto con el valor del cabezal de reproducción (valor entero). También puede pasar los detalles de calidad de los datos de experiencia, si es necesario.

## Administrar eventos de medios por tipo {#handle-by-type}

Seleccione las pestañas siguientes para ver ejemplos de control de tipo de evento para cada tipo de evento y método de seguimiento de sesión (automático o manual).


### Reproducir {#play}

El tipo de evento `media.play` se usa para rastrear cuándo comienza la reproducción de contenido. Este evento debe enviarse cuando el reproductor cambia de estado a &quot;reproduciendo&quot;. Otros estados desde los que el reproductor pasa a &quot;reproduciendo&quot; incluyen &quot;almacenamiento en búfer&quot;, reanudación de &quot;pausa&quot; por parte del usuario, recuperación de un error o reproducción automática.

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


### Pause {#pause}

El tipo de evento `media.pauseStart` se usa para hacer un seguimiento de cuándo se pone en pausa una reproducción de contenido. Este evento debe enviarse cuando el usuario presione **[!UICONTROL Pausa]**. No hay ningún tipo de evento de reanudación. Se infiere una reanudación cuando se envía un evento `media.play` después de `media.pauseStart`.

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

El tipo de evento `media.error` se usa para realizar un seguimiento de cuándo se produce un error durante la reproducción de contenido. Este evento debe enviarse cuando se produce un error.

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

El tipo de evento `media.adBreakStart` se usa para hacer un seguimiento de cuándo comienza una pausa publicitaria. Este evento debe enviarse cuando se inicie una pausa publicitaria.

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

El tipo de evento `media.adBreakComplete` se usa para hacer un seguimiento de cuándo finaliza una pausa publicitaria. Este evento debe enviarse cuando se complete una pausa publicitaria.

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

El tipo de evento `media.adStart` se usa para hacer un seguimiento del inicio de un anuncio. Este evento debe enviarse cuando se inicie un anuncio.

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

El tipo de evento `media.adComplete` se usa para hacer un seguimiento del momento en el que finaliza un anuncio. Este evento debe enviarse cuando se complete un anuncio.

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

El tipo de evento `media.adSkip` se usa para rastrear cuándo se omite un anuncio. Este evento debe enviarse cuando se omite un anuncio.

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

El tipo de evento `media.chapterStart` se usa para hacer un seguimiento de cuándo comienza un capítulo. Este evento debe enviarse cuando comience un capítulo.

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

El tipo de evento `media.chapterComplete` se usa para realizar un seguimiento del momento en que finaliza un capítulo. Este evento debe enviarse cuando se complete un capítulo.

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

El tipo de evento `media.chapterSkip` se usa para hacer un seguimiento de cuándo se omite un capítulo. Este evento debe enviarse cuando se omita un capítulo.

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

El tipo de evento `media.bufferStart` se usa para hacer un seguimiento del inicio del almacenamiento en búfer. Este evento debe enviarse cuando se inicie el almacenamiento en búfer. No hay ningún tipo de evento `bufferResume`. Se infiere un `bufferResume` al enviar un evento de reproducción después de `bufferStart`.

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

El tipo de evento `media.bitrateChange` se usa para realizar un seguimiento de cuándo cambia la velocidad de bits. Este evento debe enviarse cuando cambie la velocidad de bits.

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

El tipo de evento `media.stateUpdate` se usa para rastrear cuándo cambia el estado del reproductor. Este evento debe enviarse cuando cambie el estado del reproductor.

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

El tipo de evento `media.sessionEnd` se usa para notificar al backend de Media Analytics que cierre inmediatamente la sesión cuando el usuario ha abandonado el contenido y es poco probable que vuelva.

Si no envía un evento `sessionEnd`, se agotará el tiempo de espera de la sesión abandonada cuando no se reciba ningún evento durante 10 minutos o cuando no se produzca ningún movimiento del cabezal de reproducción durante 30 minutos. La sesión se elimina automáticamente.

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

El tipo de evento `media.sessionComplete` se usa para realizar un seguimiento de cuándo finaliza una sesión multimedia. Este evento debe enviarse cuando se llegue al final del contenido principal.

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
