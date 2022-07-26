---
title: Grupo de campos de esquema de detalles publicitarios
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de publicidad .
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 11%

---

# [!UICONTROL Detalles publicitarios] grupo de campos de esquema

[!UICONTROL Detalles publicitarios] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). El grupo de campos proporciona un solo `advertising` a un esquema, que captura información relacionada con impresiones de publicidad, pulsaciones y atribución.

![Estructura del grupo de campo](../../images/field-groups/advertising-details/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `adAssetReference` | Objeto | Captura información de los recursos sobre el anuncio. Consulte la [subsección abajo](#adAssetReference) para obtener más información sobre la estructura de este objeto. |
| `adAssetViewDetails` | Objeto | Captura los detalles de vista para la reproducción del anuncio. Consulte la [subsección abajo](#adAssetViewDetails) para obtener más información sobre la estructura de este objeto. |
| `adViewability` | Objeto | Captura el número de impresiones que ven los usuarios finales, como el volumen del reproductor, la versión de la biblioteca, el estado de la ventana y las dimensiones de la ventanilla móvil. Consulte la [subsección abajo](#adViewability) para obtener más información sobre la estructura de este objeto. |
| `clicks` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de acciones de clic en el anuncio. |
| `completes` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de veces que se ha visto hasta el final un recurso de medios temporizados. Esto no significa necesariamente que el usuario final haya visto todo el vídeo, ya que puede que lo haya omitido. |
| `conversions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de veces que una acción predefinida (o acciones) activó un evento para la evaluación del rendimiento. |
| `federated` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica si se creó un evento de experiencia mediante una federación de datos, como el uso compartido de datos entre clientes. |
| `firstQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 25 % de su duración. |
| `impressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de impresiones de publicidad enviadas a un usuario final con el potencial de ser visualizadas. |
| `midpoints` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 50 % de su duración. |
| `starts` | [[!UICONTROL Medida]](../../data-types/measure.md) | Número de veces que se ha empezado a reproducir un anuncio de vídeo digital. |
| `thirdQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | El número de veces que un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 75 % de su duración. |
| `timePlayed` | [[!UICONTROL Medida]](../../data-types/measure.md) | Cantidad de tiempo que un usuario final emplea en un recurso de medios temporizados específico. |
| `downloadedPlayback` | Booleano | Cuando se configura como `true`, indica que la visita se genera debido a la reproducción de una sesión de publicidad descargada. |

{style=&quot;table-layout:auto&quot;}

## `adAssetReference` {#adAssetReference}

La variable `adAssetReference` captura la información del recurso sobre el anuncio.

![estructura adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_dc.title` | Cadena | Nombre descriptivo y legible por el usuario del recurso publicitario. |
| `_xmpDM.duration` | Número entero | Duración o duración del recurso en segundos. |
| `_id` | Cadena | Un identificador único del recurso publicitario que sigue a la variable [ID de anuncio estándar](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | Cadena | Empresa o marca cuyo producto aparece en el anuncio. |
| `campaign` | Cadena | ID de la campaña de publicidad. |
| `creativeID` | Cadena | El ID del creador de la publicidad. |
| `creativeURL` | Cadena | La dirección URL del creador de la publicidad. |
| `placementID` | Cadena | ID de colocación de la publicidad. |
| `siteID` | Cadena | ID del sitio de publicidad. |

{style=&quot;table-layout:auto&quot;}

## `adAssetViewDetails` {#adAssetViewDetails}

La variable `adAssetViewDetails` captura los detalles de vista para la reproducción del anuncio.

![estructura adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Pausa publicitaria]](../../data-types/ad-break.md) | Describe cómo se inserta un anuncio temporizado en un medio temporizado. |
| `index` | Número entero | Índice del anuncio dentro de la pausa publicitaria principal. Por ejemplo, el primer anuncio tiene un índice `0` y el segundo anuncio tiene índice `1`. |
| `playerName` | Cadena | Nombre del reproductor responsable de procesar el anuncio. |

{style=&quot;table-layout:auto&quot;}

## `adViewability` {#adViewability}

La variable `adViewability` captura el número de impresiones que ven los usuarios finales, como el volumen del reproductor, la versión de la biblioteca, el estado de la ventana y las dimensiones de la ventanilla móvil.

![estructura adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Detalles de implementación]](../../data-types/implementation-details.md) | Nombre y versión de la biblioteca instrumentada para medir las métricas de visibilidad. |
| `measuredAdNotVisible` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que la publicidad no está visible según la medición de una biblioteca de visualizaciones en el momento de la impresión. |
| `measuredMuted` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que el anuncio está silenciado según la medición de una biblioteca de visualizaciones en el momento de la impresión. |
| `unmeasurableIframe` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que la publicidad se muestra en una ventana inactiva, según la medición de la biblioteca de visualizaciones en el momento de la impresión. |
| `unmeasurableOther` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que la biblioteca de visualizaciones no puede ejecutar correctamente las mediciones debido a que la publicidad se muestra dentro de un iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Impresión(s) de un anuncio a un usuario final con biblioteca de visibilidad instrumentada. |
| `viewabilityCompletes` | [[!UICONTROL Medida]](../../data-types/measure.md) | Finalización(es) de un anuncio a un usuario final que una biblioteca de visualizaciones considere visible en el momento de la finalización. |
| `viewableFirstQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | Primer cuartil de un anuncio a un usuario final considerado visible en el primer cuartil de reproducción por una biblioteca de visualizaciones. |
| `viewableImpressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Impresiones de un anuncio para un usuario final que una biblioteca de visualizaciones considere visible después de dos segundos de reproducción. |
| `viewableMidpoints` | [[!UICONTROL Medida]](../../data-types/measure.md) | Punto medio de un anuncio a un usuario final considerado visible en el punto medio de reproducción por una biblioteca de visualizaciones. |
| `viewableThirdQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | Tercer cuartil de un anuncio a un usuario final considerado visible en el tercer cuartil de reproducción por una biblioteca de visualizaciones. |
| `activeWindow` | Booleano | Indica si el anuncio se mostró en la ventana activa del dispositivo del usuario. |
| `adHeight` | Número entero | Número de píxeles verticales del reproductor, medidos durante la ejecución. Puede ser mayor que el tamaño del anuncio si el reproductor tiene controles o miniaturas adicionales. |
| `adUnitDepth` | Número entero | Los editores pueden incrustar unidades de publicidad dentro de contenedores (iFrames) para limitar el acceso de la publicidad únicamente al código de la página. Este valor describe cuántos contenedores de la unidad de publicidad se muestran dentro de. |
| `adWidth` | Número entero | Número de píxeles horizontales del reproductor, medidos durante la ejecución. Puede ser mayor que el tamaño del anuncio si el reproductor tiene controles o miniaturas adicionales. |
| `measurementEligible` | Booleano | Indica si el anuncio fue elegible para la medición de la capacidad de visualización. Una publicidad es apta si la unidad tiene un formato creativo admitido y un tipo de etiqueta. |
| `percentViewable` | Número entero | El porcentaje de píxeles del anuncio que se considera visible en el momento de la medición. |
| `playerVolume` | Número entero | El porcentaje de volumen del reproductor medido durante la ejecución, donde `0` está silenciado y `100` es el volumen máximo. |
| `viewable` | Booleano | Indica si la publicidad se pudo ver durante la ejecución. Los anuncios en pantalla se consideran visibles cuando al menos el 50% de la publicidad es visible durante al menos un segundo. Los anuncios de vídeo se consideran visibles cuando al menos el 50 % del anuncio está visible mientras el vídeo se reproduce durante al menos dos segundos consecutivos. |
| `viewportHeight` | Número entero | Tamaño vertical (en píxeles) de la ventana en la que se mostró la experiencia dentro de la medición durante la ejecución. Para un evento de vista web, este valor indica la altura de la ventanilla del explorador. |
| `viewportWidth` | Número entero | El tamaño horizontal (en píxeles) de la ventana en la que se mostró la experiencia dentro de la medición durante la ejecución. Para un evento de vista web, este valor indica la anchura de la ventanilla del explorador. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
