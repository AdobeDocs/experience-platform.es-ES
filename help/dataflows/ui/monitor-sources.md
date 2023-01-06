---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos;fuentes
description: Este tutorial proporciona pasos para monitorizar el flujo de datos, mediante la vista de monitorización agregada y la monitorización entre servicios.
solution: Experience Platform
title: Monitorizar flujos de datos para orígenes en la interfaz de usuario
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Monitorización de flujos de datos para orígenes en la interfaz de usuario

>[!IMPORTANT]
>
>Las fuentes de flujo continuo, como el [Fuente de API HTTP](../../sources/connectors/streaming/http.md) no son compatibles actualmente con el panel de monitorización. En este momento, solo puede utilizar el panel para controlar los orígenes de lotes.

En Adobe Experience Platform, los datos se incorporan a partir de una amplia variedad de fuentes, se analizan en el Experience Platform y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia con flujos de datos.

El panel de monitorización proporciona una representación visual del recorrido de un flujo de datos. Puede utilizar una vista de monitorización agregada y navegar verticalmente desde el nivel de origen, hasta un flujo de datos y hasta una ejecución de flujo de datos, lo que le permite ver las métricas correspondientes que contribuyen al éxito o al fracaso de un flujo de datos. También puede utilizar la capacidad de supervisión entre servicios del panel de monitorización para supervisar el recorrido de un flujo de datos desde un origen, hasta [!DNL Identity Service]y [!DNL Profile].

Este tutorial proporciona pasos para monitorizar el flujo de datos, mediante la vista de monitorización agregada y la monitorización entre servicios.

