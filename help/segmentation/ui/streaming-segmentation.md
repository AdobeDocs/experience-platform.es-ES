---
keywords: Experience Platform;inicio;temas populares;segmentación de flujo;Segmentación;Servicio de segmentación;servicio de segmentación;guía de ui;
solution: Experience Platform
title: Guía de la IU de segmentación por flujo continuo
topic: ui guide
description: La segmentación por flujo continuo en Adobe Experience Platform le permite realizar la segmentación en tiempo casi real mientras se centra en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos llegan a la plataforma, lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a la plataforma, lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.
translation-type: tm+mt
source-git-commit: c0c42f872666323bfb3bdbdf5fb02475d3b5bc79
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---


# Segmentación por flujo continuo

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la interfaz de usuario. Para obtener información sobre el uso de la segmentación de flujo mediante la API, lea la [guía de la API de segmentación de flujo](../api/streaming-segmentation.md).

La segmentación por flujo continuo en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real mientras se concentran en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos de flujo llegan a [!DNL Platform], lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a [!DNL Platform], lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

>[!NOTE]
>
>La segmentación por flujo continuo solo se puede utilizar para evaluar los datos que se transmiten a la plataforma. En otras palabras, los datos ingestados mediante la ingestión por lotes no se evaluarán mediante la segmentación por flujo continuo y se evaluarán junto con el trabajo de segmento programado por la noche.
>
>Además, los segmentos evaluados con la segmentación de flujo pueden variar entre la pertenencia ideal y la real si el segmento se basa en otro segmento que se evalúa mediante la segmentación por lotes. Por ejemplo: si el segmento A se basa en el segmento B y el segmento B se evalúa mediante la segmentación por lotes, ya que el segmento B solo se actualiza cada 24 horas, el segmento A se alejará aún más de los datos reales hasta que se vuelva a sincronizar con la actualización del segmento B.

## Tipos de consulta de segmentación por flujo continuo

>[!NOTE]
>
>Para que la segmentación por flujo continuo funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre cómo habilitar la segmentación programada, consulte [la sección de segmentación por flujo en la guía del usuario de segmentación](./overview.md#scheduled-segmentation).

Una consulta se evaluará automáticamente con segmentación de flujo continuo si cumple cualquiera de los siguientes criterios:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Visita entrante dentro de un período de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |  |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Visita entrante que hace referencia a un perfil dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o varios atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Varios eventos que hacen referencia a un perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o más atributos de perfil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Una definición de segmento **no** se habilitará para la segmentación de flujo continuo en los siguientes escenarios:

- La definición del segmento incluye segmentos o características de Adobe Audience Manager (AAM).
- La definición de segmento incluye varias entidades (consultas de varias entidades).

Además, se aplican algunas directrices al realizar la segmentación de flujo:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites para la ventana retroactiva. |
| Consulta con historial de eventos | <ul><li>La ventana retroactiva está limitada a **un día**.</li><li>Debe existir una condición estricta de ordenación de tiempo **entre los eventos.**</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición de segmento cambiará automáticamente de &quot;Streaming&quot; a &quot;Batch&quot;.

## Detalles del segmento de segmentación de flujo continuo

Después de crear un segmento de flujo continuo habilitado, puede realizar vistas de los detalles de dicho segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Específicamente, se muestran detalles sobre el **[!UICONTROL tamaño total de audiencia cualificada]**. El **[!UICONTROL tamaño total de audiencia cualificada]** muestra el número total de audiencias calificadas de la última ejecución del trabajo de segmento completado. Si un trabajo de segmento no se completó en las últimas 24 horas, el número de audiencias se tomará de una estimación en su lugar.

Debajo hay un gráfico de líneas que muestra el número de segmentos que fueron calificados y descalificados en las últimas 24 horas. La lista desplegable se puede ajustar para mostrar las últimas 24 horas, la semana pasada o los últimos 30 días.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Para obtener información adicional sobre la última evaluación de segmentos, seleccione la burbuja de información.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obtener más información sobre las definiciones de segmentos, lea la sección anterior sobre [detalles de definición de segmentos](#segment-details).

## Demostración en vídeo de segmentación por flujo continuo

El siguiente vídeo está diseñado para admitir su comprensión de la segmentación de flujo continuo. Muestra un ejemplo de la experiencia del cliente seguido de una visita rápida de las funciones clave en la interfaz [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Pasos siguientes

Esta guía del usuario explica cómo funcionan las definiciones de segmentos con transmisión habilitada en Adobe Experience Platform y cómo supervisar los segmentos con transmisión habilitada.

Para obtener más información sobre el uso de la interfaz de usuario de Adobe Experience Platform, lea la [Guía del usuario de segmentación](./overview.md).