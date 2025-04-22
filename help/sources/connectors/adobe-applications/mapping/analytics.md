---
title: Asignación de campos para el conector de Adobe Analytics Source
description: Asigne campos de Adobe Analytics a campos XDM mediante el conector de Source de Analytics.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 316879afe8c94657156c768cdc14d4710da9fd35
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 6%

---

# Asignaciones de campos de Analytics

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través de la fuente de Analytics. Algunos de los datos introducidos a través de ADC se pueden asignar directamente desde campos de Analytics a campos del modelo de datos de experiencia (XDM), mientras que otros datos requieren transformaciones y funciones específicas para asignarse correctamente.

![Ilustración del recorrido de datos de Adobe Analytics de Analytics a Experience Platform.](../images/analytics-data-experience-platform.png)

## Parámetros de medios de streaming

Lea la siguiente tabla para obtener información sobre los parámetros de medios de streaming.

| Fuente de datos | Ruta de campo XDM | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | cadena | El nombre descriptivo (en lenguaje natural) del vídeo. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | cadena | Nombre del autor de los medios. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | cadena | El nombre del artista del álbum o del grupo que realiza la grabación musical o el vídeo. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | cadena | El nombre del álbum al que pertenece el vídeo o la grabación musical. |
| `videolength` | `mediaReporting.sessionDetails.length ` | entero | Duración o tiempo de ejecución del vídeo. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | cadena |
| `video` | `mediaReporting.sessionDetails.name` | cadena | El ID del vídeo. |
| `videoshow` | `mediaReporting.sessionDetails.show` | cadena | El nombre del programa o serie. El nombre del programa o serie solo es necesario si el programa forma parte de una serie. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | cadena | El tipo de medios de streaming, como &quot;vídeo&quot; o &quot;audio&quot;. |
| `videoseason` | `mediaReporting.sessionDetails.season` | cadena | Número de temporada al que pertenece el programa. Este valor solo es necesario si el programa forma parte de una serie. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | cadena | El número del episodio. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | cadena[] | El género del vídeo. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | cadena | Identificador de una instancia de un flujo de contenido único para una reproducción individual. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName ` | cadena | Nombre del reproductor de vídeo. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | cadena | Canal de distribución desde el que se reprodujo el contenido. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | cadena | El tipo de envío de flujo utilizado para el contenido. Se establece automáticamente como &quot;Vídeo&quot; para todas las vistas de vídeo. Los valores recomendados incluyen: VOD, Live, Lineal, UGC, DVOD, Radio, Podcast, Audiobook y Canción. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | cadena | El nombre de la red o del canal. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | cadena | El tipo de fuente. Esto puede representar datos reales relacionados con la fuente, como &quot;East HD&quot; o &quot;SD&quot;, o el origen de la fuente, como una dirección URL. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | cadena |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | Booleano | Un valor booleano que indica si el vídeo se ha iniciado o no. Esto ocurre una vez que el usuario selecciona el botón de reproducción y contará incluso si hay anuncios previos a la emisión, almacenamiento en búfer, errores, etc. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | Booleano | Un valor booleano que indica si se ha iniciado el primer fotograma del contenido. Si el usuario lo cierra durante cualquier tiempo de almacenamiento en búfer o de anuncios, el &quot;inicio del contenido&quot; no se calificaría. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | entero | Duración (en segundos) de todos los eventos de `type=PLAY` en el contenido principal. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | Booleano | Un valor booleano que indica si un recurso de medios cronometrados se vio hasta su finalización. Este valor no significa necesariamente que el visualizador haya visto todo el vídeo, ya que este valor no tiene en cuenta que el visualizador pueda saltarse algunas partes. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | entero | Cantidad total de tiempo que un usuario dedica a un recurso de medios cronometrados específico, incluido el tiempo viendo anuncios. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | entero | La suma de los intervalos únicos vistos por un usuario en un recurso de medios cronometrados. En otras palabras, la duración de los intervalos de reproducción vistos varias veces solo se cuenta una vez. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | número | El tiempo promedio invertido en contenido para un elemento de medios específico. En otras palabras, el tiempo total invertido en contenido dividido por la duración de todas las sesiones de reproducción. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | Booleano | Un valor booleano que indica si el cabezal de reproducción de un vídeo determinado ha superado el marcador del 10 % de la duración total del vídeo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante, los marcadores omitidos no se cuentan. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | Booleano | Un valor booleano que indica si el cabezal de reproducción de un vídeo determinado ha superado el marcador del 25 % de la duración total del vídeo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante, los marcadores omitidos no se cuentan. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | Booleano | Un valor booleano que indica si el cabezal de reproducción de un vídeo determinado ha superado el marcador del 50 % de la duración total del vídeo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante, los marcadores omitidos no se cuentan. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | Booleano | Un valor booleano que indica si el cabezal de reproducción de un vídeo determinado ha superado el marcador del 75 % de la duración total del vídeo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante, los marcadores omitidos no se cuentan. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | Booleano | Un valor booleano que indica si el cabezal de reproducción de un vídeo determinado ha superado el marcador del 95 % de la duración total del vídeo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante, los marcadores omitidos no se cuentan. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | Booleano | Un valor booleano que indica si se produjeron una o más pausas durante la reproducción de un solo elemento de medios. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | entero | El número de periodos de detención que se produjeron durante la reproducción. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | entero | La duración total (en segundos) durante la cual un usuario pausó la reproducción. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | cadena | Identificador de MVPD proporcionado mediante autenticación de Adobe. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | cadena | Define que el usuario ha sido autorizado mediante la autenticación de Adobe. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | Define la hora del día a la que se emitió o reprodujo el contenido. |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | Booleano | Valor booleano que marca cada reproducción que se reanudó después de más de 30 minutos de búfer, pausa o bloqueo. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | Booleano | Un valor booleano que indica que se ha visto al menos un fotograma. Este fotograma no tiene por qué ser el primero. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | cadena | El nombre de la discográfica. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | cadena | La emisora de radio o el nombre en el que se reproduce el audio. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | cadena | Nombre del editor del contenido de audio. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | número | Indica la cantidad de tiempo (en segundos) que transcurrió entre la última interacción conocida de un usuario y el momento en que se cerró la sesión. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | cadena | El tipo de anuncio cargado según lo definido por su propia representación interna. |

{style="table-layout:auto"}

## Parámetros de Advertising

Lea la siguiente tabla para obtener información sobre los parámetros publicitarios.

| Fuente de datos | Ruta de campo XDM | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | cadena | El nombre del anuncio. En los informes, &quot;Nombre del anuncio&quot; es la clasificación y &quot;Nombre del anuncio (variable)&quot; es la eVar. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | entero | El índice del anuncio dentro del inicio del anuncio principal. Por ejemplo, el primer anuncio tiene el índice 0 y el segundo tiene el índice 1. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | entero | Duración del anuncio de vídeo, medida en segundos. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | cadena | Nombre del reproductor utilizado para reproducir el anuncio. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | cadena | El ID de la pausa publicitaria. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | cadena | El nombre descriptivo (en lenguaje natural) de la pausa publicitaria. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | cadena | La compañía o marca cuyo producto aparece en el anuncio. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | cadena | El ID de la campaña de publicidad. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | Booleano | Un valor booleano que indica si el anuncio se ha iniciado o no. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | Booleano | Un valor booleano que indica si el objeto se ha completado o no. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | entero | Cantidad total de tiempo, en segundos, que se emplea para ver el anuncio. |

{style="table-layout:auto"}

## Parámetros de capítulo

Lea la siguiente tabla para obtener información sobre los parámetros del capítulo.

| Fuente de datos | Ruta de campo XDM | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | cadena | El ID del capítulo generado automáticamente. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | Booleano | Un valor booleano que indica si el capítulo se ha iniciado o no. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | Booleano | Un valor booleano que indica si el capítulo se ha completado o no. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | entero | El tiempo, medido en segundos, empleado en el capítulo. |

{style="table-layout:auto"}

## Parámetros de estado del reproductor

Lea la siguiente tabla para obtener información sobre los parámetros de estado del reproductor.

| Fuente de datos | Ruta de campo XDM | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | Booleano | Un valor booleano que indica si el estado del vídeo está configurado o no en pantalla completa. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | entero | El número de veces que se estableció un estado de vídeo en pantalla completa. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | entero | Duración total de cuando el estado del vídeo se estableció en pantalla completa. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | Booleano | Un valor booleano que indica si están habilitados o no los subtítulos. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | entero | La cantidad de veces que se habilitaron los subtítulos. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | entero | Duración total de cuando se habilitaron los subtítulos. |
| `videostatemute` | `mediaReporting.states[].isSet` | Booleano | Un valor booleano que indica si el estado del vídeo se estableció en silencio o no. |
| `videostatemutecount` | `mediaReporting.states[].count` | entero | El número de veces que se silenció un vídeo. |
| `videostatemutetime` | `mediaReporting.states[].time` | entero | Duración total del vídeo en silencio. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | Booleano | Un valor booleano que indica si está habilitado o no el modo imagen en imagen. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | entero | La cantidad de veces que está habilitado el modo imagen en imagen. |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | entero | Duración total de la activación del modo imagen en imagen. |
| `videostateinfocus` | `mediaReporting.states[].isSet` | Booleano | Un valor booleano que indica si el modo enfocado está habilitado o no |
| `videostateinfocuscount` | `mediaReporting.states[].count` | entero | La cantidad de veces que se habilitó el modo de imagen en pantalla. |
| `videostateinfocustime` | `mediaReporting.states[].time` | entero | Duración total de cuando se habilitó el modo de enfoque. |

{style="table-layout:auto"}

## Parámetros de calidad

Lea la siguiente tabla para obtener información sobre los parámetros de calidad.

| Fuente de datos | Ruta de campo XDM | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | número | Velocidad de bits media (en kbps, total). Esta métrica se calcula como una media ponderada de todos los valores de velocidad de bits relacionados con la duración de reproducción que se dan durante una sesión de reproducción. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Booleano | Un valor booleano que indica el número de flujos en los que se produjeron cambios en la velocidad de bits. Esta métrica se define como verdadera solo si tuvo lugar al menos un cambio en la velocidad de bits durante una sesión de reproducción. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | entero |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | cadena | El número de cambios de velocidad de bits. Este valor se calcula como una suma de todos los eventos de cambio de velocidad de bits que se producen durante una sesión de reproducción. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | entero | Duración, medida en segundos, que transcurrió entre la carga y el inicio del vídeo. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Booleano | Un valor booleano que indica el número de flujos en los que se perdieron fotogramas. Esta métrica se define como &quot;true&quot; solo si se perdió al menos un fotograma durante una sesión de reproducción. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | entero | El número de fotogramas descartados durante la reproducción del contenido principal. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | entero | Número de eventos de búfer. Esta métrica se calcula como un recuento de los diferentes estados del búfer que se produjeron durante una sesión de reproducción. Es la cantidad de veces que el reproductor entra en estado de búfer desde otros estados, como reproducción o pausa. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | entero | Cantidad total de tiempo, medido en segundos, que se dedica al almacenamiento en búfer. Este valor se calcula como una suma de todas las duraciones de eventos de búfer que se produjeron durante una sesión de reproducción. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | Booleano | Un valor booleano que indica el número de flujos afectados por el almacenamiento en búfer. Esta métrica se define como verdadera solo si tuvo lugar al menos un evento de búfer durante una sesión de reproducción. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Booleano | Un valor booleano que indica el número de flujos en los que se produjo un evento de error. Por ejemplo, si se llamó a trackError durante la sesión de reproducción y se generó una llamada de latido type=error. Esta métrica se define como verdadera solo si tuvo lugar al menos un error durante la reproducción. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | entero | El número de errores que se produjeron. Este valor se calcula como una suma de todos los eventos de error que se produjeron durante una sesión de reproducción. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | matriz de cadena | ID de error únicos generados por el SDK del reproductor. Debe proporcionar los códigos de error o los ID en el momento de la implementación mediante las API de error proporcionadas. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | matriz de cadena | Los ID de error únicos de cualquier fuente externa, como errores de CDN. Debe proporcionar los códigos de error o los ID en el momento de la implementación mediante las API de error proporcionadas. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | Booleano | ID de error únicos generados por Media SDK durante la reproducción. |

{style="table-layout:auto"}

## Campos obsoletos

Lea esta sección para obtener información sobre los campos de asignación de Analytics obsoletos.

### Campos de asignación directa

+++Seleccione esta opción para ver una tabla de campos de asignación directa obsoletos

| Fuente de datos | Campo XDM | Tipo de XDM | Descripción |
| --- | --- | --- | --- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | cadena | eVars de Analytics personalizadas. Cada organización puede utilizar eVars de forma diferente. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | cadena | Propiedades personalizadas de Analytics. Cada organización puede utilizar props de forma diferente. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | entero | El ID de número del explorador. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | entero | Altura del explorador, en píxeles. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | entero | Anchura del explorador, en píxeles. |
| `m_campaign` | `marketing.trackingCode` | cadena | La variable utilizada en la dimensión Código de seguimiento. |
| `m_channel` | `web.webPageDetails.siteSection` | cadena | La variable utilizada en la dimensión Secciones del sitio. |
| `m_domain` | `environment.domain` | cadena | La variable utilizada en la dimensión Dominio. Se basa en el proveedor de servicios de Internet (ISP) del usuario. |
| `m_geo_city` | `placeContext.geo.city` | cadena | El nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| `m_geo_dma` | `placeContext.geo.dmaID` | entero | El ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| `m_geo_region` | `placeContext.geo.stateProvince` | cadena | El nombre del estado o la región de la visita. Se basa en la dirección IP de la visita. |
| `m_geo_zip` | `placeContext.geo.postalCode` | cadena | El código postal de la visita. Se basa en la dirección IP de la visita. |
| `m_keywords` | `search.keywords` | cadena | La variable utilizada en la dimensión Palabra clave. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | entero | ID numérica que representa el sistema operativo del visitante. Se basa en la columna user_agent. |
| `m_page_url` | `web.webPageDetails.URL` | cadena | La URL de la visita individual a la página. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | cadena | Es igual a 1 en visitas que tienen un nombre de página. Esto es similar a la métrica Vistas de página de Adobe Analytics. |
| `m_referrer` | `web.webReferrer.URL` | cadena | Dirección URL de la página anterior. |
| `m_search_page_num` | `search.pageDepth` | entero | Lo utiliza la dimensión Rango de todas las páginas de búsqueda. Indica en qué página de resultados de búsqueda apareció su sitio antes de que el usuario hiciera clic para acceder a su sitio. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | cadena | Variable de estado. |
| `m_user_server` | `web.webPageDetails.server` | cadena | Variable utilizada en la dimensión Servidor. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | cadena | Variable utilizada para rellenar la dimensión Código postal. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | cadena | Enumera todos los idiomas aceptados, tal como se indica en la cabecera Accept-Language-HTTP. |
| `homepage` | `web.webPageDetails.isHomePage` | Booleano | Ya no se utiliza. Se indica si la dirección URL actual es la página principal del explorador. |
| `ipv6` | `environment.ipV6` | cadena |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | cadena | La versión de JavaScript admitida por el explorador. |
| `user_agent` | `environment.browserDetails.userAgent` | cadena | La cadena del agente de usuario enviada en el encabezado HTTP. |
| `mobileappid` | `application.name` | cadena | El id. de la aplicación móvil, almacenado en el siguiente formato: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | cadena | Nombre del dispositivo móvil. En iOS, se almacena como una cadena de 2 dígitos separados por comas. El primer número representa la generación del dispositivo y el segundo número representa la familia del dispositivo. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | cadena | Utilizado por Mobile Services. Representa el punto de interés. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | número | Utilizado por Mobile Services. Representa la distancia del punto de interés. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | número | Recopilado desde la variable de datos de contexto a.loc.acc. Indica la precisión del GPS en metros en el momento de la recogida. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | cadena | Recopilado desde la variable de datos de contexto a.loc.category. Describe la categoría de un lugar específico. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | cadena | Recopilado desde la variable de datos de contexto a.loc.id. Identificador de un punto de interés determinado. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | cadena | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | número | Señalización principal de Mobile Services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | número | Señalización menor de Mobile Services. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | cadena | UUID de señalización de Mobile Services. |
| `mobileinstalls` | `application.firstLaunches` | Objeto | Se activa la primera vez que se ejecuta después de la instalación o reinstalación | {id (cadena), value (número)} |
| `mobileupgrades` | `application.upgrades` | Objeto | Notifica el número de actualizaciones de aplicaciones. Los déclencheur se ejecutan por primera vez después de la actualización o cada vez que cambia el número de versión. | {id (cadena), value (número)} |
| `mobilelaunches` | `application.launches` | Objeto | El número de veces que se ha iniciado la aplicación. | {id (cadena), value (número)} |
| `mobilecrashes` | `application.crashes` | Objeto |  | {id (cadena), value (número)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Objeto |  | {id (cadena), value (número)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objeto | | {id (cadena), value (número)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objeto | | {id (cadena), value (número)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objeto | Hora de inicio de la calidad de vídeo. | {id (cadena), value (número)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objeto | | {id (cadena), value (número)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objeto | Recuento de búfer de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objeto | Tiempo de búfer de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objeto | Recuento de cambios de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objeto | Velocidad de bits promedio de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objeto | Recuento de errores de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objeto | | {id (cadena), value (número)} |

{style="table-layout:auto"}

+++

## Campos de asignación generados

Los campos seleccionados procedentes de ADC deben transformarse, lo que requiere que la lógica más allá de una copia directa de Adobe Analytics se genere en XDM.

+++Seleccione para ver una tabla de campos de asignación generados en desuso

| Fuente de datos | Campo XDM | Tipo de XDM | Descripción |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Propiedades personalizadas de Analytics, configuradas para ser props de lista. Contiene una lista delimitada de valores. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Utilizado por variables de jerarquía. Contiene una lista delimitada de valores. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Variables de lista personalizadas de Analytics. Contiene una lista delimitada de valores. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | entero | El ID de profundidad de color, que se basa en el valor de la columna c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comercio estándar activados en la visita. | {id (cadena), value (número)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados activados en la visita. | {id (objeto), value (objeto)} |
| `m_geo_country` | `placeContext.geo.countryCode` | cadena | Abreviatura del país del que provino la visita basada en la dirección IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | número | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | número | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | Booleano | Un indicador que indica si Java™ está habilitado. |
| `m_latitude` | `placeContext.geo._schema.latitude` | número | |
| `m_longitude` | `placeContext.geo._schema.longitude` | número | |
| `m_page_event_var1` | `web.webInteraction.URL` | cadena | Variable que solo se utiliza en las solicitudes de imagen de seguimiento de vínculos. Esta variable contiene la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| `m_page_event_var2` | `web.webInteraction.name` | cadena | Variable que solo se utiliza en las solicitudes de imagen de seguimiento de vínculos. Muestra el nombre personalizado del vínculo, si se especifica. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | Booleano | Variable que se utiliza para rellenar la dimensión Páginas no encontradas. Esta variable debe estar vacía o debe contener &quot;ErrorPage&quot;. |
| `m_pagename_no_url` | `web.webPageDetails.name` | número | El nombre de la página (si está configurado). Si no se especifica ninguna página, este valor se deja vacío. |
| `m_paid_search` | `search.isPaid` | Booleano | Un indicador que se establece si la visita coincide con la detección de búsquedas de pago. |
| `m_product_list` | `productListItems[].items` | matriz | La lista de productos, tal como se transmite mediante la variable products. | {SKU (cadena), cantidad (entero), priceTotal (número)} |
| `m_ref_type` | `web.webReferrer.type` | cadena | ID numérica que representa el tipo de referente de la visita.<br/>`1`: Dentro del sitio<br/>`2`: Otros sitios web<br/>`3`: Motores de búsqueda<br/>`4`: Disco duro<br/>`5`: USENET<br/>`6`: Escritos o marcadores (sin referente)<br/>`7`: correo electrónico<br/>`8`: Sin JavaScript<br/>`9`: Redes sociales |
| `m_search_engine` | `search.searchEngine` | cadena | El ID numérico que representa el motor de búsqueda que refirió al visitante a su sitio. |
| `post_currency` | `commerce.order.currencyCode` | cadena | El código de moneda que se utilizó durante la transacción. |
| `post_cust_hit_time_gmt` | `timestamp` | cadena | Esto solo se utiliza en conjuntos de datos con marca de tiempo habilitada. Es la marca de tiempo que se envía con la visita en función de la hora de UNIX®. |
| `post_cust_visid` | `identityMap` | objeto | El ID de visitante de cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | Booleano | El ID de visitante de cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | cadena | El ID de visitante de cliente. |
| `post_visid_high` + `visid_low` | `identityMap` | objeto | Un identificador único de una visita. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | cadena | Un identificador único de una visita. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | Booleano | Se usa con `visid_low` para identificar una visita de forma exclusiva. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | cadena | Se usa con `visid_low` para identificar una visita de forma exclusiva. |
| `post_visid_low` | `identityMap` | objeto | Se utiliza con visid_high para identificar una visita de forma exclusiva. |
| `hit_time_gmt` | `receivedTimestamp` | cadena | La marca de tiempo de la visita basada en la hora de UNIX®. |
| `hitid_high` + `hitid_low` | `_id` | cadena | Un identificador único para identificar una visita. |
| `hitid_low` | `_id` | cadena | Se utiliza con hitid_high para identificar una visita de forma exclusiva. |
| `ip` | `environment.ipV4` | cadena | La dirección IP, basada en el encabezado HTTP de la solicitud de imagen. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | Booleano | La versión de JavaScript utilizada. |
| `mcvisid_high` + `mcvisid_low` | identityMap | objeto | El ID de visitante de Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserID._experience.mcid.id | cadena | El Experience Cloud ID (ECID) también se conoce como MCID y a veces se utiliza en áreas de nombres. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | Booleano | El Experience Cloud ID (ECID) también se conoce como MCID y a veces se utiliza en áreas de nombres. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | cadena | El Experience Cloud ID (ECID) también se conoce como MCID y a veces se utiliza en áreas de nombres. |
| `mcvisid_low` | `identityMap` | objeto | El ID de visitante de Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | cadena | ID de vinculación de visita. El campo de análisis sdid_high y sdid_low es el ID de datos suplementario que se utiliza para unir dos (o más) visitas entrantes. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | cadena | Proximidad de señalización de Mobile Services. |

{style="table-layout:auto"}

+++

## Campos de asignación dividida

Estos campos tienen un solo origen, pero se asignan a **varias** ubicaciones XDM.

+++Seleccione esta opción para ver una tabla de campos de asignación dividida obsoletos

| Fuente de datos | Campo XDM | Tipo de XDM | Descripción |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | entero | ID numérica que representa la resolución del monitor. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | cadena | Versión del sistema operativo móvil. |

{style="table-layout:auto"}

+++

## Campos de asignación avanzados

Los campos seleccionados (conocidos como &quot;valores posteriores&quot;) contienen datos después de que Adobe haya ajustado sus valores mediante Reglas de procesamiento, Reglas de VISTA y Tablas de búsqueda. La mayoría de los valores de publicación tienen un homólogo preprocesado.

El conector de origen de Analytics envía datos preprocesados a un conjunto de datos en Experience Platform. Puede transformar estos datos en su homólogo posprocesado mediante transformaciones. Para obtener más información sobre cómo realizar estas transformaciones mediante el servicio de consultas, consulte [Funciones definidas por Adobe](/help/query-service/sql/adobe-defined-functions.md) en la guía del usuario del servicio de consultas.

Para obtener más información sobre cómo realizar estas transformaciones mediante el servicio de consultas, consulte [Funciones definidas por Adobe](/help/query-service/sql/adobe-defined-functions.md) en la guía del usuario del servicio de consultas.

+++Seleccione para ver una tabla de campos de asignación avanzados obsoletos

| Fuente de datos | Campo XDM | Tipo de XDM | Descripción |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | cadena | eVars de Analytics personalizadas. Cada organización puede utilizar eVars de forma diferente. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | cadena | Propiedades personalizadas de Analytics. Cada organización puede utilizar props de forma diferente. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | entero | Altura del explorador, en píxeles. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | entero | Anchura del explorador, en píxeles. |
| `post_campaign` | `marketing.trackingCode` | cadena | La variable utilizada en la dimensión Código de seguimiento. |
| `post_channel` | `web.webPageDetails.siteSection` | cadena | La variable utilizada en la dimensión Secciones del sitio. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | cadena | El ID de visitante personalizado, si está establecido. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | cadena | La URL de la primera página a la que llega el visitante. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | cadena | Variable utilizada en la dimensión Página de entrada original. El nombre de página de la página de entrada del visitante. |
| `post_keywords` | `search.keywords` | cadena | Las palabras clave que se recopilaron para la visita. |
| `post_page_url` | `web.webPageDetails.URL` | cadena | La URL de la visita individual a la página. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | cadena | Es igual a 1 en visitas que tienen un nombre de página. Esto es similar a la métrica Vistas de página de Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | cadena | Variable que se utiliza para identificar compras de forma exclusiva. |
| `post_referrer` | `web.webReferrer.URL` | cadena | Dirección URL de la página anterior. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | cadena |  Variable de estado. |
| `post_user_server` | `web.webPageDetails.server` | cadena | Variable utilizada en la dimensión Servidor. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | cadena | Variable utilizada para rellenar la dimensión Código postal. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | entero | El ID numérico del explorador. |
| `domain` | `environment.domain` | cadena | La variable utilizada en la dimensión Dominio. Se basa en el proveedor de servicios de Internet (ISP) del usuario. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | cadena | La primera URL de referencia del visitante. |
| `geo_city` | `placeContext.geo.city` | cadena | El nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| `geo_dma` | `placeContext.geo.dmaID` | entero | El ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| `geo_region` | `placeContext.geo.stateProvince` | cadena | El nombre del estado o la región de la visita. Se basa en la dirección IP de la visita. |
| `geo_zip` | `placeContext.geo.postalCode` | cadena | El código postal de la visita. Se basa en la dirección IP de la visita. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | entero | ID numérica que representa el sistema operativo del visitante. Se basa en la columna user_agent. |
| `search_page_num` | `search.pageDepth` | entero | Esta variable la utiliza la dimensión Clasificación de todas las páginas de búsqueda e indica en qué página de resultados de búsqueda se encuentra el sitio | apareció en antes de que el usuario hiciera clic en el sitio. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | cadena | Variable utilizada en la dimensión Palabras clave de búsqueda. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | entero | Variable utilizada en la dimensión Número de visita. Comienza en 1 y aumenta cada vez que se inicia una nueva visita (por usuario). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | entero | Variable utilizada en la dimensión Profundidad de visita. Este valor aumenta en 1 por cada visita que genera el usuario y se restablece después de cada visita. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | cadena | El primer referente de la visita. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | entero | El primer nombre de página de la visita. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Propiedades personalizadas de Analytics, configuradas para ser props de lista. Contiene una lista delimitada de valores. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Lo utilizan las variables de jerarquía y contiene una lista delimitada de valores. | {values (array), delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Una lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comercio estándar activados en la visita. | {id (cadena), value (número)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados activados en la visita.| {id (objeto), value (objeto)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Un indicador que indica si Java™ está habilitado. |
| `post_latitude` | `placeContext.geo._schema.latitude` | número |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | número |   |
| `post_page_event` | `web.webInteraction.type` | cadena | El tipo de visita que se envía en la solicitud de imagen (visita estándar, vínculo de descarga, vínculo de salida o vínculo personalizado en el que se hace clic). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | número | Es igual a 1 si la visita es un clic en vínculo. Esto es similar a la métrica Eventos de página de Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | cadena | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Es la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| `post_page_event_var2` | `web.webInteraction.name` | cadena | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Es el nombre personalizado del vínculo. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | booleano | Se utiliza para rellenar la dimensión Páginas no encontradas. Esta variable debe estar vacía o debe contener &quot;ErrorPage&quot; |
| `post_pagename_no_url` | `web.webPageDetails.name` | número | El nombre de la página (si está configurado). Si no se especifica ninguna página, este valor se deja vacío. |
| `post_product_list` | `productListItems[].items` | matriz | La lista de productos, tal como se transmite mediante la variable products. | {SKU (cadena), cantidad (entero), priceTotal (número)} |
| `post_search_engine` | `search.searchEngine` | cadena | El ID numérico que representa el motor de búsqueda que refirió al visitante a su sitio. |
| `mvvar1_instances` | `.list.items[]` | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| `mvvar2_instances` | `.list.items[]` | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| `mvvar3_instances` | `.list.items[]` | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| `color` | `device.colorDepth` | entero | ID de profundidad de color, basada en el valor de la columna c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | cadena | El ID numérico, que representa el tipo de referente del primer referente del visitante. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | entero | Marca de tiempo de la primera visita del visitante en tiempo UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | cadena | Abreviatura del país del que provino la visita basada en la dirección IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | número |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | número |  |
| `paid_search` | `search.isPaid` | booleano | Un indicador que se establece si la visita coincide con la detección de búsquedas de pago. |
| `ref_type` | `web.webReferrer.type` | cadena | ID numérica que representa el tipo de referente de la visita. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booleano | Un indicador (1=de pago, 0=no pagado) que indica si la primera visita se produjo a partir de una visita de búsqueda de pago. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | cadena | ID numérica que representa el tipo de referente del primer referente de la visita. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | cadena | ID numérica del primer motor de búsqueda de la visita. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | entero | Marca de tiempo de la primera visita individual de la visita en tiempo UNIX®. |

+++