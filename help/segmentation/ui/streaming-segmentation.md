---
keywords: Experience Platform;inicio;temas populares;segmentación por streaming;Segmentación;Servicio de segmentación;servicio de segmentación;guía de iu;
solution: Experience Platform
title: Guía de IU de segmentación de streaming
description: La segmentación por streaming en Adobe Experience Platform le permite realizar la segmentación en tiempo casi real al tiempo que se centra en la riqueza de datos. Con la segmentación por streaming, la calificación de segmentos ahora se produce cuando los datos llegan a Platform, lo que alivia la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a Platform, lo que significa que la inscripción a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 0%

---

# Segmentación de streaming

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la interfaz de usuario. Para obtener información sobre el uso de la segmentación de streaming mediante la API, lea la [guía de API de segmentación de streaming](../api/streaming-segmentation.md).

Segmentación de streaming en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real al tiempo que se centran en la riqueza de datos. Con la segmentación por streaming, la calificación de segmentos ahora se produce cuando los datos de streaming llegan a [!DNL Platform], aliviando la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a [!DNL Platform], lo que significa que el abono a segmentos se mantendrá actualizado sin ejecutar trabajos de segmentación programados.

>[!NOTE]
>
>La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los datos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión.
>
>Además, los segmentos evaluados con la segmentación de flujo continuo pueden variar entre la pertenencia ideal y real si el segmento se basa en otro segmento que se evalúa mediante la segmentación por lotes. Por ejemplo, si el segmento A se basa en el segmento B y el segmento B se evalúa mediante la segmentación por lotes, ya que el segmento B solo se actualiza cada 24 horas, el segmento A se alejará más de los datos reales hasta que se vuelva a sincronizar con la actualización del segmento B.

## Tipos de consulta de segmentación de streaming {#query-types}

