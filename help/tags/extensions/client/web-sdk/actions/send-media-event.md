---
title: Enviar evento multimedia
description: Envíe datos de medios a Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Enviar evento multimedia

La acción **[!UICONTROL Send media event]** envía un evento multimedia a un conjunto de datos, que luego pueden usar aplicaciones y servicios como Adobe Experience Platform o Adobe Analytics. Esta acción es útil cuando rastrea contenido de medios de streaming en su propiedad.

![Imagen de la interfaz de usuario de Experience Platform que muestra la pantalla del evento de envío de medios.](../assets/send-media-event.png)

Las opciones disponibles dependen de **[!UICONTROL Media event type]** que seleccione. Todos los tipos de eventos multimedia requieren un **[!UICONTROL Player ID]**, que es el nombre del reproductor de contenido.

Algunos tipos de eventos ofrecen la capacidad de configurar otros campos. Si un tipo de evento de medios no aparece en la lista aquí, el único campo disponible es [!UICONTROL Player ID]. Los siguientes tipos de eventos de medios incluyen otros campos:

## [!UICONTROL Ad break start]

Permite configurar los detalles del pod de publicidad.

* **[!UICONTROL Ad break name]**: nombre descriptivo de la pausa para anuncios.
* **[!UICONTROL Ad break offset (seconds)]**: el desplazamiento de la pausa publicitaria dentro del contenido, en segundos.
* **[!UICONTROL Ad break index]**: el índice de desglose de anuncios dentro del contenido, comenzando en 1.

## [!UICONTROL Ad start]

Permite configurar los detalles de la publicidad.

* **[!UICONTROL Ad name]**: nombre descriptivo del anuncio.
* **[!UICONTROL Ad ID]**: ID del anuncio. Se admite cualquier valor alfanumérico.
* **[!UICONTROL Ad length (seconds)]**: duración del anuncio de vídeo, en segundos.
* **[!UICONTROL Advertiser]**: compañía o marca cuyo producto aparece en el anuncio.
* **[!UICONTROL Campaign ID]**: ID de la campaña de publicidad.
* **[!UICONTROL Creative ID]**: ID del creativo de publicidad.
* **[!UICONTROL Creative URL]**: la dirección URL del creador de la publicidad.
* **[!UICONTROL Placement ID]**: ID de ubicación de la publicidad.
* **[!UICONTROL Site ID]**: ID del sitio de publicidad.
* **[!UICONTROL Pod position]**: el índice del anuncio dentro del salto de anuncio principal, comenzando en 0.

Este tipo de evento también admite la capacidad de proporcionar metadatos personalizados como parte de la carga útil de evento de medios.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: un objeto [Calidad de la experiencia](/help/xdm/data-types/qoe-data-details-collection.md) que especifica la velocidad de bits, los fotogramas perdidos, los fotogramas por segundo y el tiempo para el inicio.

## [!UICONTROL Chapter start]

Permite configurar los detalles del capítulo.

* **[!UICONTROL Chapter name]**: nombre del capítulo o segmento.
* **[!UICONTROL Chapter length]**: duración del capítulo, expresada en segundos.
* **[!UICONTROL Chapter index]**: posición del capítulo dentro del contenido.
* **[!UICONTROL Chapter offset]**: desplazamiento del capítulo desde el inicio del contenido, en segundos.

Este tipo de evento también admite la capacidad de proporcionar metadatos personalizados como parte de la carga útil de evento de medios.

## [!UICONTROL Error]

Permite configurar los detalles del error.

* **[!UICONTROL Error name]**: nombre del error.
* **[!UICONTROL Source]**: origen del error.

## [!UICONTROL Session start]

Permite configurar los detalles de la sesión de contenido.

