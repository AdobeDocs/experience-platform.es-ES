---
title: getMediaAnalyticsTracker
description: Obtenga información sobre cómo crear un objeto Rastreador de Media Analytics y utilizarlo para rastrear eventos de medios.
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---

# `getMediaAnalyticsTracker`

Este comando del SDK web recupera un rastreador de Media Analytics. Puede utilizar este comando para crear una instancia de objeto y, a continuación, utilizar las mismas API que las proporcionadas por la [biblioteca Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), realizar un seguimiento de los eventos de medios.

El comando `getMediaAnalyticsTracker` devuelve la API heredada de Media Analytics.


| Nombre del método | Descripción | Sintaxis |
|-----------------|---|----------------|
| `getInstance` | Crea una instancia del contenido para realizar un seguimiento de la sesión de reproducción. | `Media.getInstance()` |
| `createMediaObject` | Crea un objeto que contiene información multimedia. Devuelve un objeto vacío si se pasan parámetros no válidos. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Crea un objeto que contiene información de un salto. Devuelve un objeto vacío si se pasan parámetros no válidos. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Crea un objeto que contiene información de publicidad. Devuelve un objeto vacío si se pasan parámetros no válidos. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Crea un objeto que contiene información del capítulo. Devuelve un objeto vacío si se pasan parámetros no válidos. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Crea un objeto que contiene información de estado. Devuelve un objeto vacío si se pasan parámetros no válidos. | `Media.createStateObject(name)` |
| `createQoEObject` | Crea un objeto que contiene información de QoE. Devuelve un objeto vacío si se pasan parámetros no válidos. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Métodos de instancia

| Nombre del método | Descripción | Sintaxis |
|---|---|----|
| `trackSessionStart` | Realice un seguimiento de la intención de iniciar la reproducción. Esto inicia una sesión de seguimiento en la instancia de seguimiento de medios. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Rastrear la reproducción o reanudación de contenido después de una pausa previa. | `trackerInstance.trackPlay()` |
| `trackPause` | Rastrear pausa de medios. | `trackerInstance.trackPause()` |
| `trackComplete` | Seguimiento de contenido completado. Llame a este método solo cuando el medio se haya visto por completo. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Rastrear el final de una sesión de visualización. Llame a este método aunque el usuario no vea el contenido completo. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Realizar un seguimiento de un error que se produjo durante la reproducción de contenido. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Realice un seguimiento de un evento personalizado. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Actualice la posición del cabezal de reproducción. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Actualice la calidad de la experiencia. | `trackerInstance.updateQoEObject(qoe)` |

## Constantes

| Nombre de constante | Descripción | Valor |
|-----------------|--|-----------------|
| `MediaType` | Tipo de medio | `Video`, `Audio` |
| `StreamType` | Tipo de flujo | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Define las claves de metadatos estándar para las transmisiones de vídeo | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Define las claves de metadatos estándar para las secuencias de audio. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Define las claves de metadatos estándar para los anuncios. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Define el tipo de un evento de seguimiento. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Define valores estándar para el seguimiento del estado del reproductor. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |
