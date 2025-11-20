---
title: Monitorización de audiencias de streaming
description: Aprenda a utilizar el panel de monitorización para monitorizar las audiencias que se evalúan mediante la segmentación de streaming
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 6%

---


# Monitorización de audiencias de streaming

introducción a blurb

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Flujos de datos](../home.md): Los flujos de datos representan trabajos de datos que transfieren información a través de Experience Platform. Se configuran en varios servicios para facilitar el movimiento de datos desde los conectores de origen a los conjuntos de datos de destino, así como al servicio de identidad, el perfil del cliente en tiempo real y los destinos.
* [Servicio de segmentación](../../segmentation/home.md):
* [Capacidades](../../landing/license-usage-and-guardrails/capacity.md): en Experience Platform, las capacidades le permiten saber si su organización ha superado alguna de sus protecciones y le proporcionan información sobre cómo solucionar estos problemas.

## Métricas de monitorización para audiencias de streaming {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Tasa de evaluación"
>abstract="Esta métrica representa el número de registros evaluados por segundo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="Latencia de ingesta de P95"
>abstract="Esta métrica mide la latencia del percentil 95 de un evento que llega a Adobe Experience Platform para una evaluación correcta de la audiencia."
>text="Learn more in documentation"

La siguiente tabla proporciona información más detallada sobre las métricas que se utilizan para las audiencias de streaming.

| Métrica | Descripción | Dimensiones |
| ------ | ----------- | ---------- |
| Tasa de evaluación | Número de evaluaciones de audiencia procesadas por segundo. | Espacio aislado, Conjunto de datos |
| Latencia de ingesta de P95 | Latencia del percentil 95 de la llegada del evento de éxito a la audiencia. | Espacio aislado, Conjunto de datos |
| Registros recibidos | Número total de registros recibidos de la ingesta de transmisión para la segmentación de transmisión durante la ventana de tiempo seleccionada. | Conjunto de datos |
| Registros evaluados | Número total de registros que **evaluó correctamente** mediante la segmentación de flujo continuo durante la ventana de tiempo seleccionada. | Conjunto de datos |
| Error de registros | Número total de registros que **no superaron** la evaluación en la segmentación de flujo continuo debido a errores durante la ventana de tiempo seleccionada. | Conjunto de datos, ejecución de flujo |
| Registros omitidos | El número total de registros que **omitió** la evaluación en la segmentación de flujo continuo debido a errores durante la ventana de tiempo seleccionada. | Conjunto de datos, ejecución de flujo |
| Perfiles cualificados | El número de perfiles que se clasificaron para la audiencia durante la ventana de tiempo seleccionada. | Zona protegida, Audiencia |
| Perfiles descalificados | El número de perfiles que se descalificaron de la audiencia durante la ventana de tiempo seleccionada. | Zona protegida, Audiencia |

{style="table-layout:auto"}

## Uso del panel de monitorización para audiencias de streaming {#monitoring-dashboard}

Para acceder al panel de monitorización de las audiencias de streaming, vaya a la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Monitoring]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Streaming end-to-end]**.

IMAGEN

En la parte superior del panel se encuentra la tarjeta de métrica **[!UICONTROL Audiences]**. Muestra información sobre **la tasa de evaluación** de las audiencias.