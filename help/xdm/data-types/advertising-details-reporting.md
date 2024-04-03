---
title: Tipo de datos de informes de detalles publicitarios
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia (XDM) de creación de informes de detalles publicitarios.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 11%

---

# [!UICONTROL Detalles de publicidad] Tipo de datos de informes

[!UICONTROL Detalles de publicidad] Los informes son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura atributos clave relacionados con los anuncios. Incluye información como el ID de anuncio, los ID de anunciante y de campaña, la duración, la posición dentro de una secuencia, los detalles sobre el reproductor que representa el anuncio, etc. Puede utilizar este tipo de datos para realizar un seguimiento y analizar diversos aspectos del rendimiento y la participación de los anuncios, así como para proporcionar información sobre cómo las audiencias interactúan con los distintos anuncios y responden a ellos.

+++Seleccione esta opción para mostrar un diagrama del tipo de datos del informe de detalles publicitarios.
![Diagrama del tipo de datos de creación de informes de detalles publicitarios.](../images/data-types/advertising-details-information.png)
+++

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nombre del anuncio] | `friendlyName` | string | El nombre del anuncio en lenguaje natural. En los informes, “Nombre del anuncio” es la clasificación y “Nombre del anuncio (variable)” es la eVar. |
| [!UICONTROL ID de anuncio] | `name` | string | El ID de la publicidad. Cualquier combinación de números enteros y/o letras. |
| [!UICONTROL Duración O Duración Del Anuncio] | `length` | entero | Duración del anuncio de vídeo en segundos. |
| [!UICONTROL Posición del anuncio en la secuencia (inicio del anuncio)] | `podPosition` | entero | El índice del anuncio dentro del inicio del anuncio principal; por ejemplo, el primer anuncio tiene índice 0 y el segundo anuncio tiene índice 1. |
| [!UICONTROL Nombre del reproductor del anuncio] | `playerName` | string | Nombre del reproductor responsable de procesar el anuncio. |
| [!UICONTROL Anunciante de publicidad] | `advertiser` | string | La compañía o marca cuyo producto aparece en el anuncio. |
| [!UICONTROL Campaña de publicidad] | `campaignID` | string | El ID de la campaña de publicidad. |
| [!UICONTROL ID de creativo de publicidad] | `creativeID` | string | El ID del creador de la publicidad. |
| [!UICONTROL ID del sitio del anuncio] | `siteID` | string | El ID del sitio de publicidad. |
| [!UICONTROL URL de creatividad publicitaria] | `creativeURL` | string | La URL del creador de la publicidad. |
| [!UICONTROL ID de colocación de anuncio] | `placementID` | string | ID de colocación de la publicidad. |
| [!UICONTROL Anuncio completado] | `isCompleted` | Booleano | Registra si el anuncio se ha completado. |
| [!UICONTROL Anuncio iniciado] | `isStarted` | Booleano | Registra si el anuncio se ha iniciado. |
| [!UICONTROL Tiempo de publicidad reproducida] | `timePlayed` | entero | Cantidad total de tiempo, en segundos, que se emplea para ver el anuncio (es decir, el número de segundos reproducidos). |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
