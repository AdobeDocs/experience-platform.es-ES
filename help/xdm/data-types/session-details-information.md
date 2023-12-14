---
title: Tipo de datos de información de detalles de sesión
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de información de detalles de sesión.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 11%

---

# [!UICONTROL Información de detalles de sesión] tipo de datos

[!UICONTROL Información de detalles de sesión] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que realiza un seguimiento de los datos relacionados con las sesiones de reproducción de contenido. El esquema engloba una amplia gama de propiedades que proporcionan información sobre cómo se consume el contenido multimedia. Utilice el [!UICONTROL Información de detalles de sesión] tipo de datos para capturar la participación del usuario mediante el registro de eventos de reproducción, interacciones de publicidad, marcadores de progreso, pausas y otras métricas. Esto ofrece una valiosa perspectiva del comportamiento del usuario y los patrones de consumo de contenido.

+++Seleccione para mostrar un diagrama del tipo de datos Información de detalles de la sesión.
![Diagrama del tipo de datos Información de detalles de la sesión.](../images/data-types/session-details-information.png)
+++

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL ID de sesión de contenido] | `ID` | string | El [!UICONTROL ID de sesión de contenido] identifica una instancia de un flujo de contenido único para una reproducción individual. |
| [!UICONTROL ID de contenido] | `name` | string | **Requerido** El [!UICONTROL ID de contenido] es un identificador único del contenido. Se puede utilizar para vincular con otros ID de CMS o del sector. |
| [!UICONTROL Nombre del contenido] | `friendlyName` | Cadena | El [!UICONTROL Nombre del contenido] es el nombre &quot;práctico&quot; (legible en lenguaje natural) del contenido. |
| [!UICONTROL Longitud del contenido de medios] | `length` | Número entero | **Requerido** El [!UICONTROL Longitud del contenido de medios] contiene la duración/tiempo de ejecución del clip: Es la longitud (o duración) máxima del contenido que se está reproduciendo (en segundos). |
| [!UICONTROL Tipo de contenido de difusión] | `contentType` | Cadena | **Requerido** El [!UICONTROL Tipo de contenido de difusión] del envío del flujo. Valores disponibles por [!UICONTROL Tipo de emisión] incluir:<br>Audio: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; y &quot;radio&quot;;<br>Vídeo: &quot;VoD&quot;, &quot;Live&quot;, &quot;Lineal&quot;, &quot;UGC&quot; y &quot;DVoD&quot;.<br>Los clientes pueden proporcionar valores personalizados para este parámetro. |
| [!UICONTROL Nombre del reproductor de contenido] | `playerName` | Cadena | **Requerido** Nombre del reproductor de contenido. |
| [!UICONTROL Canal de contenido] | `channel` | Cadena | **Requerido** El [!UICONTROL Canal de contenido] es el canal de distribución desde el que se reprodujo el contenido. |
| [!UICONTROL Versión] | `appVersion` | Cadena | La versión del SDK utilizada por el reproductor. Podría tener cualquier valor personalizado que sea adecuado para el reproductor. |
| [!UICONTROL Nombre de serie] | `show` | Cadena | El Nombre Del Programa O La Serie. El Nombre del programa solo es necesario si el programa forma parte de una serie. |
| [!UICONTROL Número de temporada] | `season` | Cadena | El [!UICONTROL Número de temporada] a la que pertenece el programa. La temporada solo es necesaria si el programa es un episodio de una serie. |
| [!UICONTROL Número de episodio] | `episode` | Cadena | El número del episodio. |
| [!UICONTROL ID de recurso] | `assetID` | Cadena | El [!UICONTROL ID de recurso] es el identificador único del contenido del recurso de contenidos, como el identificador de episodio de series de TV, el identificador de recursos de una película o el identificador de eventos en directo. Normalmente, estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden proceder de otros sistemas propietarios o internos. |
| [!UICONTROL Género] | `genre` | Cadena | El tipo o agrupación de contenido según lo definido por el productor de contenido. Los valores deben estar delimitados por comas en la implementación de variables. |
| [!UICONTROL Fecha de la primera emisión] | `firstAirDate` | Cadena | La fecha en la que el contenido se emitió por primera vez en televisión. Cualquier formato de fecha es aceptable, pero el Adobe recomienda: AAAA-MM-DD. |
| [!UICONTROL Fecha de la primera emisión digital] | `firstDigitalDate` | Cadena | La fecha en la que el contenido se emitió por primera vez en cualquier canal o plataforma digital. Cualquier formato de fecha es aceptable, pero el Adobe recomienda: AAAA-MM-DD. |
| [!UICONTROL Valor de clasificación] | `rating` | Cadena | La clasificación definida por las pautas de clasificación por edades de la TV. |
| [!UICONTROL  Nombre del creador] | `originator` | Cadena | Nombre del creador del contenido. |
| [!UICONTROL Red de difusión] | `network` | Cadena | El nombre de la red/canal. |
| [!UICONTROL Tipo de programa] | `showType` | Cadena | El tipo de contenido como, por ejemplo, tráiler o episodio completo. |
| [!UICONTROL Tipo de carga de publicidad] | `adLoad` | Cadena | El tipo de anuncio cargado según lo definido por la representación interna de cada cliente. |
| [!UICONTROL Identificador de MVPD] | `mvpd` | Cadena | El [!UICONTROL Identificador de MVPD] que se proporcionó mediante autenticación de Adobe. |
| [!UICONTROL Medios autorizados] | `authorized` | Cadena | Confirma si el usuario ha sido autorizado a través de la autenticación de Adobe. |
| [!UICONTROL Parte del día] | `dayPart` | Cadena | Propiedad que define la hora del día a la que se emitió o reprodujo el contenido. Podría tener cualquier valor establecido como petición del cliente |
| [!UICONTROL Tipo de fuente] | `feed` | Cadena | El tipo de fuente, que puede representar datos reales relacionados con la fuente, como EAST HD o SD, o el origen de la fuente, como una dirección URL. |
| [!UICONTROL Formato de flujo] | `streamFormat` | Cadena | El formato de la emisión (HD, SD). |
| [!UICONTROL Reanudar] | `hasResume` | Booleano | Marca cada reproducción que se reanudó después de más de 30 minutos de búfer, pausa o detención. |
| [!UICONTROL Tipo de emisión] | `streamType` | Cadena | El tipo de flujo de medios. |
| [!UICONTROL Artista] | `artist` | Cadena | El nombre del artista del álbum o del grupo que realiza la grabación musical o el vídeo. |
| [!UICONTROL Álbum] | `album` | Cadena | El nombre del álbum al que pertenece la grabación musical o el vídeo. |
| [!UICONTROL Etiqueta de registro] | `label` | Cadena | El nombre de la discográfica. |
| [!UICONTROL Autor] | `author` | Cadena | Nombre del autor de los medios. |
| [!UICONTROL Estación de radio] | `station` | Cadena | Nombre de la emisora de radio en la que se reproduce el audio. |
| [!UICONTROL Editor] | `publisher` | Cadena | Nombre del editor del contenido de audio. |
| [!UICONTROL Segmento de vídeo] | `segment` | Cadena | Intervalo que describe la parte del contenido que se ha visto en minutos. |
| [!UICONTROL Indicador de medios descargados] | `isDownloaded` | Booleano | El flujo se reprodujo localmente en el dispositivo después de descargarse. |
| [!UICONTROL Datos federados] | `isFederated` | Booleano | [!UICONTROL Datos federados] se establece en true cuando la visita está federada (es decir, recibida por el cliente como parte de un recurso compartido de datos federado, en lugar de su propia implementación). |
| [!UICONTROL Inicio de medios] | `isViewed` | Booleano | El evento de carga para los medios. Esto ocurre cuando el usuario selecciona el botón de reproducción. Esto cuenta incluso si hay anuncios previos a la emisión, almacenamiento en búfer, errores, etc. |
| [!UICONTROL Inicio de contenido] | `isPlayed` | Booleano | [!UICONTROL El contenido comienza] se vuelve verdadero cuando se consume el primer fotograma del contenido. Si el usuario lo cierra durante un anuncio, el almacenamiento en búfer, etc., no habrá [!UICONTROL El contenido comienza] evento. |
| [!UICONTROL El contenido finaliza] | `isCompleted` | Booleano | [!UICONTROL El contenido finaliza] indica si un recurso de medios cronometrados se vio hasta su finalización. Este evento no significa necesariamente que el usuario haya visto todo el vídeo, ya que podría haberse saltado algunas partes. |
| [!UICONTROL Tiempo invertido en contenido] | `timePlayed` | Número entero | [!UICONTROL Tiempo invertido en contenido] suma la duración del evento (en segundos) para todos los eventos de tipo REPRODUCIR en el contenido principal. |
| [!UICONTROL Tiempo invertido en contenido] | `totalTimePlayed` | Número entero | Describe la cantidad total de tiempo que un usuario dedica a un recurso de medios cronometrados específico, lo que incluye el tiempo viendo anuncios. |
| [!UICONTROL Tiempo de reproducción única] | `uniqueTimePlayed` | Número entero | Describe la suma de los intervalos únicos vistos por un usuario en un recurso de medios cronometrados; es decir, la duración de los intervalos de reproducción vistos varias veces solo se cuenta una vez. |
| [!UICONTROL Promedio de audiencia por minuto] | `averageMinuteAudience` | Número | Describe la media de tiempo dedicado al contenido de un elemento de medios específico; es decir, el tiempo total de contenido invertido dividido por la duración de todas las sesiones de reproducción. |
| [!UICONTROL Recuento de anuncios] | `adCount` | Número entero | El número de anuncios que comenzaron durante la reproducción. |
| [!UICONTROL Recuento de capítulos] | `chapterCount` | Número entero | El número de capítulos que comenzaron durante la reproducción. |
| [!UICONTROL Marcador de progreso al 10 %] | `hasProgress10` | Booleano | Indica que el cabezal de reproducción ha superado el marcador del 10% de los medios según la longitud del flujo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.   |
| [!UICONTROL Marcador de progreso del 25 %] | `hasProgress25` | Booleano | Indica que el cabezal de reproducción ha superado el marcador del 25% de los medios según la longitud del flujo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.   |
| [!UICONTROL Marcador de progreso al 50 %] | `hasProgress50` | Booleano | Indica que el cabezal de reproducción ha superado el marcador del 50 % de los medios según la longitud del flujo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.   |
| [!UICONTROL Marcador de progreso al 75 %] | `hasProgress75` | Booleano | Indica que el cabezal de reproducción ha superado el marcador del 75% de los medios según la longitud del flujo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.   |
| [!UICONTROL Marcador de progreso al 95 %] | `hasProgress95` | Booleano | Indica que el cabezal de reproducción ha superado el marcador del 95% de los medios según la longitud del flujo. El marcador se cuenta solo una vez, incluso hacia atrás. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.   |
| [!UICONTROL Flujos estimados] | `estimatedStreams` | Número | El número estimado de transmisiones de vídeo o audio para cada parte individual de contenido. |
| [!UICONTROL Pausar flujos afectados] | `hasPauseImpactedStreams` | Booleano | Indica si se han producido una o más pausas durante la reproducción de un solo elemento de medios. |
| [!UICONTROL Pausar eventos] | `pauseCount` | Número entero | [!UICONTROL Pausar eventos] cuenta el número de periodos de pausa que se produjeron durante la reproducción. |
| [!UICONTROL Duración total de la pausa] | `pauseTime` | Número entero | [!UICONTROL Duración total de la pausa] describe la duración en segundos durante la cual el usuario pausó la reproducción. |
| [!UICONTROL Vistas de segmentos de medios] | `hasSegmentView` | Booleano | [!UICONTROL Vistas de segmentos de medios] indica cuándo se ha visto al menos un fotograma, no necesariamente el primero. |
| [!UICONTROL Tiempo de espera del servidor de sesión multimedia] | `secondsSinceLastCall` | Número | El [!UICONTROL Tiempo de espera del servidor de sesión multimedia] indica la cantidad de tiempo en segundos que transcurrió entre la última interacción conocida del usuario y el momento en que se cerró la sesión. |
| [!UICONTROL Red de distribución de contenido] | `cdn` | Cadena | El [!UICONTROL Red de distribución de contenido] del contenido reproducido. |
| [!UICONTROL Pev3] | `pev3` | Cadena | [!UICONTROL Pev3] es el tipo de flujo de medios utilizado para los informes. |
| [!UICONTROL Rcp] | `pccr` | Booleano | [!UICONTROL Rcp] indica que se produjo una redirección. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