* **[!UICONTROL Handle media session automatically]**: Casilla de verificación que permite a Web SDK enviar los pings necesarios automáticamente. Puede desactivar esta casilla si desea enviar pings manualmente.
* **[!UICONTROL Playhead]**: cabezal de reproducción en segundos.
* **[!UICONTROL Content type]**: el tipo de contenido. Se admite cualquier valor de cadena; Adobe también ofrece los siguientes ajustes preestablecidos:
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: duración máxima del contenido que se está consumiendo, en segundos. Para medios activos con una duración desconocida, el valor predeterminado es `86400`.
* **[!UICONTROL Content ID]**: ID de contenido del contenido.
* **[!UICONTROL Ad load type]**: tipo de anuncio cargado. Se admiten los dos valores siguientes:
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: El álbum al que pertenece la canción.
* **[!UICONTROL Artist]**: el artista de la canción.
* **[!UICONTROL Asset ID]**: identificador único del contenido del recurso multimedia. Estos ID generalmente se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden proceder de otros sistemas propietarios o internos.
* **[!UICONTROL Author]**: nombre del autor del audiolibro.
* **[!UICONTROL Authorized]**: indicador que determina si el usuario ha iniciado sesión mediante la autenticación de Adobe.
* **[!UICONTROL Day part]**: hora del día a la que se emitió o reprodujo el contenido. Se admite cualquier valor de cadena.
* **[!UICONTROL Episode]**: el número del episodio.
* **[!UICONTROL Feed type]**: tipo de fuente.
* **[!UICONTROL First air date]**: La fecha en la que el contenido se emitió por primera vez en televisión. Se admite cualquier valor de cadena; sin embargo, Adobe recomienda usar el formato `YYYY-MM-DD`.
* **[!UICONTROL First digital date]**: la fecha en la que se emitió por primera vez el contenido en cualquier canal o plataforma digital. Se admite cualquier valor de cadena; sin embargo, Adobe recomienda usar el formato `YYYY-MM-DD`.
* **[!UICONTROL Content name]**: nombre descriptivo del contenido.
* **[!UICONTROL Genre]**: tipo o agrupación de contenido definido por el productor de contenido. Este campo admite varios valores, delimitados por una coma.
* **[!UICONTROL Label]**: nombre de la discográfica.
* **[!UICONTROL Rating]**: la clasificación definida por las pautas de clasificación para menores de TV.
* **[!UICONTROL MVPD]**: MVPD proporcionado por la autenticación de Adobe.
* **[!UICONTROL Network]**: nombre de red o canal.
* **[!UICONTROL Originator]**: el creador del contenido.
* **[!UICONTROL Publisher]**: editor del contenido de audio.
* **[!UICONTROL Season]**: si el programa forma parte de una serie, el número de temporada del programa.
* **[!UICONTROL Show]**: si el programa forma parte de una serie, el nombre de la serie.
* **[!UICONTROL Show type]**: el tipo de programa. Se admite cualquier valor de cadena; Adobe también ofrece los siguientes ajustes preestablecidos:
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: el tipo de flujo.
* **[!UICONTROL Stream format]**: formato de la emisión, como HD o SD.
* **[!UICONTROL Station]**: nombre o ID de la emisora de radio.

Este tipo de evento también admite la capacidad de proporcionar metadatos personalizados como parte de la carga útil de evento de medios. También permite anular la configuración del flujo de datos, lo que le permite controlar qué aplicaciones y servicios reciben estos datos. Cuando se establece una anulación de la configuración de la secuencia de datos tanto en un comando individual como en los ajustes de configuración de la extensión de la etiqueta, el comando individual tiene prioridad. Consulte [Anulaciones de configuración de secuencia de datos](../configure/configuration-overrides.md) para obtener más información.

## [!UICONTROL States update]

Permite configurar los detalles de actualización de estado. Puede iniciar o finalizar los siguientes estados:

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

Los campos disponibles son los siguientes:

* **[!UICONTROL States started]**: menú desplegable que le permite indicar que se ha iniciado un estado. Si selecciona el botón **[!UICONTROL Add another state that started]** podrá iniciar varios estados en la misma acción.
* **[!UICONTROL States ended]**: menú desplegable que le permite indicar que ha finalizado un estado. Al seleccionar el botón **[!UICONTROL Add another state that ended]**, puede finalizar varios estados en la misma acción.
