---
title: Tipo de datos de colección de detalles publicitarios
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de recopilación de detalles publicitarios.
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 11%

---

# [!UICONTROL Detalles de publicidad] Tipo de datos de colección

[!UICONTROL Detalles de publicidad] La recopilación es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura atributos clave relacionados con los anuncios. Incluye información como el ID de anuncio, los ID de anunciante y de campaña, la duración, la posición dentro de una secuencia, los detalles sobre el reproductor que representa el anuncio, etc. Puede utilizar este tipo de datos para realizar un seguimiento y analizar diversos aspectos del rendimiento y la participación de los anuncios, así como para proporcionar información sobre cómo las audiencias interactúan con los distintos anuncios y responden a ellos. Esta información que proporciona se utiliza para rastrear los datos de flujo continuo.

+++Seleccione esta opción para mostrar un diagrama de la recopilación de detalles publicitarios.
![Diagrama del tipo de datos de recopilación de detalles publicitarios.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Anunciante de publicidad]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | string | No | La compañía o marca cuyo producto aparece en el anuncio. |
| [[!UICONTROL Campaña de publicidad]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | string | No | El ID de la campaña de publicidad. |
| [[!UICONTROL ID de creativo de publicidad]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | string | No | El ID del creador de la publicidad. |
| [[!UICONTROL URL de creatividad publicitaria]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | string | No | La URL del creador de la publicidad. |
| [[!UICONTROL Posición del anuncio en la secuencia (inicio del anuncio)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | entero | Sí | El índice del anuncio dentro del inicio del anuncio principal; por ejemplo, el primer anuncio tiene índice 0 y el segundo anuncio tiene índice 1. |
| [[!UICONTROL Duración O Duración Del Anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | entero | Sí | Duración del anuncio de vídeo en segundos. |
| [[!UICONTROL Nombre del anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | string | Sí | El nombre del anuncio en lenguaje natural. En los informes, “Nombre del anuncio” es la clasificación y “Nombre del anuncio (variable)” es la eVar. |
| [[!UICONTROL ID de colocación de anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | string | No | ID de colocación de la publicidad. |
| [[!UICONTROL Nombre del reproductor del anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | string | Sí | Nombre del reproductor responsable de procesar el anuncio. |
| [[!UICONTROL ID del sitio del anuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | string | No | El ID del sitio de publicidad. |
