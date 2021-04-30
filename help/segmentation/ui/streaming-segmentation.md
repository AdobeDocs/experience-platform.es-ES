---
keywords: Experience Platform;inicio;temas populares;segmentación de flujo continuo;Segmentación;Servicio de segmentación;servicio de segmentación;guía de interfaz de usuario;
solution: Experience Platform
title: Guía de la interfaz de usuario de segmentación por transmisión
topic-legacy: ui guide
description: La segmentación por transmisión en Adobe Experience Platform le permite realizar segmentación en tiempo casi real, mientras se centra en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos llegan a Platform, lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a Platform, lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: b4a04b52ff9a2b7a36fda58d70a2286fea600ff1
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# Segmentación por transmisión

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la interfaz de usuario de . Para obtener información sobre el uso de la segmentación de flujo continuo mediante la API, consulte la [guía de la API de segmentación de flujo continuo](../api/streaming-segmentation.md).

La segmentación por transmisión en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real, mientras se concentra en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos de flujo continuo llegan a [!DNL Platform], lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar ya que los datos se pasan a [!DNL Platform], lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

>[!NOTE]
>
>La segmentación por transmisión solo se puede utilizar para evaluar los datos que se transmiten a Platform. En otras palabras, los datos ingeridos mediante la ingesta por lotes no se evaluarán mediante la segmentación de flujo continuo y se evaluarán junto con el trabajo de segmento programado por la noche.
>
>Además, los segmentos evaluados con la segmentación de flujo continuo pueden variar entre la pertenencia ideal y real si el segmento se basa en otro segmento que se evalúa mediante la segmentación por lotes. Por ejemplo, si el segmento A se basa en el segmento B y el segmento B se evalúa mediante la segmentación por lotes, ya que el segmento B solo se actualiza cada 24 horas, el segmento A se alejará más de los datos reales hasta que se vuelva a sincronizar con la actualización del segmento B.

## Tipos de consultas de segmentación por transmisión

>[!NOTE]
>
>Para que la segmentación de flujo continuo funcione, debe habilitar la segmentación programada para la organización. Para obtener más información sobre la activación de la segmentación programada, consulte [la sección de segmentación de flujo continuo en la guía del usuario de segmentación](./overview.md#scheduled-segmentation).

Una consulta se evaluará automáticamente con la segmentación de flujo continuo si cumple cualquiera de los siguientes criterios:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Visita entrante dentro de un periodo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Visita entrante con una ventana de tiempo | Cualquier definición de segmento que haga referencia a un solo evento entrante con un intervalo de tiempo. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |  |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Visita entrante que hace referencia a un perfil dentro de un periodo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o más atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se utiliza un segmento de segmentos, la descalificación del perfil se producirá  **cada 24 horas**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Varios eventos que hacen referencia a un perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o más atributos de perfil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Una definición de segmento **no** se habilitará para la segmentación de flujo continuo en los siguientes escenarios:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager (AAM).
- La definición del segmento incluye varias entidades (consultas de varias entidades).

Además, se aplican algunas directrices al realizar segmentación de flujo continuo:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva está limitada a **un día**.</li><li>Existe una condición estricta de ordenación de tiempo **debe** entre los eventos.</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición del segmento pasará automáticamente de &quot;Transmisión&quot; a &quot;Lote&quot;.

## Detalles del segmento de segmentación por transmisión

Después de crear un segmento con la transmisión habilitada, puede ver los detalles de ese segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

En concreto, se muestran detalles sobre **[!UICONTROL total qualified audience size]**. El **[!UICONTROL Total qualified audience size]** muestra el número total de audiencias cualificadas de la última ejecución de trabajo de segmentos completada. Si un trabajo de segmento no se completó en las últimas 24 horas, el número de audiencias se tomará de una estimación en su lugar.

Debajo hay un gráfico de líneas que muestra el número de segmentos calificados y descalificados en las últimas 24 horas. La lista desplegable se puede ajustar para mostrar las últimas 24 horas, la semana pasada o los últimos 30 días.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Para obtener información adicional sobre la última evaluación de segmentos, seleccione la burbuja de información.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obtener más información sobre las definiciones de segmentos, lea la sección anterior sobre [detalles de definición de segmentos](#segment-details).

## Pasos siguientes

En esta guía del usuario se explica cómo funcionan las definiciones de segmentos con transmisión habilitada en Adobe Experience Platform y cómo se monitorizan los segmentos con transmisión habilitada.

Para obtener más información sobre el uso de la interfaz de usuario de Adobe Experience Platform, lea la [Guía del usuario de segmentación](./overview.md).