>[!NOTE]
>
>Para que la segmentación de streaming funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre la activación de la segmentación programada, consulte [Consulte la sección segmentación de streaming en la guía del usuario de segmentación](./overview.md#scheduled-segmentation).

Una consulta se evaluará automáticamente con la segmentación de flujo continuo si cumple cualquiera de los siguientes criterios:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Evento único | Cualquier definición de segmento que haga referencia a un único evento entrante sin restricción horaria. | ![Se muestra un ejemplo de un solo evento.](../images/ui/streaming-segmentation/incoming-hit.png) |
| Evento único dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un único evento entrante. | ![Se muestra un ejemplo de un solo evento dentro de una ventana de tiempo relativa.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Evento único con una ventana de tiempo | Cualquier definición de segmento que haga referencia a un único evento entrante con un intervalo de tiempo. | ![Se muestra un ejemplo de un solo evento con una ventana de tiempo.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |  |
| Evento único con un atributo de perfil | Cualquier definición de segmento que haga referencia a un único evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. **Nota:** La consulta se evalúa inmediatamente cuando llega el evento. Sin embargo, en el caso de un evento de perfil, debe esperar 24 horas para incorporarse. | ![Se muestra un ejemplo de un solo evento con un atributo de perfil.](../images/ui/streaming-segmentation/profile-hit.png) |
| Evento único con un atributo de perfil dentro de una ventana de tiempo relativa | Cualquier definición de segmento que haga referencia a un único evento entrante y a uno o más atributos de perfil. | ![Se muestra un ejemplo de un solo evento con un atributo de perfil dentro de una ventana de tiempo relativa.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se utiliza un segmento de segmentos, se producirá la descalificación del perfil **cada 24 horas**. | ![Se muestra un ejemplo de un segmento de segmentos.](../images/ui/streaming-segmentation/two-batches.png) |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o más atributos de perfil. | ![Se muestra un ejemplo de varios eventos con un atributo de perfil.](../images/ui/streaming-segmentation/event-history-success.png) |

Una definición de segmento **no** habilitarse para la segmentación de flujo continuo en los siguientes casos:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager AAM ().
- La definición del segmento incluye varias entidades (consultas de varias entidades).
- La definición del segmento incluye una combinación de un solo evento y una `inSegment` evento.
   - Sin embargo, si el segmento contenido en la variable `inSegment` El evento es solo de perfil, la definición del segmento **testamento** habilitarse para la segmentación de flujo continuo.

Tenga en cuenta las siguientes directrices a la hora de realizar la segmentación por streaming:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva se limita a **un día**.</li><li>Una condición de orden de tiempo estricta **debe** existen entre los eventos.</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición de segmento cambiará automáticamente de &quot;Flujo&quot; a &quot;Lote&quot;.

Además, la descalificación de segmentos, de manera similar a la calificación de segmentos, se produce en tiempo real. Como resultado, si una audiencia ya no cumple los requisitos para un segmento, se elimina inmediatamente. Por ejemplo, si la definición del segmento solicita &quot;Todos los usuarios que compraron zapatos rojos en las últimas tres horas&quot;, después de tres horas, todos los perfiles que inicialmente se calificaron para la definición del segmento serán no calificados.

## Detalles del segmento de segmentación de streaming

Después de crear un segmento habilitado para streaming, puede ver los detalles de ese segmento.

![Se muestra la página de detalles del segmento.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

En concreto, la variable **[!UICONTROL Total cualificado]** Esta métrica se muestra y muestra el número total de audiencias aptas, según las evaluaciones por lotes y de flujo continuo para este segmento.

Debajo hay un gráfico de líneas que muestra la cantidad de nuevas audiencias que se actualizaron en las últimas 24 horas con el método de evaluación de streaming. El menú desplegable se puede ajustar para mostrar las últimas 24 horas, la semana pasada o los últimos 30 días. El **[!UICONTROL Nueva audiencia actualizada]** La métrica de se basa en el cambio en el tamaño de la audiencia durante el intervalo de tiempo seleccionado, evaluado por la segmentación de flujo continuo. Esta métrica no incluye la audiencia cualificada total de la evaluación diaria de lotes de segmentos.

>[!NOTE]
>
>Un segmento se considera cualificado si pasa de no tener estado a realizado o si va de salir a realizado. Un segmento se considera no cualificado si pasa de realizado a existente o de existente a existente.
>
>Puede encontrar más información sobre estos estados en la tabla de estado dentro de la [resumen de segmentación](./overview.md#browse).

![La tarjeta Perfiles a lo largo del tiempo se resalta y muestra un gráfico de líneas de los perfiles a lo largo del tiempo.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Para obtener información adicional acerca de la última evaluación de segmentos, seleccione la burbuja de información junto a **[!UICONTROL Total cualificado]**.

![Se ha seleccionado la burbuja de información para el Total de perfiles cualificados. Muestra información sobre la hora de la última evaluación del segmento.](../images/ui/streaming-segmentation/info-bubble.png)

Para obtener más información sobre las definiciones de segmentos, lea la sección anterior sobre [detalles de definición del segmento](#segment-details).

## Pasos siguientes

En esta guía se explica cómo funcionan las definiciones de segmentos habilitadas para la transmisión en Adobe Experience Platform y cómo monitorizar los segmentos habilitados para la transmisión.

Para obtener más información sobre el uso de la interfaz de usuario de Adobe Experience Platform, lea la [Guía del usuario de segmentación](./overview.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de streaming:

### ¿La &quot;descalificación&quot; de la segmentación de streaming también se produce en tiempo real?

En la mayoría de los casos, la descalificación de la segmentación de streaming se produce en tiempo real. Sin embargo, los segmentos de flujo continuo que utilizan segmentos de segmentos sí lo hacen **no** descalificar en tiempo real, en lugar de descalificar después de 24 horas.

### ¿En qué datos funciona la segmentación por streaming?

La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los segmentos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión. Los eventos transmitidos al sistema con una marca de tiempo de más de 24 horas se procesarán en el trabajo por lotes siguiente.

### ¿Cómo se definen los segmentos como segmentación por lotes o de flujo continuo?

Un segmento se define como segmentación por lotes o de flujo continuo basada en una combinación de tipo de consulta y duración del historial de eventos. Puede encontrar una lista de los segmentos que se evaluarán como segmento de flujo continuo en la [sección tipos de consulta de segmentación de streaming](#query-types).

Tenga en cuenta que si un segmento contiene **ambos** un `inSegment` y una cadena de evento único directa, no cumple los requisitos para la segmentación de flujo continuo. Si desea que este segmento cumpla los requisitos para la segmentación de flujo continuo, debe convertir la cadena de evento único directo en su propio segmento.

### ¿Por qué sigue aumentando el número de segmentos &quot;cualificados totales&quot; mientras que el número de &quot;últimos X días&quot; permanece en cero dentro de la sección de detalles del segmento?

El número total de segmentos cualificados se obtiene del trabajo de segmentación diario, que incluye audiencias que cumplen los requisitos para los segmentos por lotes y de flujo continuo. Este valor se muestra para los segmentos por lotes y de flujo continuo.

El número bajo los &quot;últimos X días&quot; **solamente** incluye audiencias que cumplen los requisitos de la segmentación de streaming y **solamente** aumenta si ha transmitido datos al sistema y estos se contabilizan en esa definición de transmisión. Este valor es **solamente** se muestra para segmentos de flujo continuo. Como resultado, este valor **mayo** mostrar como 0 para los segmentos por lotes.

Como resultado, si ve que el número bajo &quot;Últimos X días&quot; es cero y el gráfico de líneas también informa de cero, tiene **no** transmite al sistema todos los perfiles aptos para ese segmento.

### ¿Cuánto tiempo tarda un segmento en estar disponible?

Un segmento puede tardar hasta una hora en estar disponible.