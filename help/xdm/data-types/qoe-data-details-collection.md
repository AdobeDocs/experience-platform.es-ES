---
title: Tipo de datos de recopilación de detalles de datos de QoE (calidad de experiencia)
description: Obtenga información sobre el tipo de datos de QoE (calidad de experiencia) Detalles de recopilación de datos Tipo de datos Modelo de datos de experiencia (XDM).
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# Tipo de datos de recopilación de detalles de datos de QoE (calidad de experiencia)

[!UICONTROL Datos de QoE] La recopilación es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona métricas detalladas relacionadas con la calidad de la experiencia (QoE) durante la reproducción de contenido. Utilice el [!UICONTROL Datos de QoE] Tipo de datos de recopilación para capturar detalles como información de velocidad de bits, velocidad de fotogramas, eventos de almacenamiento en búfer, fotogramas perdidos, etc. Los campos de recopilación de medios capturan datos y los envían a otros servicios de Adobe para un procesamiento posterior. Este tipo de datos permite el análisis de la calidad de la reproducción, lo que permite obtener información sobre el rendimiento del streaming, la experiencia del usuario y los posibles problemas encontrados durante las sesiones de reproducción.

+++Seleccione para mostrar el tipo de datos Detalles de datos de QoE.
![Diagrama del tipo de datos de recopilación de detalles de datos de QoE (calidad de experiencia).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Velocidad de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | entero | No | El valor de velocidad de bits (en kbps). |
| [[!UICONTROL Fotogramas perdidos]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | entero | No | Recuento total de fotogramas descartados durante la reproducción. |
| [[!UICONTROL Fotogramas por segundo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | entero | No | Velocidad de fotogramas de la secuencia actual (en fotogramas por segundo). |
| [[!UICONTROL Tiempo para el inicio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | entero | No | Duración (en segundos) entre la carga y el inicio del vídeo. |

{style="table-layout:auto"}
