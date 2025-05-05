---
title: Tipo de datos de recopilación de detalles de datos de QoE (calidad de experiencia)
description: Obtenga información sobre el tipo de datos de QoE (calidad de experiencia) Detalles de recopilación de datos Tipo de datos Modelo de datos de experiencia (XDM).
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# Tipo de datos de recopilación de detalles de datos de QoE (calidad de experiencia)

[!UICONTROL Detalles de datos de QoE] La colección es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona métricas detalladas relacionadas con la calidad de experiencia (QoE) durante la reproducción de contenido. Utilice el tipo de datos de colección [!UICONTROL Detalles de datos de QoE] para capturar detalles como información de velocidad de bits, velocidad de fotogramas, eventos de almacenamiento en búfer, fotogramas perdidos, etc. Los campos de recopilación de medios capturan datos y los envían a otros servicios de Adobe para un procesamiento posterior. Este tipo de datos permite el análisis de la calidad de la reproducción, lo que permite obtener información sobre el rendimiento del streaming, la experiencia del usuario y los posibles problemas encontrados durante las sesiones de reproducción.

+++Seleccione para mostrar el tipo de datos Detalles de datos de QoE.
![Un diagrama del tipo de datos de recopilación de detalles de datos de QoE (calidad de experiencia).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Velocidad de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=es#average-bitrate) | `bitrate` | entero | No | El valor de velocidad de bits (en kbps). |
| [[!UICONTROL Fotogramas perdidos]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=es#dropped-frames) | `droppedFrames` | entero | No | Recuento total de fotogramas descartados durante la reproducción. |
| [[!UICONTROL Fotogramas Por Segundo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=es#frames-per-second) | `framesPerSecond` | entero | No | Velocidad de fotogramas de la secuencia actual (en fotogramas por segundo). |
| [[!UICONTROL Tiempo Para El Inicio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=es#time-to-start-1) | `timeToStart` | entero | No | Duración (en segundos) entre la carga y el inicio del vídeo. |

{style="table-layout:auto"}
