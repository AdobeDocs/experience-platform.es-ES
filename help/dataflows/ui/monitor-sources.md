---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos;fuentes
description: Este tutorial proporciona pasos para monitorizar el flujo de datos mediante la vista de monitorización agregada y la monitorización entre servicios.
solution: Experience Platform
title: Monitorización de flujos de datos para fuentes en la IU
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 8%

---

# Monitorización de flujos de datos para orígenes en la interfaz de usuario

>[!IMPORTANT]
>
>Fuentes de flujo, como la [Fuente de API HTTP](../../sources/connectors/streaming/http.md) no son compatibles actualmente con el tablero de monitorización. En este momento, solo puede utilizar el panel para monitorizar los orígenes de lotes.

En Adobe Experience Platform, los datos se incorporan desde una amplia variedad de fuentes, se analizan dentro de Experience Platform y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia a los flujos de datos.

El panel de monitorización le proporciona una representación visual del recorrido de un flujo de datos. Puede utilizar una vista de monitorización agregada y navegar verticalmente desde el nivel de origen, a un flujo de datos y a una ejecución de flujo de datos, lo que le permite ver las métricas correspondientes que contribuyen al éxito o al fracaso de un flujo de datos. También puede utilizar la capacidad de monitorización entre servicios del panel de monitorización para monitorizar el recorrido de un flujo de datos desde un origen a [!DNL Identity Service], y a [!DNL Profile].

Este tutorial proporciona pasos para monitorizar el flujo de datos mediante la vista de monitorización agregada y la monitorización entre servicios.

## Primeros pasos {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   * [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../sources/home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Servicio de identidad](../../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento uniendo identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Vista de monitorización agregada {#aggregated-monitoring-view}

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

En el [IU de Platform](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** desde la navegación izquierda para acceder a [!UICONTROL Monitorización] panel. El [!UICONTROL Monitorización] El tablero contiene métricas e información sobre todos los flujos de datos de origen, incluida información sobre el estado del tráfico de datos de una fuente a [!DNL Identity Service], y a [!DNL Profile].

En el centro del salpicadero se encuentra el [!UICONTROL Ingesta de origen] panel, que contiene métricas y gráficos que muestran datos sobre registros ingeridos y registros fallidos.

![monitoring-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

De forma predeterminada, los datos mostrados contienen tasas de ingesta de las últimas 24 horas. Seleccionar **[!UICONTROL Últimas 24 horas]** para ajustar el lapso de tiempo de los registros mostrados.

![change-date](../assets/ui/monitor-sources/change-date.png)

Aparece una ventana emergente de calendario, que proporciona opciones para marcos de tiempo de ingesta alternativos. Seleccionar **[!UICONTROL Últimos 30 días]** y luego seleccione **[!UICONTROL Aplicar]**

![adjust-time-frame](../assets/ui/monitor-sources/adjust-timeframe.png)

Los gráficos están activados de forma predeterminada y puede desactivarlos para ampliar la lista de fuentes a continuación. Seleccione el **[!UICONTROL Métricas y gráficos]** para desactivar los gráficos.

![metrics-and-graphics](../assets/ui/monitor-sources/metrics-graphs.png)

| Ingesta de origen | Descripción |
| ---------------- | ----------- |
| [!UICONTROL Registros ingeridos ] | Número total de registros ingeridos. |
| [!UICONTROL Error de registros] | Número total de registros que no se ingirieron debido a errores en los datos. |
| [!UICONTROL Total de flujos de datos fallidos] | El número total de flujos de datos con un `failed` estado. |

La lista de ingesta de fuentes muestra todas las fuentes que contienen al menos una cuenta existente. La lista también incluye información sobre la tasa de ingesta de cada origen, el número de registros fallidos y el número total de flujos de datos fallidos en función del lapso de tiempo aplicado.

![source-ingestion](../assets/ui/monitor-sources/source-ingestion.png)

Para ordenar por la lista de orígenes, seleccione **[!UICONTROL Mis fuentes]** y, a continuación, seleccione la categoría que desee en el menú desplegable. Por ejemplo, para centrarse en el almacenamiento en la nube, seleccione  **[!UICONTROL Almacenamiento en la nube]**

![clasificar por categoría](../assets/ui/monitor-sources/sort-by-category.png)

Para ver todos los flujos de datos existentes en todas las fuentes, seleccione **[!UICONTROL Flujos de datos]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

También puede introducir una fuente en la barra de búsqueda para aislar una sola fuente. Una vez identificado el origen, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto a él para ver una lista de sus flujos de datos activos.

![búsqueda](../assets/ui/monitor-sources/search.png)

Aparecerá una lista de flujos de datos. Para reducir la lista y centrarse en los flujos de datos con errores, seleccione **[!UICONTROL Mostrar solo errores]**.

![show-failures-only](../assets/ui/monitor-sources/show-failures-only.png)

Busque el flujo de datos que desea monitorizar y, a continuación, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) al lado, para ver más información sobre su estado de ejecución.

![flujo de datos](../assets/ui/monitor-sources/dataflow.png)

La página de ejecución del flujo de datos muestra información sobre la fecha de inicio de ejecución del flujo de datos, el tamaño de los datos, el estado y su duración del tiempo de procesamiento. Seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) junto al tiempo de inicio de ejecución del flujo de datos para ver sus detalles de ejecución.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

El [!UICONTROL Detalles de ejecución del flujo de datos] Esta página muestra información sobre los metadatos del flujo de datos, el estado de ingesta parcial y el resumen de errores. El resumen del error contiene el error de nivel superior específico que muestra en qué paso el proceso de ingesta encontró un error.

Desplácese hacia abajo para ver información más específica sobre el error que se ha producido.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

El [!UICONTROL Errores de ejecución de flujo de datos] el panel muestra el error específico y el código de error que resultó en el error de ingesta del flujo de datos. En este escenario, se produjo un error de transformación del asignador, que resultó en el error de 24 registros.

Seleccionar **[!UICONTROL Archivos]** para obtener más información.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

El [!UICONTROL Archivos] el panel contiene información sobre el nombre y la ruta del archivo.

Para obtener una representación más granular del error, seleccione **[!UICONTROL Previsualizar diagnósticos de error]**.

![archivos](../assets/ui/monitor-sources/files.png)

El [!UICONTROL Previsualización de diagnósticos de error] aparece una ventana que muestra una previsualización de hasta 100 errores en el flujo de datos. Puede seleccionar **[!UICONTROL Descargar]** para recuperar un comando curl, que le permite descargar los diagnósticos de error.

Cuando haya terminado, seleccione **[!UICONTROL Cerrar]**

![diagnóstico de errores](../assets/ui/monitor-sources/error-diagnostics.png)

Puede utilizar el sistema de ruta de exploración en el encabezado superior para volver al [!UICONTROL Monitorización] panel. Seleccionar **[!UICONTROL Ejecutar inicio: 14/2/2021, 21:47]** para volver a la página anterior y, a continuación, seleccione **[!UICONTROL Flujo de datos: demostración de ingesta de datos de fidelidad: fallido]** para volver a la página flujos de datos.

![rutas de exploración](../assets/ui/monitor-sources/breadcrumbs.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha monitorizado correctamente el flujo de datos de ingesta desde el nivel de origen utilizando **[!UICONTROL Monitorización]** panel. También ha identificado correctamente los errores que contribuyeron al error de los flujos de datos durante el proceso de ingesta. Consulte los siguientes documentos para obtener más información:

* [Supervisión de identidades en flujos de datos](./monitor-identities.md)
* [Supervisión de perfiles en flujos de datos](./monitor-profiles.md)
