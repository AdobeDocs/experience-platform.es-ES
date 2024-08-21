---
title: Tipo de datos de colección de detalles de Advertising
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de recopilación de detalles de Advertising.
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 14%

---

# [!UICONTROL Detalles de Advertising] Tipo de datos de colección

La colección [!UICONTROL Detalles de Advertising] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura atributos clave relacionados con los anuncios. Incluye información como el ID de anuncio, los ID de anunciante y de campaña, la duración, la posición dentro de una secuencia, los detalles sobre el reproductor que representa el anuncio, etc. Puede utilizar este tipo de datos para realizar un seguimiento y analizar diversos aspectos del rendimiento y la participación de los anuncios, así como para proporcionar información sobre cómo las audiencias interactúan con los distintos anuncios y responden a ellos. Esta información que proporciona se utiliza para rastrear los datos de flujo continuo.

+++Seleccione esta opción para mostrar un diagrama del tipo de datos de la recopilación de detalles de Advertising.
![Un diagrama del tipo de datos de la colección de detalles de Advertising.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Anunciante de anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | cadena | No | La compañía o marca cuyo producto aparece en el anuncio. |
| [[!UICONTROL Campaña de publicidad]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | cadena | No | El ID de la campaña de publicidad. |
| [[!UICONTROL ID de creativo de publicidad]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | cadena | No | El ID de creatividad publicitaria. |
| [[!UICONTROL URL de creatividad publicitaria]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | cadena | No | El URL de creatividad publicitaria. |
| [[!UICONTROL Posición Del Anuncio En La Pod (Inicio Del Anuncio)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | entero | Sí | El índice del anuncio dentro del inicio del anuncio principal; por ejemplo, el primer anuncio tiene índice 0 y el segundo anuncio tiene índice 1. |
| [[!UICONTROL Duración O Longitud Del Anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | entero | Sí | Duración del anuncio de vídeo en segundos. |
| [[!UICONTROL Nombre del anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | cadena | Sí | El nombre del anuncio en lenguaje natural. En los informes, &quot;Nombre del anuncio&quot; es la clasificación y &quot;Nombre del anuncio (variable)&quot; es el eVar. |
| [[!UICONTROL ID. de colocación de anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | cadena | No | ID de colocación de la publicidad. |
| [[!UICONTROL Nombre del reproductor del anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | cadena | Sí | El nombre del reproductor responsable de reproducir el anuncio. |
| [[!UICONTROL Id. de sitio de publicidad]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | cadena | No | El ID del sitio de publicidad. |

{style="table-layout:auto"}
