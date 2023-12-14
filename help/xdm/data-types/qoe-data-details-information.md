---
title: Tipo de datos de información de detalles de datos de QoE (calidad de experiencia)
description: Obtenga información sobre el tipo de datos de QoE (calidad de experiencia) Información Tipo de datos Modelo de datos de experiencia (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# Tipo de datos de información de detalles de datos de QoE (calidad de experiencia)

[!UICONTROL Información de detalles de datos de QoE] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona métricas detalladas relacionadas con la calidad de la experiencia (QoE) durante la reproducción de contenido. Utilice el [!UICONTROL Información de detalles de datos de QoE] tipo de datos para capturar detalles como información de velocidad de bits, velocidad de fotogramas, eventos de almacenamiento en búfer, fotogramas perdidos, etc. Este tipo de datos permite el análisis de la calidad de la reproducción, lo que permite obtener información sobre el rendimiento del streaming, la experiencia del usuario y los posibles problemas encontrados durante las sesiones de reproducción.

+++Seleccione esta opción para mostrar el tipo de datos Información de detalles de datos de QoE.
![Un diagrama del tipo de datos de información de detalles de datos de QoE (calidad de experiencia).](../images/data-types/qoe-data-details-information.png)
+++

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL Contenedor de velocidad de bits media] | `bitrateAverageBucket` | string | Velocidad de bits media (en kbps) clasificada en bloques predefinidos a intervalos de 100 kbps. |
| [!UICONTROL Velocidad de bits] | `bitrate` | entero | El valor de velocidad de bits (en kbps). |
| [!UICONTROL Velocidad de bits media] | `bitrateAverage` | number | Velocidad de bits media (en kbps, total). Se calcula como una media ponderada de los valores de velocidad de bits. |
| [!UICONTROL Flujos afectados por el cambio de velocidad] | `hasBitrateChangeImpactedStreams` | Booleano | Indica si los cambios en la velocidad de bits afectaron a los flujos durante la reproducción. |
| [!UICONTROL Cambios de velocidad de bits] | `bitrateChangeCount` | entero | Recuento total de cambios en la velocidad de bits durante la reproducción. |
| [!UICONTROL Flujos afectados por la pérdida de cuadros] | `hasDroppedFrameImpactedStreams` | Booleano | Indica si los flujos se vieron afectados por los fotogramas perdidos durante la reproducción. |
| [!UICONTROL Fotogramas perdidos] | `droppedFrames` | entero | Recuento total de fotogramas descartados durante la reproducción. |
| [!UICONTROL Pérdidas antes del inicio] | `isDroppedBeforeStart` | Booleano | Indica si los usuarios abandonan el vídeo antes de su inicio, independientemente de los anuncios. |
| [!UICONTROL Fotogramas por segundo] | `framesPerSecond` | entero | Velocidad de fotogramas de la secuencia actual (en fotogramas por segundo). |
| [!UICONTROL Tiempo para el inicio] | `timeToStart` | entero | Duración (en segundos) entre la carga y el inicio del vídeo. |
| [!UICONTROL Flujos afectados por búfer] | `hasBufferImpactedStreams` | Booleano | Indica si los flujos se vieron afectados por el almacenamiento en búfer durante la reproducción. |
| [!UICONTROL Eventos de búfer] | `bufferCount` | entero | Recuento de diferentes estados de búfer durante la reproducción. |
| [!UICONTROL Duración total del búfer] | `bufferTime` | entero | Tiempo total (en segundos) invertido en el almacenamiento en búfer durante la reproducción. |
| [!UICONTROL Flujos afectados por error] | `hasErrorImpactedStreams` | Booleano | Indica si los flujos experimentaron errores durante la reproducción. |
| [!UICONTROL Errores] | `errorCount` | entero | Recuento total de errores que se produjeron durante la reproducción. |
| [!UICONTROL Flujos afectados por estancamiento] | `hasStallImpactedStreams` | Booleano | Indica si las transmisiones experimentaron un estancamiento durante la reproducción. |
| [!UICONTROL Eventos de demora] | `stallCount` | entero | Recuento de eventos de demora durante la reproducción. |
| [!UICONTROL Duración total del estancamiento] | `stallTime` | entero | El tiempo total (en segundos) que la reproducción se detuvo durante la reproducción. |
| [!UICONTROL ID de error del SDK del reproductor] | `playerSdkErrors` | matriz de cadenas | ID de error únicos generados por el SDK de reproductor durante la reproducción. |
| [!UICONTROL ID de error externo] | `externalErrors` | matriz de cadenas | ID de error únicos procedentes de fuentes externas, como errores de CDN. |
| [!UICONTROL ID de error de Media SDK] | `mediaSdkErrors` | matriz de cadenas | ID de error únicos generados por Media SDK durante la reproducción. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

