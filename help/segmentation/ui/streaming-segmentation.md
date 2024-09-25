---
solution: Experience Platform
title: Guía de IU de segmentación de streaming
description: La segmentación por streaming en Adobe Experience Platform le permite realizar la segmentación en tiempo casi real al tiempo que se centra en la riqueza de datos. Con la segmentación por streaming, la calificación de segmentos ahora se produce cuando los datos llegan a Platform, lo que alivia la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a Platform, lo que significa que la inscripción a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---

# Segmentación de streaming

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la interfaz de usuario. Para obtener información sobre el uso de la segmentación de transmisión por secuencias mediante la API, lea la [guía de la API de segmentación por transmisión](../api/streaming-segmentation.md).

La segmentación de streaming en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real al tiempo que se centran en la riqueza de datos. Con la segmentación por streaming, la calificación de segmentos ahora se produce cuando los datos de streaming llegan a [!DNL Platform], lo que alivia la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a [!DNL Platform], lo que significa que el abono a segmentos se mantendrá actualizado sin ejecutar trabajos de segmentación programados.

>[!NOTE]
>
>La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los datos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión.
>
>Además, los segmentos evaluados con la segmentación de flujo continuo pueden variar entre la pertenencia ideal y real si la definición del segmento se basa en otra definición de segmento que se evalúa mediante la segmentación por lotes. Por ejemplo, si el segmento A se basa en el segmento B y el segmento B se evalúa mediante la segmentación por lotes, ya que el segmento B solo se actualiza cada 24 horas, el segmento A se alejará más de los datos reales hasta que se vuelva a sincronizar con la actualización del segmento B.

## Tipos de consulta de segmentación de streaming {#query-types}

