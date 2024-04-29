---
description: Aprenda a utilizar el tablero de monitorización para monitorizar los datos introducidos desde las fuentes.
title: Monitorización de flujos de datos para fuentes en la IU
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 51f8a8c77518a0b2e9e4b914c891f97433db1ef2
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 8%

---

# Monitorización de flujos de datos para orígenes en la interfaz de usuario

>[!IMPORTANT]
>
>Fuentes de flujo, como la [Fuente de API HTTP](../../sources/connectors/streaming/http.md) no son compatibles actualmente con el tablero de monitorización. En este momento, solo puede utilizar el panel para monitorizar los orígenes de lotes.

Lea este documento para aprender a utilizar el panel de monitorización para monitorizar los flujos de datos de origen en la interfaz de usuario de Experience Platform.

## Introducción  {#get-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   * [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../sources/home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Servicio de identidad](../../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento uniendo identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Monitorización de los datos de origen mediante el panel de monitorización

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

<!-- In the [Platform UI](https://platform.adobe.com), select **[!UICONTROL Monitoring]** from the left navigation to access the [!UICONTROL Monitoring] dashboard. The [!UICONTROL Monitoring] dashboard contains metrics and information on all sources dataflows, including insights into the health of data traffic from a source to [!DNL Identity Service], and to [!DNL Profile].

At the center of the dashboard is the [!UICONTROL Source ingestion] panel, which contains metrics and graphs that display data on records ingested and records failed. -->

En el panel de monitorización, seleccione [!UICONTROL Fuentes] en el encabezado principal para actualizar el panel con una visualización de las fuentes de la tasa de ingesta de flujo de datos.

![Panel de monitorización con la tarjeta de fuentes seleccionada.](../assets/ui/monitor-sources/sources.png)

El [!UICONTROL Tasa de ingesta] El gráfico muestra la tasa de ingesta de datos en función del lapso de tiempo configurado. De forma predeterminada, el panel de monitorización muestra la tasa de ingesta de las últimas 24 horas. Para ver los pasos sobre cómo configurar el lapso de tiempo, lea la guía en [configuración del intervalo de tiempo de monitorización](monitor.md#configure-monitoring-time-frame).

El gráfico se muestra de forma predeterminada. Para ocultar el gráfico, seleccione **[!UICONTROL Métricas y gráficos]** para desactivar la opción y ocultar el gráfico.

![El gráfico de métricas de tasa de ingesta.](../assets/ui/monitor-sources/metrics-graph.png)

La parte inferior del panel muestra una tabla que describe el informe de métricas actuales para todos los flujos de datos de origen existentes.

![La tabla de métricas del panel de monitorización.](../assets/ui/monitor-sources/metrics-table.png)

| Métricas | Descripción |
| --- | --- |
| Registros recibidos | Número total de registros recibidos del origen. |
| Registros ingeridos | Número total de registros ingeridos en el lago de datos. |
| Registros omitidos | Número total de registros omitidos. |
| Error de registros | Número total de registros que no se pudieron ingerir debido a errores. |
| Tasa de ingesta | El porcentaje de registros que se ingirieron en función del número total de registros recibidos. |
| Total de flujos de datos fallidos | Número total de flujos de datos que han fallado. |

{style="table-layout:auto"}

Puede filtrar aún más los datos mediante las opciones proporcionadas sobre la tabla de métricas:

| Filtrado de opciones | Descripción |
| --- | --- |
| Buscar | Utilice la barra de búsqueda para filtrar la vista a un solo tipo de origen. |
| Fuentes | Seleccionar **[!UICONTROL Fuentes]** para filtrar la vista y mostrar los datos de métricas por tipo de origen. Esta es la visualización predeterminada que utiliza el panel de monitorización. |
| Flujos de datos | Seleccionar **[!UICONTROL Flujos de datos]** para filtrar la vista y mostrar los datos de métricas por flujo de datos. |
| Mostrar solo errores | Seleccionar **[!UICONTROL Mostrar solo errores]** para filtrar la vista y mostrar solo los flujos de datos que han informado sobre errores de ingesta. |
| Mis fuentes | Puede filtrar aún más la vista utilizando [!UICONTROL Mis fuentes] menú desplegable. Utilice el menú desplegable para filtrar la vista por categoría. Como alternativa, puede seleccionar **[!UICONTROL Todas las fuentes]** para mostrar las métricas de todos los recursos o fuentes, o seleccione **[!UICONTROL Mis fuentes]** para mostrar solo los orígenes con los que tiene una cuenta correspondiente. |

{style="table-layout:auto"}

Para monitorizar los datos que se están introduciendo en un flujo de datos específico, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto a una fuente.

![Monitorice un flujo de datos específico seleccionando el icono de filtro junto a una fuente determinada.](../assets/ui/monitor-sources/monitor-dataflow.png)

La tabla de métricas se actualiza a una tabla de flujos de datos activos que corresponden al origen seleccionado. Durante este paso, puede ver información adicional sobre los flujos de datos, incluido su conjunto de datos y tipo de datos correspondientes, así como una marca de tiempo para indicar cuándo fueron los últimos activos.

Para inspeccionar más a fondo un flujo de datos, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto a un flujo de datos.

![La tabla de flujos de datos del panel de monitorización.](../assets/ui/monitor-sources/select-dataflow.png)

A continuación, se le dirigirá a una interfaz que enumera todas las iteraciones de ejecución de flujo de datos del flujo de datos seleccionado.

Las ejecuciones de flujo de datos representan una instancia de ejecución de flujo de datos. Por ejemplo, si un flujo de datos está programado para ejecutarse por hora a las 9:00, 10:00 y 11:00 a.m., tendría tres instancias de ejecución de flujo. Las ejecuciones de flujo son específicas de su organización particular.

Para inspeccionar métricas de una iteración de ejecución de flujo de datos específica, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto al flujo de datos.

![La página de métrica de ejecución del flujo de datos.](../assets/ui/monitor-sources/dataflow-page.png)

Utilice esta página para ver las métricas y la información de la iteración de ejecución seleccionada.

![La página de detalles de ejecución del flujo de datos.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Detalles de ejecución del flujo de datos | Descripción |
| --- | --- |
| Registros ingeridos | El número total de registros que se ingirieron desde la ejecución del flujo de datos. |
| Error de registros | Número total de registros que no se ingirieron debido a errores en la ejecución del flujo de datos. |
| Total de archivos | Número total de archivos en la ejecución del flujo de datos. |
| Tamaño de los datos | El tamaño total de los datos contenidos en la ejecución del flujo de datos. |
| ID de ejecución de flujo de datos | El ID de la iteración de ejecución del flujo de datos. |
| ID de organización | El ID de la organización en la que se creó la ejecución del flujo de datos. |
| Estado | El estado de ejecución del flujo de datos. |
| Inicio de ejecución de flujo de datos | Una marca de tiempo que indica cuándo se inició la ejecución del flujo de datos. |
| Fin de ejecución de flujo de datos | Una marca de tiempo que indica cuándo terminó la ejecución del flujo de datos. |
| Conjunto de datos | Conjunto de datos utilizado para crear el flujo de datos. |
| Tipo de datos | El tipo de datos que se encontraban en el flujo de datos. |
| Ingesta parcial | La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos precisos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos. Puede habilitar la ingesta parcial durante el proceso de creación del flujo de datos. |
| Diagnósticos de error | Error diagnostics indica a la fuente que produzca diagnósticos de error a los que puede hacer referencia posteriormente al monitorizar la actividad del conjunto de datos y el estado del flujo de datos. Puede habilitar diagnósticos de error durante el proceso de creación del flujo de datos. |
| Resumen de errores | Ante una ejecución fallida del flujo de datos, el resumen del error muestra un código y una descripción de error para resumir por qué ha fallado la iteración de ejecución. |

{style="table-layout:auto"}

Si el flujo de datos ejecuta informes de errores, puede desplazarse hacia abajo hasta la parte inferior de la página utilizando [!UICONTROL Errores de ejecución de flujo de datos] interfaz.

Utilice el [!UICONTROL Error de registros] para ver las métricas de los registros que no se han introducido debido a errores. Para ver un informe de errores completo, seleccione **[!UICONTROL Previsualizar diagnósticos de error]**. Para descargar una copia del diagnóstico de errores y del manifiesto del archivo, seleccione **[!UICONTROL Descargar]** y, a continuación, copie la llamada de API de ejemplo que se utilizará con el [!DNL Data Access] API.

>[!NOTE]
>
>Solo puede utilizar diagnósticos de error si la función se ha habilitado durante el proceso de creación de la conexión de origen.

![El panel de errores de ejecución del flujo de datos.](../assets/ui/monitor-sources/errors.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha monitorizado correctamente el flujo de datos de ingesta desde el nivel de origen utilizando **[!UICONTROL Monitorización]** panel. También ha identificado correctamente los errores que contribuyeron al error de los flujos de datos durante el proceso de ingesta. Consulte los siguientes documentos para obtener más información:

* [Supervisión de datos de identidad](./monitor-identities.md).
* [Monitorización de datos de perfil](./monitor-profiles.md).
