---
keywords: Experience Platform;inicio;temas populares;monitorización;monitorización;flujos de datos;monitorizar consumo;consumo de datos;ingesta de datos;ver registros;ver lotes;
solution: Experience Platform
title: Supervisión de la ingesta de datos
topic-legacy: overview
description: En esta guía del usuario se proporcionan pasos sobre cómo monitorizar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Monitorización de la ingesta de datos

La ingesta de datos le permite introducir sus datos en Adobe Experience Platform. Puede utilizar la ingesta por lotes, que le permite insertar sus datos mediante varios tipos de archivo (como CSV), o la ingesta de flujo, que le permite introducir sus datos en [!DNL Platform] mediante el uso de extremos de flujo en tiempo real.

En esta guía del usuario se proporcionan pasos sobre cómo monitorizar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.

## Monitorización de la transmisión de datos de extremo a extremo

En la [IU del Experience Platform](https://platform.adobe.com), haga clic en **[!UICONTROL Monitoring]** en el menú de navegación de la izquierda y, a continuación, haga clic en **[!UICONTROL Streaming end-to-end]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Aparece la página de monitorización **[!UICONTROL Streaming end-to-end]**. Este espacio de trabajo proporciona un gráfico que muestra la tasa de recepción de eventos transmitidos por [!DNL Platform], un gráfico que muestra la tasa de eventos transmitidos que [[!DNL Real-time Customer Profile]](../../profile/home.md) procesaron correctamente, así como una lista detallada de datos entrantes.

![](../images/quality/monitor-data-flows/list-streams.png)

De forma predeterminada, el gráfico superior muestra la tasa de ingesta durante los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios períodos de tiempo haciendo clic en el botón resaltado.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

El gráfico inferior muestra la tasa de eventos de flujo procesados correctamente en [!DNL Profile] durante los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios períodos de tiempo haciendo clic en el botón resaltado.

>[!NOTE]
>
>Para que los datos aparezcan en este gráfico, los datos deben estar **explícitamente** habilitados para [!DNL Profile]. Para aprender a habilitar la transmisión de datos para [!DNL Profile], lea la [guía del usuario de conjuntos de datos](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Debajo de los gráficos hay una lista de todos los registros de ingesta de transmisión que se corresponden con el intervalo de fechas mostrado arriba. Cada lote enumerado muestra su ID, nombre del conjunto de datos, la última vez que se actualizó, el número de registros en el lote, así como el número de errores (si existe). Puede hacer clic en cualquiera de los registros para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Visualización de registros de flujo continuo

Al ver los detalles de un registro transmitido correctamente, se muestra información como el número de registros ingeridos, el tamaño del archivo y las horas de inicio y finalización de ingesta.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Los detalles de un registro de flujo continuo con errores muestran la misma información que un registro con éxito.

![](../images/quality/monitor-data-flows/failed-batch.png)

Además, los registros fallidos proporcionan detalles sobre los errores que se produjeron al procesar el lote. En el siguiente ejemplo, se produjo un error del sistema al validar el conjunto de datos del catálogo.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Monitorización de la ingesta de datos de extremo a extremo por lotes

En [[!DNL Experience Platform UI]](https://platform.adobe.com), haga clic en **[!UICONTROL Monitoring]** en el menú de navegación de la izquierda.

![](../images/quality/monitor-data-flows/click-monitoring.png)

Aparece la página de monitorización **[!UICONTROL Batch end-to-end]**, que muestra una lista de los lotes ingestados anteriormente. Puede hacer clic en cualquiera de los lotes para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/list-batches.png)

### Visualización de lotes

Al ver los detalles de un lote exitoso, se muestra información como el número de registros ingeridos, el tamaño del archivo y las horas de inicio y finalización de ingesta.

![](../images/quality/monitor-data-flows/successful-batch.png)

Los detalles de un lote con errores muestran la misma información que un lote con éxito, con la adición del número de registros con errores.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Además, los lotes con errores proporcionan detalles sobre los errores que se produjeron al procesar el lote. En el ejemplo siguiente, se produjo un error con el lote ingerido porque utilizaba un campo desconocido de `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)