## Primeros pasos {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile]y [!DNL Destinations].
   * [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración de frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../sources/home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Servicio de identidad](../../identity-service/home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Vista de monitorización agregada {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Ingesta de origen"
>abstract="La vista de consumo de origen contiene información sobre el estado de la actividad de datos y las métricas del servicio de lago de datos, incluidos los registros ingeridos y los registros con errores. Consulte la guía de definición de métricas para obtener más información sobre métricas y gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Detalles de ejecución de flujo de datos"
>abstract="El procesamiento de fuentes contiene información sobre el estado de la actividad de datos y las métricas del servicio de lago de datos, incluidos los registros ingeridos y los registros con errores. Consulte la guía de definición de métricas para obtener más información sobre métricas y gráficos."
>text="Learn more in documentation"

En el [Interfaz de usuario de Platform](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Monitorización] tablero. La variable [!UICONTROL Monitorización] tablero contiene métricas e información sobre todos los flujos de datos de fuentes, incluida la información sobre el estado del tráfico de datos de una fuente a otra [!DNL Identity Service]y [!DNL Profile].

En el centro del panel se encuentra la variable [!UICONTROL Ingesta de origen] , que contiene métricas y gráficos que muestran datos en registros ingestados y registros con errores.

![panel de monitorización](../assets/ui/monitor-sources/monitoring-dashboard.png)

De forma predeterminada, los datos mostrados contienen tasas de ingesta de las últimas 24 horas. Select **[!UICONTROL Últimas 24 horas]** para ajustar el lapso de tiempo de los registros mostrados.

![fecha de cambio](../assets/ui/monitor-sources/change-date.png)

Aparece una ventana emergente de calendario que proporciona opciones para intervalos de tiempo de ingesta alternativos. Select **[!UICONTROL Últimos 30 días]** y, a continuación, seleccione **[!UICONTROL Aplicar]**

![ajuste del intervalo de tiempo](../assets/ui/monitor-sources/adjust-timeframe.png)

Los gráficos están habilitados de forma predeterminada y puede deshabilitarlos para expandir la lista de fuentes a continuación. Seleccione el **[!UICONTROL Métricas y gráficos]** para desactivar los gráficos.

![métricas y gráficos](../assets/ui/monitor-sources/metrics-graphs.png)

| Ingesta de origen | Descripción |
| ---------------- | ----------- |
| [!UICONTROL Registros ingestados ] | El número total de registros introducidos. |
| [!UICONTROL Error de registros] | El número total de registros que no se incorporaron debido a errores en los datos. |
| [!UICONTROL Total de flujos de datos fallidos] | El número total de flujos de datos con un `failed` estado. |

La lista de consumo de origen muestra todas las fuentes que contienen al menos una cuenta existente. La lista también incluye información sobre la tasa de ingesta de cada fuente, el número de registros fallidos y el número total de flujos de datos fallidos en función del lapso de tiempo aplicado.

![ingesta de origen](../assets/ui/monitor-sources/source-ingestion.png)

Para ordenar por la lista de fuentes, seleccione **[!UICONTROL Mis fuentes]** y, a continuación, seleccione la categoría que desee en el menú desplegable. Por ejemplo, para centrarse en las almacenamiento en la nube, seleccione  **[!UICONTROL Almacenamiento en la nube]**

![ordenar por categoría](../assets/ui/monitor-sources/sort-by-category.png)

Para ver todos los flujos de datos existentes en todas las fuentes, seleccione **[!UICONTROL Flujos de datos]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Como alternativa, puede introducir una fuente en la barra de búsqueda para aislar una sola fuente. Una vez que haya identificado el origen, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto a él para ver una lista de sus flujos de datos activos.

![búsqueda](../assets/ui/monitor-sources/search.png)

Aparecerá una lista de flujos de datos. Para reducir la lista y centrarse en los flujos de datos con errores, seleccione **[!UICONTROL Mostrar solo errores]**.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Busque el flujo de datos que desea monitorizar y, a continuación, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto a él, para ver más información sobre su estado de ejecución.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

La página de ejecución del flujo de datos muestra información sobre la fecha de inicio de la ejecución del flujo de datos, el tamaño de los datos, el estado y la duración del tiempo de procesamiento. Seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto al tiempo de inicio de ejecución del flujo de datos para ver sus detalles de ejecución del flujo de datos.

![dataflow run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

La variable [!UICONTROL Detalles de ejecución de flujo de datos] muestra información sobre los metadatos del flujo de datos, el estado de ingesta parcial y el resumen de errores. El resumen del error contiene el error específico de nivel superior que muestra en qué paso el proceso de ingesta encontró un error.

Desplácese hacia abajo para ver información más específica sobre el error que se ha producido.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

La variable [!UICONTROL Errores de ejecución del flujo de datos] muestra el error específico y el código de error que provocó el error de ingesta del flujo de datos. En este escenario, se produjo un error de transformación del asignador, que dio como resultado un error de 24 registros.

Select **[!UICONTROL Archivos]** para obtener más información.

![dataflow run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

La variable [!UICONTROL Archivos] contiene información sobre el nombre y la ruta del archivo.

Para una representación más granular del error, seleccione **[!UICONTROL Previsualizar diagnósticos de error]**.

![files](../assets/ui/monitor-sources/files.png)

La variable [!UICONTROL Vista previa del diagnóstico de errores] , mostrando una vista previa de hasta 100 errores en el flujo de datos. Puede seleccionar **[!UICONTROL Descargar]** para recuperar un comando curl, que luego le permite descargar los diagnósticos de error.

Cuando haya terminado, seleccione **[!UICONTROL Cerrar]**

![diagnóstico de errores](../assets/ui/monitor-sources/error-diagnostics.png)

Puede utilizar el sistema de rutas de exploración del encabezado superior para volver al [!UICONTROL Monitorización] tablero. Select **[!UICONTROL Ejecutar inicio: 14/2/2021, 9:47 PM]** para volver a la página anterior y, a continuación, seleccione **[!UICONTROL Flujo de datos: Demostración de ingesta de datos de fidelidad: error]** para volver a la página flujos de datos.

![rutas de exploración](../assets/ui/monitor-sources/breadcrumbs.png)

## Pasos siguientes {#next-steps}

Siguiendo este tutorial, ha monitorizado correctamente el flujo de datos de ingesta desde el nivel de origen utilizando la variable **[!UICONTROL Monitorización]** tablero. También ha identificado correctamente los errores que han contribuido al error de los flujos de datos durante el proceso de ingesta. Consulte los siguientes documentos para obtener más información:

* [Supervisión de identidades en flujos de datos](./monitor-identities.md)
* [Supervisión de perfiles en flujos de datos](./monitor-profiles.md)
