---
keywords: Experience Platform;inicio;temas populares;monitorización;monitorización;flujos de datos;monitorizar consumo;consumo de datos;ingesta de datos;ver registros;ver lotes;
solution: Experience Platform
title: Monitorización de la ingesta de datos
topic-legacy: overview
description: En esta guía del usuario se proporcionan pasos sobre cómo monitorizar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: dce7faa7fc680e37b537bf623c3a33e6c6e37169
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Monitorización de la ingesta de datos

La ingesta de datos le permite introducir sus datos en Adobe Experience Platform. Puede utilizar la ingesta por lotes, que le permite insertar sus datos mediante varios tipos de archivo (como CSV), o la ingesta por transmisión, que le permite introducir sus datos en [!DNL Platform] uso de extremos de flujo continuo en tiempo real.

Esta guía del usuario proporciona pasos sobre cómo monitorizar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.

## Monitorización de la transmisión de datos de extremo a extremo {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="Tasa de ingesta"
>abstract="Número de eventos que se procesan correctamente por segundo."
>text="Learn more in the documentation"
>additional-url="http://www.adobe.com/go/monitor-dataflows-en" text="Monitorización de flujos de datos para orígenes en la interfaz de usuario"

>[!TIP]
>
>Para calcular los eventos totales en una fecha determinada, utilice la expresión de: `total events / day = ingestion rate * 60 * 60 * 24`.

En el [IU de Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** en el menú de navegación de la izquierda, seguido de **[!UICONTROL Transmisión de extremo a extremo]**.

La variable **[!UICONTROL Transmisión de extremo a extremo]** página de monitorización. Este espacio de trabajo proporciona un gráfico que muestra la tasa de eventos de flujo continuo que recibe [!DNL Platform], un gráfico que muestra la tasa de eventos de flujo continuo que procesaron correctamente [[!DNL Real-time Customer Profile]](../../profile/home.md), así como una lista detallada de los datos entrantes.

![](../images/quality/monitor-data-flows/list-streams.png)

De forma predeterminada, el gráfico superior muestra la tasa de ingesta durante los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios períodos de tiempo seleccionando el botón resaltado.

![](../images/quality/monitor-data-flows/events-received.png)

El gráfico inferior muestra la tasa de eventos de flujo procesados correctamente por [!DNL Profile] en los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios períodos de tiempo seleccionando el botón resaltado.

>[!NOTE]
>
>Para que los datos aparezcan en este gráfico, los datos deben **explícitamente** habilitado para [!DNL Profile]. Para aprender a habilitar la transmisión de datos para [!DNL Profile], lea la [guía del usuario de conjuntos de datos](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Debajo de los gráficos hay una lista de todos los registros de ingesta de transmisión que se corresponden con el intervalo de fechas mostrado arriba. Cada lote enumerado muestra su ID, nombre del conjunto de datos, la última vez que se actualizó, el número de registros en el lote, así como el número de errores (si existe). Puede seleccionar cualquiera de los registros para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/streams.png)

### Visualización de registros de flujo continuo

Al ver los detalles de un registro transmitido correctamente, se muestra información como el número de registros ingeridos, el tamaño del archivo y las horas de inicio y finalización de ingesta.

![](../images/quality/monitor-data-flows/successful-streaming.png)

Los detalles de un registro de flujo continuo con errores muestran la misma información que un registro con éxito.

![](../images/quality/monitor-data-flows/failed-batch.png)

Además, los registros fallidos proporcionan detalles sobre los errores que se produjeron al procesar el lote. En el siguiente ejemplo, se produjo un error de análisis al convertir o validar los datos.

>[!NOTE]
>
>Si hay errores en las filas incorporadas, estas filas **not** se debe eliminar a menos que el mensaje resultante dé como resultado un XDM no válido.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Monitorización de la ingesta de datos de extremo a extremo por lotes

En el [[!DNL Experience Platform UI]](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** en el menú de navegación de la izquierda.

La variable **[!UICONTROL Lote de extremo a extremo]** página de monitorización, que muestra una lista de los lotes ingestados anteriormente. Puede seleccionar cualquiera de los lotes para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Visualización de lotes

Al ver los detalles de un lote exitoso, se muestra información como el número de registros ingeridos, el tamaño del archivo y las horas de inicio y finalización de ingesta.

![](../images/quality/monitor-data-flows/successful-batch.png)

Los detalles de un lote con errores muestran la misma información que un lote con éxito, con la adición del número de registros con errores.

![](../images/quality/monitor-data-flows/failed-batch.png)

Además, los lotes con errores proporcionan detalles sobre los errores que se produjeron al procesar el lote. En el ejemplo siguiente, se produjo un error con el lote ingerido porque tiene el número máximo de identidades para la persona.

>[!NOTE]
>
>Si hay errores en las filas incorporadas, estas filas **not** se debe eliminar a menos que el mensaje resultante dé como resultado un XDM no válido.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
