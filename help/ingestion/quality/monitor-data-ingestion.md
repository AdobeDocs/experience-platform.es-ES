---
keywords: Experience Platform;home;popular topics;monitoring;monitor;data flows;monitor ingestion;data ingestion;Data ingestion;view records;view batches;
solution: Experience Platform
title: Monitoreo de la ingesta de datos
topic: overview
description: Esta guía del usuario proporciona un paso sobre cómo supervisar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cfdaf72b7f4bf190877006ccd4cc6a7fd014adc2
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Monitoreo de la ingesta de datos

La ingestión de datos le permite ingerir sus datos en Adobe Experience Platform. Puede utilizar la ingestión por lotes, que le permite insertar los datos mediante varios tipos de archivo (como CSV), o la ingestión por flujo continuo, que le permite ingerir los datos para [!DNL Platform] utilizar puntos finales de flujo en tiempo real.

Esta guía del usuario proporciona un paso sobre cómo supervisar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.

## Monitoreo de la transmisión de datos end-to-end

En la interfaz de usuario [del](https://platform.adobe.com)Experience Platform, haga clic en **[!UICONTROL Monitoreo]** en el menú de navegación de la izquierda y, a continuación, haga clic en **[!UICONTROL Transmisión de extremo a extremo]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Aparece la página de supervisión **[!UICONTROL de flujo completo]** . Este espacio de trabajo proporciona un gráfico que muestra la velocidad de eventos transmitidos que recibe [!DNL Platform], un gráfico que muestra la velocidad de eventos transmitidos que se procesaron correctamente por [[!DNL Real-time Customer Profile]](../../profile/home.md), así como una lista detallada de los datos entrantes.

![](../images/quality/monitor-data-flows/list-streams.png)

De forma predeterminada, el gráfico superior muestra la tasa de ingestión durante los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios períodos de tiempo haciendo clic en el botón resaltado.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

El gráfico inferior muestra la tasa de eventos de flujo procesados correctamente en [!DNL Profile] los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios períodos de tiempo haciendo clic en el botón resaltado.

>[!NOTE]
>
>Para que los datos se muestren en este gráfico, los datos deben habilitarse **explícitamente** para [!DNL Profile]. Para aprender a habilitar la transmisión de datos para [!DNL Profile], lea la guía [del usuario de](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)conjuntos de datos.

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Debajo de los gráficos hay una lista de todos los registros de ingestión de flujo que corresponden al intervalo de fechas mostrado arriba. Cada lote de la lista muestra su ID, el nombre del conjunto de datos, cuándo se actualizó por última vez, el número de registros en el lote, así como el número de errores (si existe). Puede hacer clic en cualquiera de los registros para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Visualización de registros de flujo continuo

Al ver los detalles de un registro transmitido correctamente, se muestra información como el número de registros ingestados, el tamaño del archivo, el inicio de ingestión y las horas de finalización.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Los detalles de un registro de flujo fallido muestran la misma información que un registro exitoso.

![](../images/quality/monitor-data-flows/failed-batch.png)

Además, los registros con errores proporcionan detalles sobre los errores que se produjeron durante el procesamiento del lote. En el ejemplo siguiente, se produjo un error del sistema al validar el datasetId del catálogo.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Monitorear la ingesta de datos de extremo a extremo por lotes

En el [[!DNL Experience Platform UI]](https://platform.adobe.com), haga clic en **[!UICONTROL Monitoreo]** en el menú de navegación de la izquierda.

![](../images/quality/monitor-data-flows/click-monitoring.png)

Se abre la página de supervisión **[!UICONTROL por lotes de extremo a extremo]** , que muestra una lista de los lotes previamente ingestados. Puede hacer clic en cualquiera de los lotes para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/list-batches.png)

### Visualización de lotes

Al ver los detalles de un lote exitoso, se muestra información como el número de registros ingestados, el tamaño del archivo, el inicio de ingestión y las horas de finalización.

![](../images/quality/monitor-data-flows/successful-batch.png)

Los detalles de un lote dañado muestran la misma información que un lote exitoso, con la adición del número de registros fallidos.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Además, los lotes con errores proporcionan detalles sobre los errores que se produjeron durante el procesamiento del lote. En el ejemplo siguiente, se produjo un error con el lote ingestado porque se utilizó un campo desconocido de `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)