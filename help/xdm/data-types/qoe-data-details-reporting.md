---
title: Datos de QoE (calidad de experiencia) Detalles del tipo de datos del informe
description: Obtenga información sobre el tipo de datos de QoE (calidad de experiencia) Detalles de datos de informe Tipo de datos Modelo de datos de experiencia (XDM).
exl-id: 608baa9b-12ca-466c-a962-1401abc0344e
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# Tipo de datos de informes Detalles de datos de QoE (calidad de experiencia)

[!UICONTROL Detalles de datos de QoE] La creación de informes es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona métricas detalladas relacionadas con la calidad de experiencia (QoE) durante la reproducción de contenido. Use el tipo de datos de informe [!UICONTROL Detalles de datos de QoE] para capturar detalles como información de velocidad de bits, velocidad de fotogramas, eventos de almacenamiento en búfer, fotogramas perdidos, etc. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos que envían los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican. Este tipo de datos permite el análisis de la calidad de la reproducción, lo que permite obtener información sobre el rendimiento del streaming, la experiencia del usuario y los posibles problemas encontrados durante las sesiones de reproducción.

+++Seleccione esta opción para mostrar el tipo de datos de informes Detalles de datos de QoE.
![Un diagrama del tipo de datos de informes de detalles de datos de QoE (calidad de experiencia).](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL Velocidad de bits media]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate-1) | `bitrateAverage` | número | Velocidad de bits media (en kbps, total). Se calcula como una media ponderada de los valores de velocidad de bits. |
| [[!UICONTROL Promedio de espacio de velocidad de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrateAverageBucket` | cadena | Velocidad de bits media (en kbps) clasificada en bloques predefinidos a intervalos de 100 kbps. |
| [[!UICONTROL Velocidad de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | entero | El valor de velocidad de bits (en kbps). |
| [[!UICONTROL Transmisiones afectadas por el cambio de velocidad de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | Booleano | Indica si los cambios en la velocidad de bits afectaron a los flujos durante la reproducción. |
| [[!UICONTROL Cambios de velocidad de bits]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-changes) | `bitrateChangeCount` | entero | Recuento total de cambios en la velocidad de bits durante la reproducción. |
| [[!UICONTROL Eventos de búfer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-events) | `bufferCount` | entero | Recuento de diferentes estados de búfer durante la reproducción. |
| [[!UICONTROL Flujos afectados por el búfer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-impacted-streams) | `hasBufferImpactedStreams` | Booleano | Indica si los flujos se vieron afectados por el almacenamiento en búfer durante la reproducción. |
| [[!UICONTROL Flujos afectados por la pérdida de fotogramas]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | Booleano | Indica si los flujos se vieron afectados por los fotogramas perdidos durante la reproducción. |
| [[!UICONTROL Fotogramas perdidos]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames-1) | `droppedFrames` | entero | Recuento total de fotogramas descartados durante la reproducción. |
| [[!UICONTROL Pérdidas antes del inicio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#drops-before-start) | `isDroppedBeforeStart` | Booleano | Indica si los usuarios abandonan el vídeo antes de su inicio, independientemente de los anuncios. |
| [[!UICONTROL Transmisiones afectadas por el error]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#error-impacted-streams) | `hasErrorImpactedStreams` | Booleano | Indica si los flujos experimentaron errores durante la reproducción. |
| [[!UICONTROL Errores]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#errors-%2F-error-events) | `errorCount` | entero | Recuento total de errores que se produjeron durante la reproducción. |
| [[!UICONTROL Id. de error externo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#external-error-ids) | `externalErrors` | matriz de cadenas | ID de error únicos procedentes de fuentes externas, como errores de CDN. |
| [[!UICONTROL Fotogramas Por Segundo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | entero | Velocidad de fotogramas de la secuencia actual (en fotogramas por segundo). |
| [[!UICONTROL ID de error de Media SDK]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#media-sdk-error-ids) | `mediaSdkErrors` | matriz de cadenas | ID de error únicos generados por Media SDK durante la reproducción. |
| [[!UICONTROL ID de error del SDK del reproductor]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#player-sdk-error-ids) | `playerSdkErrors` | matriz de cadenas | ID de error únicos generados por el SDK de reproductor durante la reproducción. |
| [[!UICONTROL Eventos de demora]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-events) | `stallCount` | entero | Recuento de eventos de demora durante la reproducción. |
| [[!UICONTROL Flujos afectados por estancamiento]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-impacted-streams) | `hasStallImpactedStreams` | Booleano | Indica si las transmisiones experimentaron un estancamiento durante la reproducción. |
| [[!UICONTROL Tiempo Para El Inicio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | entero | Duración (en segundos) entre la carga y el inicio del vídeo. |
| [[!UICONTROL Duración total del búfer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-buffer-duration-1) | `bufferTime` | entero | Tiempo total (en segundos) invertido en el almacenamiento en búfer durante la reproducción. |
| [[!UICONTROL Duración total de demora]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-stalling-duration) | `stallTime` | entero | El tiempo total (en segundos) que la reproducción se detuvo durante la reproducción. |

{style="table-layout:auto"}
