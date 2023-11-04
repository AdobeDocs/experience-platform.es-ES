---
keywords: Experience Platform;inicio;temas populares;monitorización;monitorización;flujos de datos;monitorización de ingesta;ingesta de datos;ingesta de datos;visualización de registros;visualización de lotes;
solution: Experience Platform
title: Monitorización de la ingesta de datos
description: Esta guía del usuario proporciona información sobre cómo monitorizar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 9399a242b855e151e5822035bc952efa89fe4bf0
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 4%

---

# Monitorización de la ingesta de datos

La ingesta de datos le permite introducir sus datos en Adobe Experience Platform. Puede utilizar la ingesta por lotes, que le permite insertar los datos mediante varios tipos de archivo (como CSV), o la ingesta por secuencias, que le permite introducir los datos en [!DNL Platform] uso de extremos de transmisión en tiempo real.

Esta guía del usuario proporciona pasos sobre cómo monitorizar los datos en la interfaz de usuario de Adobe Experience Platform. Esta guía requiere que tenga un Adobe ID y acceso a Adobe Experience Platform.

## Monitorización de la transmisión de ingesta de datos de extremo a extremo {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="Tasa de ingesta"
>abstract="Número de eventos que se procesan correctamente por segundo."
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html?lang=es" text="Monitorización de flujos de datos para orígenes en la interfaz de usuario"

>[!TIP]
>
>Para calcular el total de eventos en una fecha determinada, utilice la expresión de: `total events / day = ingestion rate * 60 * 60 * 24`.

En el [IU de Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** en el menú de navegación de la izquierda, seguido de **[!UICONTROL Transmisión de extremo a extremo]**.

El **[!UICONTROL Transmisión de extremo a extremo]** página de monitorización. Esta área de trabajo proporciona un gráfico que muestra la velocidad de los eventos transmitidos que recibe [!DNL Platform], un gráfico que muestra la velocidad de los eventos de flujo que procesó correctamente [[!DNL Real-Time Customer Profile]](../../profile/home.md), así como una lista detallada de los datos entrantes.

![](../images/quality/monitor-data-flows/list-streams.png)

De forma predeterminada, el gráfico superior muestra la tasa de ingesta durante los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios periodos de tiempo seleccionando el botón resaltado.

![](../images/quality/monitor-data-flows/events-received.png)

El gráfico inferior muestra la tasa de eventos de flujo procesados correctamente por [!DNL Profile] durante los últimos siete días. Este intervalo de fechas se puede ajustar para mostrar varios periodos de tiempo seleccionando el botón resaltado.

>[!NOTE]
>
>Para que los datos se muestren en este gráfico, deben ser **explícitamente** habilitado para [!DNL Profile]. Para obtener información sobre cómo habilitar la transmisión de datos para [!DNL Profile], lea la [guía del usuario de conjuntos de datos](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Debajo de los gráficos hay una lista de todos los registros de ingesta de transmisión que corresponden con el intervalo de fechas mostrado anteriormente. Cada lote enumerado muestra su ID, el nombre del conjunto de datos, cuándo se actualizó por última vez, el número de registros del lote, así como el número de errores (si existen). Puede seleccionar cualquiera de los registros para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/streams.png)

### Visualización de registros de flujo

Al ver los detalles de un registro transmitido correctamente, se muestra información como el número de registros introducidos, el tamaño del archivo y las horas de inicio y finalización de la ingesta.

![](../images/quality/monitor-data-flows/successful-streaming.png)

Los detalles de un registro de flujo continuo con errores muestran la misma información que un registro correcto.

![](../images/quality/monitor-data-flows/failed-batch.png)

Además, los registros con errores proporcionan detalles sobre los errores que se produjeron al procesar el lote. En el ejemplo siguiente, se produjo un error de análisis al convertir o validar los datos.

>[!NOTE]
>
>Si hay errores en las filas introducidas, estas filas **no** se perderá a menos que el mensaje resultante genere un XDM no válido.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Monitorización de la ingesta de datos de extremo a extremo por lotes

En el [[!DNL Experience Platform UI]](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** en el menú de navegación izquierdo.

El **[!UICONTROL Lote de extremo a extremo]** aparece la página control, que muestra una lista de los lotes introducidos anteriormente. Puede seleccionar cualquiera de los lotes para obtener información más detallada sobre ese registro.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Visualización de lotes

Al ver los detalles de un lote correcto, se muestra información como el número de registros ingeridos, el tamaño del archivo y las horas de inicio y finalización de la ingesta.

![](../images/quality/monitor-data-flows/successful-batch.png)

Los detalles de un lote fallido muestran la misma información que un lote correcto, con la adición del número de registros fallidos.

![](../images/quality/monitor-data-flows/failed-batch.png)

Además, los lotes con errores proporcionan detalles sobre los errores que se han producido al procesar el lote. En el siguiente ejemplo, se ha producido un error con el lote introducido porque tiene el número máximo de identidades para la persona.

>[!NOTE]
>
>Si hay errores en las filas introducidas, estas filas **no** se perderá a menos que el mensaje resultante genere un XDM no válido.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
