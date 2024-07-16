---
title: Tipo de datos de informes de detalles de Advertising
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de creación de informes de detalles de Advertising.
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Detalles de Advertising] Tipo de datos de informe

[!UICONTROL Detalles de Advertising] La creación de informes es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura atributos clave relacionados con los anuncios. Incluye información como el ID de anuncio, los ID de anunciante y de campaña, la duración, la posición dentro de una secuencia, los detalles sobre el reproductor que representa el anuncio, etc. Puede utilizar este tipo de datos para realizar un seguimiento y analizar diversos aspectos del rendimiento y la participación de los anuncios, así como para proporcionar información sobre cómo las audiencias interactúan con los distintos anuncios y responden a ellos.

+++Seleccione esta opción para mostrar un diagrama del tipo de datos de informes de detalles de Advertising.
![Un diagrama del tipo de datos de informes de detalles de Advertising.](../images/data-types/advertising-details-information.png)
+++

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nombre del anuncio] | `friendlyName` | cadena | El nombre del anuncio en lenguaje natural. En los informes, &quot;Nombre del anuncio&quot; es la clasificación y &quot;Nombre del anuncio (variable)&quot; es el eVar. |
| [!UICONTROL ID de anuncio] | `name` | cadena | El ID de la publicidad. Cualquier combinación de números enteros o letras. |
| [!UICONTROL Duración O Longitud Del Anuncio] | `length` | entero | Duración del anuncio de vídeo en segundos. |
| [!UICONTROL Posición Del Anuncio En La Pod (Inicio Del Anuncio)] | `podPosition` | entero | El índice del anuncio dentro del inicio del anuncio principal; por ejemplo, el primer anuncio tiene índice 0 y el segundo anuncio tiene índice 1. |
| [!UICONTROL Nombre del reproductor del anuncio] | `playerName` | cadena | El nombre del reproductor responsable de reproducir el anuncio. |
| [!UICONTROL Anunciante de anuncio] | `advertiser` | cadena | La compañía o marca cuyo producto aparece en el anuncio. |
| [!UICONTROL Campaña de publicidad] | `campaignID` | cadena | El ID de la campaña de publicidad. |
| [!UICONTROL ID de creativo de publicidad] | `creativeID` | cadena | El ID de creatividad publicitaria. |
| [!UICONTROL Agregar ID de sitio] | `siteID` | cadena | El ID del sitio de publicidad. |
| [!UICONTROL URL de creatividad publicitaria] | `creativeURL` | cadena | El URL de creatividad publicitaria. |
| [!UICONTROL ID de colocación de anuncio] | `placementID` | cadena | ID de colocación de la publicidad. |
| [!UICONTROL Anuncio completado] | `isCompleted` | Booleano | Registra si el anuncio se ha completado. |
| [!UICONTROL Anuncio iniciado] | `isStarted` | Booleano | Registra si el anuncio se ha iniciado. |
| [!UICONTROL Tiempo de publicidad reproducido] | `timePlayed` | entero | Cantidad total de tiempo, en segundos, que se emplea para ver el anuncio (es decir, el número de segundos reproducidos). |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