>[!NOTE]
>
>Para que la segmentación de streaming funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre cómo habilitar la segmentación programada, consulte [la descripción general de Audience Portal](./audience-portal.md#scheduled-segmentation).

Una consulta se evaluará automáticamente con la segmentación de flujo continuo si cumple cualquiera de los siguientes criterios:

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Evento único en un intervalo de tiempo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante en un intervalo de tiempo inferior a 24 horas. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Evento único con un atributo de perfil en un intervalo de tiempo relativo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante, con uno o más atributos de perfil, y que se produzca en un intervalo de tiempo relativo inferior a 24 horas. |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se usa un segmento de segmentos, la descalificación del perfil se producirá **cada 24 horas**. |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tenga uno o más atributos de perfil. |

Una definición de segmento **no** se habilitará para la segmentación de flujo continuo en los siguientes casos:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager AAM ().
- La definición del segmento incluye varias entidades (consultas de varias entidades).
- La definición del segmento incluye una combinación de un solo evento y un evento `inSegment`.
   - Sin embargo, si la definición del segmento contenida en el evento `inSegment` es solo de perfil, la definición del segmento **se habilitará** para la segmentación de flujo continuo.
- La definición del segmento utiliza &quot;Ignorar año&quot; como parte de sus restricciones de tiempo.

Tenga en cuenta las siguientes directrices a la hora de realizar la segmentación por streaming:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva está limitada a **un día**.</li><li>Debe **existir una condición de orden de tiempo estricta entre los eventos.**</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición de segmento cambiará automáticamente de &quot;Flujo&quot; a &quot;Lote&quot;.

Además, la descalificación de segmentos, de manera similar a la calificación de segmentos, se produce en tiempo real. Como resultado, si una audiencia ya no cumple los requisitos para un segmento, se elimina inmediatamente. Por ejemplo, si la definición del segmento solicita &quot;Todos los usuarios que compraron zapatos rojos en las últimas tres horas&quot;, después de tres horas, todos los perfiles que inicialmente se calificaron para la definición del segmento serán no calificados.

## Detalles de definición del segmento de segmentación de streaming

Después de crear un segmento habilitado para streaming, puede ver los detalles de ese segmento.

![Se muestra la página de detalles de la definición del segmento.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

En concreto, se muestra la métrica **[!UICONTROL Total cualificado]**, que muestra la cantidad total de audiencias cualificadas, según las evaluaciones por lotes y de flujo continuo de este segmento.

Debajo hay un gráfico de líneas que muestra la cantidad de nuevas audiencias que se actualizaron en las últimas 24 horas con el método de evaluación de streaming. El menú desplegable se puede ajustar para mostrar las últimas 24 horas, la semana pasada o los últimos 30 días. La métrica **[!UICONTROL Nueva audiencia actualizada]** se basa en el cambio en el tamaño de la audiencia durante el intervalo de tiempo seleccionado, evaluado por la segmentación de flujo continuo. Esta métrica no incluye la audiencia cualificada total de la evaluación diaria de lotes de segmentos.

>[!NOTE]
>
>Una definición de segmento se considera cualificada si pasa de no tener estado a realizada o si pasa de existir a realizada. Una definición de segmento se considera no cualificada si pasa de realizada a saliente.
>
>Encontrará más información sobre estos estados en la tabla de estados de la [descripción general de Audience Portal](./audience-portal.md#customize).

![Se resalta la tarjeta Perfiles a lo largo del tiempo, que muestra un gráfico de líneas de los perfiles a lo largo del tiempo.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Encontrará información adicional sobre la última evaluación de segmentos seleccionando la burbuja de información junto a **[!UICONTROL Total cualificado]**.

![Se ha seleccionado la burbuja de información para el total de perfiles cualificados. Muestra información sobre la última hora de evaluación del segmento.](../images/ui/streaming-segmentation/info-bubble.png)

Para obtener más información acerca de las definiciones de segmentos, lea la sección anterior sobre [detalles de definición de segmentos](#segment-details).

## Pasos siguientes

En esta guía se explica cómo funcionan las definiciones de segmentos habilitadas para la transmisión en Adobe Experience Platform y cómo monitorizar los segmentos habilitados para la transmisión.

Para obtener más información acerca del uso de la interfaz de usuario de Adobe Experience Platform, lea la [Guía del usuario de segmentación](./overview.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de streaming:

### ¿La &quot;descalificación&quot; de la segmentación de streaming también se produce en tiempo real?

En la mayoría de los casos, la descalificación de la segmentación de streaming se produce en tiempo real. Sin embargo, los segmentos de streaming que usan segmentos de segmentos **no** descalifican en tiempo real, en lugar de descalificar después de 24 horas.

### ¿En qué datos funciona la segmentación por streaming?

La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los segmentos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión. Los eventos transmitidos al sistema con una marca de tiempo de más de 24 horas se procesarán en el trabajo por lotes siguiente.

### ¿Cómo se definen los segmentos como segmentación por lotes o de flujo continuo?

Una definición de segmento se define como segmentación por lotes, por secuencias o perimetral basada en una combinación de tipo de consulta y duración del historial de eventos. Se puede encontrar una lista de los segmentos que se evaluarán como una definición de segmento de flujo continuo en la [sección de tipos de consulta de segmentación de flujo continuo](#query-types).

Tenga en cuenta que si una definición de segmento contiene **both** una expresión `inSegment` y una cadena de evento único directa, no puede calificar para la segmentación de flujo continuo. Si desea que esta definición de segmento cumpla los requisitos de la segmentación de flujo continuo, debe convertir la cadena de evento único directo en su propio segmento.

### ¿Por qué sigue aumentando el número de segmentos &quot;cualificados totales&quot; mientras que el número de &quot;últimos X días&quot; permanece en cero dentro de la sección de detalles de definición del segmento?

El número total de segmentos cualificados se obtiene del trabajo de segmentación diario, que incluye audiencias que cumplen los requisitos para los segmentos por lotes y de flujo continuo. Este valor se muestra para los segmentos por lotes y de flujo continuo.

El número bajo los &quot;últimos X días&quot; **solo** incluye audiencias que se califican en la segmentación por transmisión y **solo** aumenta si ha transmitido datos al sistema y cuenta para esa definición de transmisión. Este valor se muestra **solamente** para los segmentos de streaming. Como resultado, este valor **may** se muestra como 0 para los segmentos por lotes.

Como resultado, si ve que el número bajo &quot;Últimos X días&quot; es cero y el gráfico de líneas también informa cero, tiene **no** transmitido ningún perfil al sistema que calificaría para ese segmento.

### ¿Cuánto tiempo tarda una definición de segmento en estar disponible?

Una definición de segmento tarda hasta una hora en estar disponible.

### ¿Existen limitaciones a los datos que se transmiten en?

Para que los datos transmitidos se usen en la segmentación de flujo continuo, **debe** haber un espacio entre los eventos transmitidos. Si se transmiten demasiados eventos en el mismo segundo, Platform los tratará como datos generados por bots y se descartarán. Como práctica recomendada, debe tener **al menos** cinco segundos entre los datos de evento para asegurarse de que los datos se utilizan correctamente.
