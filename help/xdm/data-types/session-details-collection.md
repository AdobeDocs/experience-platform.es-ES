---
title: Tipo de datos de recopilación de detalles de sesión
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia (XDM) de recopilación de detalles de sesión.
source-git-commit: fb000d45d828c01fdb08d7555512f07ab52e1f7b
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 12%

---

# [!UICONTROL Detalles de sesión] Tipo de datos de colección

[!UICONTROL Detalles de sesión] La recopilación es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que realiza un seguimiento de los datos relacionados con las sesiones de reproducción de contenido. Los campos de recopilación de medios se utilizan para capturar datos que se envían a otros servicios de Adobe para un procesamiento posterior. Este esquema engloba una amplia gama de propiedades que se pueden utilizar para proporcionar perspectivas sobre el comportamiento del usuario y los patrones de consumo de contenido. Utilice el [!UICONTROL Detalles de sesión] Tipo de datos de recopilación para capturar la participación del usuario mediante el registro de eventos de reproducción, interacciones de publicidad, marcadores de progreso, pausas y otras métricas.

+++Seleccione esta opción para mostrar un diagrama de la recopilación de detalles de la sesión.
![Diagrama del tipo de datos de la recopilación de detalles de la sesión.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Tipo de carga de publicidad] | `adLoad` | Cadena | No | El tipo de anuncio cargado según lo definido por la representación interna de cada cliente. |
| [[!UICONTROL Álbum]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Cadena | No | El nombre del álbum al que pertenece la grabación musical o el vídeo. |
| [[!UICONTROL Artista]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Cadena | No | El nombre del artista del álbum o del grupo que realiza la grabación musical o el vídeo. |
| [[!UICONTROL ID de recurso]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Cadena | No | El [!UICONTROL ID de recurso] es el identificador único del contenido del recurso de contenidos, como el identificador de episodio de series de TV, el identificador de recursos de una película o el identificador de eventos en directo. Normalmente, estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden proceder de otros sistemas propietarios o internos. |
| [[!UICONTROL Autor]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Cadena | No | Nombre del autor de los medios. |
| [[!UICONTROL Tipo de contenido de difusión]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Cadena | Sí | El [!UICONTROL Tipo de contenido de difusión] del envío del flujo. Valores disponibles por [!UICONTROL Tipo de emisión] incluir:<br>Audio: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; y &quot;radio&quot;;<br>Vídeo: &quot;VoD&quot;, &quot;Live&quot;, &quot;Lineal&quot;, &quot;UGC&quot; y &quot;DVoD&quot;.<br>Los clientes pueden proporcionar valores personalizados para este parámetro. |
| [[!UICONTROL Red de difusión]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Cadena | No | El nombre de la red/canal. |
| [[!UICONTROL Canal de contenido]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Cadena | Sí | El [!UICONTROL Canal de contenido] es el canal de distribución desde el que se reprodujo el contenido. |
| [[!UICONTROL El contenido finaliza]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | Booleano | No | [!UICONTROL El contenido finaliza] indica si un recurso de medios cronometrados se vio hasta su finalización. Este evento no significa necesariamente que el usuario haya visto todo el vídeo, ya que podría haberse saltado algunas partes. |
| [!UICONTROL Red de distribución de contenido] | `cdn` | Cadena | No | El [!UICONTROL Red de distribución de contenido] del contenido reproducido. |
| [[!UICONTROL ID de contenido]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | string | Sí | El [!UICONTROL ID de contenido] es un identificador único del contenido. Se puede utilizar para vincular con otros ID de CMS o del sector. |
| [[!UICONTROL Nombre del contenido]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Cadena | No | El [!UICONTROL Nombre del contenido] es el nombre &quot;práctico&quot; (legible en lenguaje natural) del contenido. |
| [[!UICONTROL Nombre del reproductor de contenido]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Cadena | Sí | Nombre del reproductor de contenido. |
| [[!UICONTROL Nombre del creador]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Cadena | No | Nombre del creador del contenido. |
| [[!UICONTROL Parte del día]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Cadena | No | Propiedad que define la hora del día a la que se emitió o reprodujo el contenido. Podría tener cualquier valor establecido como petición del cliente |
| [[!UICONTROL Número de episodio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Cadena | No | El número del episodio. |
| [[!UICONTROL Tipo de fuente]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Cadena | No | El tipo de fuente, que puede representar datos reales relacionados con la fuente, como EAST HD o SD, o el origen de la fuente, como una dirección URL. |
| [[!UICONTROL Fecha de la primera emisión]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Cadena | No | La fecha en la que el contenido se emitió por primera vez en televisión. Cualquier formato de fecha es aceptable, pero el Adobe recomienda: AAAA-MM-DD. |
| [[!UICONTROL Fecha de la primera emisión digital]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Cadena | No | La fecha en la que el contenido se emitió por primera vez en cualquier canal o plataforma digital. Cualquier formato de fecha es aceptable, pero el Adobe recomienda: AAAA-MM-DD. |
| [[!UICONTROL Género]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Cadena | No | El tipo o agrupación de contenido según lo definido por el productor de contenido. Los valores deben estar delimitados por comas en la implementación de variables. |
| [[!UICONTROL Medios autorizados]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Cadena | No | Confirma si el usuario ha sido autorizado a través de la autenticación de Adobe. |
| [[!UICONTROL Longitud del contenido de medios]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Número entero | Sí | El [!UICONTROL Longitud del contenido de medios] contiene la duración/tiempo de ejecución del clip: Es la longitud (o duración) máxima del contenido que se está reproduciendo (en segundos). |
| [[!UICONTROL Inicio de medios]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | Booleano | No | El evento de carga para los medios. Esto ocurre cuando el usuario selecciona el botón de reproducción. Esto cuenta incluso si hay anuncios previos a la emisión, almacenamiento en búfer, errores, etc. |
| [[!UICONTROL Identificador de MVPD]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Cadena | No | Identificador del distribuidor de programación de vídeo multicanal (MVPD) proporcionado mediante autenticación de Adobe. |
| [[!UICONTROL Editor]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Cadena | No | Nombre del editor del contenido de audio. |
| [[!UICONTROL Estación de radio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Cadena | No | Nombre de la emisora de radio en la que se reproduce el audio. |
| [[!UICONTROL Valor de clasificación]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Cadena | No | La clasificación definida por las pautas de clasificación por edades de la TV. |
| [[!UICONTROL Etiqueta de registro]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Cadena | No | El nombre de la discográfica. |
| [[!UICONTROL Reanudar]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Booleano | No | Marca cada reproducción que se reanudó después de más de 30 minutos de búfer, pausa o detención. |
| [[!UICONTROL Número de temporada]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Cadena | No | El [!UICONTROL Número de temporada] a la que pertenece el programa. La temporada solo es necesaria si el programa es un episodio de una serie. |
| [[!UICONTROL Nombre de serie]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Cadena | No | El Nombre Del Programa O La Serie. El Nombre del programa solo es necesario si el programa forma parte de una serie. |
| [[!UICONTROL Tipo de programa]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Cadena | No | El tipo de contenido. Por ejemplo, un tráiler o un episodio completo. El tipo de contenido se expresa como un número entero entre 0 y 3. Por ejemplo, &quot;0&quot; = episodio completo; &quot;1&quot; = Vista previa/trailer; &quot;2&quot; = Clip; &quot;3&quot; = Otro. |
| [[!UICONTROL Formato de flujo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Cadena | No | El formato de la emisión (HD, SD). |
| [[!UICONTROL Tipo de emisión]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Cadena | No | El tipo de flujo de medios. |
| [[!UICONTROL Versión]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Cadena | No | La versión del SDK utilizada por el reproductor. Podría tener cualquier valor personalizado que sea adecuado para el reproductor. |

{style="table-layout:auto"}

<!-- This is required for sessionStart. 
Q) How do I indicate that?
Q) Do you know where to link for:
Ad Load Type
Content Delivery Network
 -->
