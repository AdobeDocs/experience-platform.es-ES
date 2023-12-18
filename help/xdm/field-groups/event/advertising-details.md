---
title: Grupo de campos de esquema de detalles publicitarios
description: Obtenga información acerca del grupo de campos de esquema Detalles de publicidad.
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 4%

---

# [!UICONTROL Detalles de publicidad] grupo de campos de esquema

[!UICONTROL Detalles de publicidad] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo `advertising` objeto a un esquema, que captura información relacionada con impresiones publicitarias, clics y atribución.

![Estructura del grupo de campos](../../images/field-groups/advertising-details/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `adAssetReference` | Objeto | Registra información de recursos sobre el anuncio. Consulte la [subsección siguiente](#adAssetReference) para obtener más información sobre la estructura de este objeto. |
| `adAssetViewDetails` | Objeto | Registra los detalles de vista de la reproducción del anuncio. Consulte la [subsección siguiente](#adAssetViewDetails) para obtener más información sobre la estructura de este objeto. |
| `adViewability` | Objeto | Registra el número de impresiones que ven los usuarios finales, como el volumen del reproductor, la versión de la biblioteca, el estado de la ventana y las dimensiones de la ventanilla de publicidad. Consulte la [subsección siguiente](#adViewability) para obtener más información sobre la estructura de este objeto. |
| `clicks` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de acciones de clic en el anuncio. |
| `completes` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un recurso de medios cronometrados se vio hasta su finalización. Esto no significa necesariamente que el usuario final haya visto todo el vídeo, ya que puede haberse saltado algunas partes. |
| `conversions` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que una acción predefinida (o acciones) activó un evento para la evaluación del rendimiento. |
| `federated` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica si se creó un evento de experiencia mediante federación de datos, como el uso compartido de datos entre clientes. |
| `firstQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un anuncio de vídeo digital se ha reproducido al 25 % a velocidad normal. |
| `impressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de impresiones de publicidad enviadas a un usuario final con el potencial de ser visto. |
| `midpoints` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un anuncio de vídeo digital se ha reproducido al 50 % a velocidad normal. |
| `starts` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de veces que ha comenzado a reproducirse un anuncio de vídeo digital. |
| `thirdQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un anuncio de vídeo digital se ha reproducido al 75 % a velocidad normal. |
| `timePlayed` | [[!UICONTROL Medida]](../../data-types/measure.md) | Cantidad de tiempo que un usuario final dedica a un recurso de medios cronometrados específico. |
| `downloadedPlayback` | Booleano | Cuando se establece en `true`, indica que la visita se genera debido a la reproducción de una sesión de anuncio descargado. |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

El `adAssetReference` El objeto de captura información de recursos sobre el anuncio.

![estructura adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_dc.title` | Cadena | El nombre descriptivo y en lenguaje natural del recurso publicitario. |
| `_xmpDM.duration` | Número entero | La duración del recurso en segundos. |
| `_id` | Cadena | Un identificador único del recurso publicitario, a continuación del [Estándar de Ad-ID](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | Cadena | La compañía o marca cuyo producto aparece en el anuncio. |
| `campaign` | Cadena | El ID de la campaña de publicidad. |
| `creativeID` | Cadena | El ID del creador de la publicidad. |
| `creativeURL` | Cadena | La URL del creador de la publicidad. |
| `placementID` | Cadena | ID de colocación de la publicidad. |
| `siteID` | Cadena | El ID del sitio de publicidad. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

El `adAssetViewDetails` captura los detalles de vista de la reproducción del anuncio.

![estructura adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Pausa para anuncios]](../../data-types/ad-break.md) | Describe cómo se inserta un anuncio cronometrado en medios cronometrados. |
| `index` | Número entero | Índice de la publicidad dentro de la pausa para anuncios principal. Por ejemplo, el primer anuncio tiene un índice `0` y el segundo anuncio tiene un índice `1`. |
| `playerName` | Cadena | Nombre del reproductor responsable de procesar el anuncio. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

El `adViewability` El objeto captura el número de impresiones que ven los usuarios finales, como el volumen del reproductor, la versión de la biblioteca, el estado de la ventana y las dimensiones de la ventanilla de publicidad.

![estructura adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Detalles de implementación]](../../data-types/implementation-details.md) | Nombre y versión de la biblioteca instrumentada para medir las métricas de visibilidad. |
| `measuredAdNotVisible` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que el anuncio no es visible según lo medido por una biblioteca de visibilidad en el momento de la impresión. |
| `measuredMuted` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que el anuncio se silencia según lo medido por una biblioteca de visibilidad en el momento de la impresión. |
| `unmeasurableIframe` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que el anuncio se muestra en una ventana inactiva según lo medido por una biblioteca de visibilidad en el momento de la impresión. |
| `unmeasurableOther` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que la biblioteca de visibilidad no puede ejecutar las mediciones correctamente debido a que el anuncio se está mostrando dentro de un iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Impresiones de un anuncio para un usuario final con biblioteca de visibilidad instrumentada. |
| `viewabilityCompletes` | [[!UICONTROL Medida]](../../data-types/measure.md) | Finalizaciones de un anuncio para un usuario final que una biblioteca de visibilidad considera que este puede ver a la hora de finalización. |
| `viewableFirstQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | Primer/os cuartil/es de un anuncio para un usuario final que una biblioteca de visibilidad considera que este puede ver en el primer cuartil. |
| `viewableImpressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Impresiones de un anuncio para un usuario final que una biblioteca de visibilidad considera que este puede tras dos segundos de reproducción. |
| `viewableMidpoints` | [[!UICONTROL Medida]](../../data-types/measure.md) | Puntos intermedios de un anuncio para un usuario final que una biblioteca de visibilidad considera que este puede ver a mitad del juego. |
| `viewableThirdQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | Tercer/os cuartil/es de un anuncio para un usuario final que una biblioteca de visibilidad considera que este puede ver en el tercer cuartil. |
| `activeWindow` | Booleano | Indica si el anuncio se mostró en la ventana activa del dispositivo del usuario. |
| `adHeight` | Número entero | El número de píxeles verticales del reproductor, medidos en tiempo de ejecución. Este puede ser más grande que el tamaño del anuncio si el reproductor tiene controles o miniaturas adicionales. |
| `adUnitDepth` | Número entero | Los editores pueden insertar bloques de anuncios en contenedores (iFrames) para limitar el acceso del anuncio únicamente al código de la página. Este valor describe en cuántos contenedores se muestra la unidad publicitaria. |
| `adWidth` | Número entero | El número de píxeles horizontales del reproductor, medidos en tiempo de ejecución. Este puede ser más grande que el tamaño del anuncio si el reproductor tiene controles o miniaturas adicionales. |
| `measurementEligible` | Booleano | Si el anuncio se podía incluir o no en la medición de la visibilidad. Un anuncio es apto si la unidad tiene un formato creativo y un tipo de etiqueta compatibles. |
| `percentViewable` | Número entero | Porcentaje de píxeles del anuncio que se consideran visibles en el momento de tomar la medida. |
| `playerVolume` | Número entero | El porcentaje de volumen del reproductor medido en tiempo de ejecución, donde `0` está silenciado y `100` es el volumen máximo. |
| `viewable` | Booleano | Indica si el anuncio se pudo ver durante la ejecución. Los anuncios de visualización se consideran visibles cuando al menos el 50 % del anuncio es visible durante un segundo. Los anuncios de vídeo se consideran visibles cuando al menos el 50 % del anuncio es visible mientras el vídeo se reproduce durante al menos dos segundos consecutivos. |
| `viewportHeight` | Número entero | El tamaño vertical (en píxeles) de la ventana en la que se mostró la experiencia, medido en tiempo de ejecución. Para un evento de visualización web, este valor indica la altura de la ventana del explorador. |
| `viewportWidth` | Número entero | El tamaño horizontal (en píxeles) de la ventana en la que se mostró la experiencia, medido en tiempo de ejecución. Para un evento de visualización web, este valor indica la anchura de la ventanilla del explorador. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
