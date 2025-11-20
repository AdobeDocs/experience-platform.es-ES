---
description: Aprenda a utilizar el tablero de monitorización para monitorizar los datos introducidos en el lago de datos.
title: Monitorización de ingesta de lago de datos
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 75970d41a316c97d98ebf6cefd3bfa0e58173030
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 10%

---

# Monitorización de ingesta de lago de datos

>[!IMPORTANT]
>
>El tablero de monitorización no admite actualmente fuentes de streaming, como la [fuente de API HTTP](../../sources/connectors/streaming/http.md). En este momento, solo puede utilizar el panel para monitorizar los orígenes de lotes.

Puede utilizar el panel de monitorización de la interfaz de usuario de Adobe Experience Platform para recuperar métricas sobre los procesos de ingesta y retención de datos en el lago de datos. Utilice los gráficos de la interfaz para monitorizar las tendencias de ingesta y retención a lo largo del tiempo y resumir el rendimiento de todos los flujos de datos de origen.

Lea este documento para aprender cómo puede utilizar el panel de monitorización para monitorizar todo el procesamiento de datos en el lago de datos, incluidas tanto la ingesta como la retención.

## Introducción {#get-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Experience Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   * [Ejecuciones](../../sources/notifications.md) de flujo de datos: Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración Frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../sources/home.md): Experience Platform permite que se ingieran datos de varias fuentes al tiempo que le brinda la capacidad de estructurar, etiquetar y mejorar los datos entrantes utilizando Experience Platform servicios.
* [Servicio](../../identity-service/home.md) de identidad: Obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.
* [Zonas protegidas](../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Uso del panel de control de monitorización para la ingesta del lago de datos

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Ingesta de origen"
>abstract="La vista Ingesta de origen contiene información sobre el estado de la actividad de datos y las métricas del servicio de lago de datos, incluidos los registros ingeridos y los registros con errores. Consulte la guía de definición de métricas para obtener más información sobre métricas y gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Detalles de ejecución del flujo de datos"
>abstract="El procesamiento de fuentes contiene información sobre el estado de la actividad de datos y las métricas del servicio de lago de datos, incluidos los registros ingeridos y los registros con errores. Consulte la guía de definición de métricas para obtener más información sobre métricas y gráficos."
>text="Learn more in documentation"

Seleccione **[!UICONTROL Data lake]** en el encabezado principal del panel de monitorización para ver la tasa de ingesta del lago de datos.

![Panel de supervisión con la tarjeta de orígenes seleccionada.](../assets/ui/monitor-sources/data-lake.png)

El gráfico [!UICONTROL Ingestion rate] muestra la tasa de ingesta de datos en función del lapso de tiempo configurado. De forma predeterminada, el panel de monitorización muestra las tasas de ingesta de las últimas 24 horas. Para ver los pasos sobre cómo configurar el lapso de tiempo, lea la guía sobre [configuración del lapso de tiempo de supervisión](monitor.md#configure-monitoring-time-frame).

El gráfico se muestra de forma predeterminada. Para ocultar el gráfico, seleccione **[!UICONTROL Metrics and graphs]** para deshabilitar la opción y ocultar el gráfico.

![Gráfico de métricas de tasa de ingesta.](../assets/ui/monitor-sources/metrics-graph.png)

La parte inferior del panel muestra una tabla que describe el informe de métricas actuales para todos los flujos de datos de origen existentes.

![La tabla de métricas del tablero de monitoreo.](../assets/ui/monitor-sources/metrics-table.png)

| Métricas | Descripción |
| --- | --- |
| Registros recibidos | El número total de registros recibidos de una fuente determinada. |
| Registros ingeridos | Número total de registros ingeridos en el lago de datos. |
| Registros eliminados | Número total de registros eliminados debido a la configuración de retención del lago de datos o a cambios en las operaciones de captura de datos. |
| Registros omitidos | El número total de registros omitidos. Un registro omitido hace referencia a los campos que se omitieron porque no eran necesarios para la ingesta. Por ejemplo, si crea un flujo de datos de origen con la ingesta parcial habilitada, puede configurar una tasa de error aceptable umbral. Durante el proceso de ingesta, la ingesta omitirá los registros de campos que no son obligatorios, como los campos de identidad, siempre que estén dentro del umbral de error. |
| Error de registros | El número total de registros que no se pudieron ingerir debido a errores. |
| Tasa de ingesta | El porcentaje de registros que se ingirieron en función del número total de registros recibidos. |
| Total de flujos de datos fallidos | Número total de flujos de datos que han fallado. |

{style="table-layout:auto"}

Puede filtrar aún más los datos mediante las opciones proporcionadas sobre la tabla de métricas:

| Filtrado de opciones | Descripción |
| --- | --- |
| Buscar | Utilice la barra de búsqueda para filtrar la vista a un solo tipo de origen. |
| Fuentes | Seleccione **[!UICONTROL Sources]** para filtrar la vista y mostrar los datos de métricas por tipo de origen. Esta es la visualización predeterminada que utiliza el panel de monitorización. |
| Flujos de datos | Seleccione **[!UICONTROL Dataflows]** esta opción para filtrar vista y mostrar Métrica datos por flujo de datos. |
| Mostrar solo errores | Seleccione esta opción **[!UICONTROL Show failures only]** para filtrar los vista y mostrar únicamente los flujos de datos que informaron errores de ingesta. |
| Mis fuentes | Puede filtrar aún más la vista mediante el menú desplegable [!UICONTROL My sources]. Utilice el menú desplegable para filtrar la vista por categoría. Como alternativa, puede seleccionar **[!UICONTROL All sources]** para mostrar las métricas de todos los orígenes o seleccionar **[!UICONTROL My sources]** para mostrar únicamente los orígenes con los que tiene una cuenta correspondiente. |

{style="table-layout:auto"}

Para personalizar la visualización de la columna, seleccione el icono de configuración de columna ![column-icon](/help/images/icons/column-settings.png).

![Panel de supervisión con el icono de configuración de columna seleccionado.](../assets/ui/monitor-sources/edit-columns.png)

A continuación, utilice la ventana *[!UICONTROL Customize table]* para seleccionar las columnas que desea que muestre el panel. Cuando termine, seleccione **[!UICONTROL Apply]**.

![Ventana emergente de columna personalizada en el panel de supervisión.](../assets/ui/monitor-sources/customize-table.png)

Para monitorizar los datos que se están ingiriendo en un flujo de datos específico, seleccione el icono de filtro ![filter](/help/images/icons/filter-add.png) junto a un origen.

>[!TIP]
>
>Puede utilizar el tablero de monitorización para monitorizar las métricas de eliminación de datos de los registros eliminados mediante políticas de retención de datos. Para obtener más información sobre la retención de datos, lea la guía sobre [configuración de políticas de retención de datos](../../catalog/datasets/user-guide.md#data-retention-policy).

![Controle un flujo de datos específico seleccionando el icono de filtro junto a una fuente determinada.](../assets/ui/monitor-sources/monitor-dataflow.png)

La tabla de métricas se actualiza a una tabla de flujos de datos activos que corresponden al origen seleccionado. Durante este paso, puede vista información adicional sobre sus flujos de datos, incluidos sus conjunto de datos y tipo de datos correspondientes, así como una marca de tiempo para indicar cuándo estuvieron activos por última vez.

Para seguir inspeccionando un flujo de datos, seleccione el filtro del icono ![de filtro](/help/images/icons/filter-add.png) junto al flujo de datos.

![La tabla de flujos de datos en el panel de supervisión.](../assets/ui/monitor-sources/select-dataflow.png)

A continuación, se le dirigirá a una interfaz que enumera todas las iteraciones de ejecución de flujo de datos del flujo de datos seleccionado.

Las ejecuciones de flujo de datos representan una instancia de ejecución de flujo de datos. Por ejemplo, si un flujo de datos está programado para ejecutarse cada hora a las 9:00, las 10:00 y las 11:00 a.m., entonces tendrá tres instancias de ejecución de flujo. Las ejecuciones de flujo son específicas de su organización particular.

Para inspeccionar métricas de una iteración de ejecución de flujo de datos específica, seleccione el filtro de icono ![de filtro](/help/images/icons/filter-add.png) junto a su flujo de datos.

![El flujo de datos se ejecuta Métrica Página.](../assets/ui/monitor-sources/dataflow-page.png)

Utilice el Página de detalles de ejecución del flujo de datos para vista métricas e información de la iteración de ejecución seleccionada.

![Los detalles de ejecución del flujo de datos Página.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Detalles de ejecución del flujo de datos | Descripción |
| --- | --- |
| Registros ingeridos | El número total de registros que se ingirieron desde la ejecución del flujo de datos. |
| Error de registros | Número total de registros que no se ingirieron debido a errores en la ejecución del flujo de datos. |
| Total de archivos | Número total de archivos en la ejecución del flujo de datos. |
| Tamaño de los datos | El tamaño total de los datos contenidos en la ejecución del flujo de datos. |
| ID de ejecución de flujo de datos | El ID de la iteración de ejecución del flujo de datos. |
| ID de la organización | El ID de la organización en la que se ejecutó el flujo de datos. |
| Estado | El estado de ejecución del flujo de datos. |
| Inicio de ejecución de flujo de datos | Una marca de tiempo que indica cuándo se inició la ejecución del flujo de datos. |
| Fin de ejecución de flujo de datos | Una marca de tiempo que indica cuándo terminó la ejecución del flujo de datos. |
| Conjunto de datos | Conjunto de datos utilizado para crear el flujo de datos. |
| Tipo de datos | El tipo de datos que se encontraban en el flujo de datos. |
| Ingesta parcial | La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos exactos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos. Puede habilitar la ingesta parcial durante el proceso de creación del flujo de datos. |
| Diagnósticos de error | Error diagnostics indica a la fuente que produzca diagnósticos de error a los que puede hacer referencia posteriormente al monitorizar la actividad del conjunto de datos y el estado del flujo de datos. Puede habilitar el diagnóstico de errores durante el proceso de creación del flujo de datos. |
| Resumen de errores | Ante una ejecución fallida del flujo de datos, el resumen del error muestra un código y una descripción de error para resumir por qué ha fallado la iteración de ejecución. |

{style="table-layout:auto"}

Si el flujo de datos ejecuta informes de errores, puede desplazarse hacia abajo hasta la parte inferior de la página utilizando la interfaz [!UICONTROL Dataflow run errors].

Utilice la sección [!UICONTROL Records failed] para ver las métricas de los registros que no se ingirieron debido a errores. Para ver un informe de error completo, seleccione **[!UICONTROL Preview error diagnostics]**. Para descargar una copia de los diagnósticos de error y del manifiesto de archivo, seleccione **[!UICONTROL Download]** y, a continuación, copie la llamada de API de ejemplo que se utilizará con la API [!DNL Data Access].

>[!NOTE]
>
>Solo puede utilizar diagnósticos de errores si la función se habilitó durante el proceso de creación de la conexión de origen.

## Próximos pasos {#next-steps}

Al seguir este tutorial, aprendió a monitor la tasa de ingestión del lago de datos utilizando el **[!UICONTROL Monitoring]** panel. También ha aprendido a identificar errores que causan errores de flujo de datos durante la ingesta. Consulte los siguientes documentos para obtener más detalles:

* [Supervisión de datos](./monitor-identities.md) de identidad.
* [Supervisar datos de perfil](./monitor-profiles.md).
