---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: Segmentación por flujo continuo
topic: ui guide
description: La segmentación por flujo continuo en Adobe Experience Platform le permite realizar la segmentación en tiempo casi real mientras se centra en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos llegan a la plataforma, lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a la plataforma, lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.
translation-type: tm+mt
source-git-commit: c7e8cf31f4c03eec9b24064c6888e09a7070aaa5
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---


# Segmentación por flujo continuo

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la interfaz de usuario. Para obtener información sobre el uso de la segmentación de flujo mediante la API, lea la guía [de la API de segmentación de](../api/streaming-segmentation.md)flujo.

La segmentación por flujo continuo [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real mientras se concentran en la riqueza de los datos. Con la segmentación de flujo continuo, la cualificación de segmentos ahora se produce cuando los datos de flujo llegan a [!DNL Platform]su destino, lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que se pasan los datos [!DNL Platform], lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

>[!NOTE]
>
>La segmentación por flujo continuo solo se puede utilizar para evaluar los datos que se transmiten a la plataforma. En otras palabras, los datos ingestados mediante la ingestión por lotes no se evaluarán mediante la segmentación de flujo continuo y requerirán que se active la evaluación por lotes.

## Tipos de consulta de segmentación por flujo continuo

>[!NOTE]
>
>Para que la segmentación por flujo continuo funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre cómo habilitar la segmentación programada, consulte [la sección de segmentación por flujo en la guía](./overview.md#scheduled-segmentation)de usuario de segmentación.

Una consulta se evaluará automáticamente con segmentación de flujo continuo si cumple cualquiera de los siguientes criterios:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Visita entrante dentro de un período de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante **en los últimos siete días**. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |  |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Visita entrante que hace referencia a un perfil dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o varios atributos de perfil, **en los últimos siete días**. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Varios eventos que hacen referencia a un perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o varios atributos de perfil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

La siguiente sección lista ejemplos de definición de segmentos que **no se habilitarán** para la segmentación de flujo continuo.

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Visita entrante dentro de un período de tiempo relativo | Si la definición del segmento se refiere a un evento entrante **no** dentro del período **de siete días**&#x200B;últimos. Por ejemplo, en las **últimas dos semanas**. | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| Visita entrante que hace referencia a un perfil dentro de una ventana relativa | Las siguientes opciones **no admitirán** la segmentación de flujo continuo:<ul><li>Un evento entrante **no** dentro del **último período** de siete días.</li><li>Definición de segmento que incluye [!DNL Adobe Audience Manager (AAM)] segmentos o características.</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| Varios eventos que hacen referencia a un perfil | Las siguientes opciones **no admitirán** la segmentación de flujo continuo:<ul><li>Un evento que **no** se produce en **las últimas 24 horas**.</li><li>Definición de segmento que incluye segmentos o características de Adobe Audience Manager (AAM).</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| Consultas de varias entidades | Las consultas de varias entidades **no son** compatibles con la segmentación por flujo. |  |

Además, se aplican algunas directrices al realizar la segmentación de flujo:

| Tipo de consulta | Directrices |
| ---------- | -------- |
| Consulta de evento único | La ventana retroactiva está limitada a **siete días**. |
| Consulta con historial de eventos | <ul><li>La ventana retroactiva está limitada a **un día**.</li><li>Entre los eventos **debe** existir una condición estricta de ordenación de tiempo.</li><li>Solo se permiten pedidos de tiempo simples (antes y después) entre los eventos.</li><li>Los eventos individuales **no se pueden** negar. Sin embargo, toda la consulta **puede** ser anulada.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición de segmento cambiará automáticamente de &quot;Streaming&quot; a &quot;Batch&quot;.

## Detalles del segmento de segmentación de flujo continuo

Después de crear un segmento de flujo continuo habilitado, puede realizar vistas de los detalles de dicho segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

En concreto, se muestran detalles sobre el tamaño **** total de audiencia cualificada. El tamaño **** total de audiencias cualificadas muestra el número total de audiencias cualificadas de la última ejecución del trabajo de segmentos completado. Si un trabajo de segmento no se completó en las últimas 24 horas, el número de audiencias se tomará de una estimación en su lugar.

Debajo hay un gráfico de líneas que muestra el número de segmentos que fueron calificados y descalificados en las últimas 24 horas. La lista desplegable se puede ajustar para mostrar las últimas 24 horas, la semana pasada o los últimos 30 días.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Para obtener información adicional sobre la última evaluación de segmentos, seleccione la burbuja de información.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obtener más información sobre las definiciones de segmentos, lea la sección anterior sobre los detalles [de definición de](#segment-details)segmentos.

## Demostración en vídeo de segmentación por flujo continuo

El siguiente vídeo está diseñado para admitir su comprensión de la segmentación de flujo continuo. Muestra un ejemplo de la experiencia del cliente seguido de una visita rápida de las funciones clave de la [!DNL Platform] interfaz.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Pasos siguientes

Esta guía del usuario explica cómo funcionan las definiciones de segmentos con transmisión habilitada en Adobe Experience Platform y cómo supervisar los segmentos con transmisión habilitada.

Para obtener más información sobre el uso de la interfaz de usuario de Adobe Experience Platform, lea la guía [de usuario de](./overview.md)Segmentación.