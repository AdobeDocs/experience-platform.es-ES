---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos;fuentes
description: Este tutorial proporciona pasos para monitorizar el flujo de datos, mediante la vista de monitorización agregada y la monitorización entre servicios.
solution: Experience Platform
title: Monitorizar flujos de datos para orígenes en la interfaz de usuario
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Monitorización de flujos de datos para orígenes en la interfaz de usuario

>[!IMPORTANT]
>
>El panel de monitorización no admite actualmente fuentes de transmisión, como [HTTP API source](../../sources/connectors/streaming/http.md). En este momento, solo puede utilizar el panel para controlar los orígenes de lotes.

En Adobe Experience Platform, los datos se incorporan a partir de una amplia variedad de fuentes, se analizan en el Experience Platform y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia con flujos de datos.

El panel de monitorización proporciona una representación visual del recorrido de un flujo de datos. Puede utilizar una vista de monitorización agregada y navegar verticalmente desde el nivel de origen, hasta un flujo de datos y hasta una ejecución de flujo de datos, lo que le permite ver las métricas correspondientes que contribuyen al éxito o al fracaso de un flujo de datos. También puede utilizar la capacidad de supervisión entre servicios del panel de monitorización para supervisar el recorrido de un flujo de datos desde un origen, a [!DNL Identity Service] y a [!DNL Profile].

Este tutorial proporciona pasos para monitorizar el flujo de datos, mediante la vista de monitorización agregada y la monitorización entre servicios.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   * [Se ejecuta](../../sources/notifications.md) el flujo de datos: Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración de frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../sources/home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Servicio](../../identity-service/home.md) de identidad: Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [Perfil](../../profile/home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores para pruebas](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Vista de monitorización agregada

En la [Platform UI](https://platform.adobe.com), seleccione **[!UICONTROL Monitoring]** en el panel de navegación izquierdo para acceder al panel [!UICONTROL Monitoring]. El tablero [!UICONTROL Monitoring] contiene métricas e información sobre todos los flujos de datos de fuentes, incluida la información sobre el estado del tráfico de datos desde una fuente a [!DNL Identity Service] y a [!DNL Profile].

En el centro del tablero se encuentra el panel [!UICONTROL Source ingestion], que contiene métricas y gráficos que muestran datos en registros ingeridos y registros con errores.

![panel de monitorización](../assets/ui/monitor-sources/monitoring-dashboard.png)

De forma predeterminada, los datos mostrados contienen tasas de ingesta de las últimas 24 horas. Seleccione **[!UICONTROL Últimas 24 horas]** para ajustar el lapso de tiempo de los registros mostrados.

![fecha de cambio](../assets/ui/monitor-sources/change-date.png)

Aparece una ventana emergente de calendario que proporciona opciones para intervalos de tiempo de ingesta alternativos. Seleccione **[!UICONTROL Últimos 30 días]** y, a continuación, seleccione **[!UICONTROL Aplicar]**

![ajuste del intervalo de tiempo](../assets/ui/monitor-sources/adjust-timeframe.png)

Los gráficos están habilitados de forma predeterminada y puede deshabilitarlos para expandir la lista de fuentes a continuación. Seleccione la opción **[!UICONTROL Métricas y gráficos]** para desactivar los gráficos.

![métricas y gráficos](../assets/ui/monitor-sources/metrics-graphs.png)

| Ingesta de origen | Descripción |
| ---------------- | ----------- |
| [!UICONTROL Registros ingestados  ] | El número total de registros introducidos. |
| [!UICONTROL Error de registros] | El número total de registros que no se incorporaron debido a errores en los datos. |
| [!UICONTROL Total de flujos de datos fallidos] | El número total de flujos de datos con estado `failed`. |

La lista de consumo de origen muestra todas las fuentes que contienen al menos una cuenta existente. La lista también incluye información sobre la tasa de ingesta de cada fuente, el número de registros fallidos y el número total de flujos de datos fallidos en función del lapso de tiempo aplicado.

![ingesta de origen](../assets/ui/monitor-sources/source-ingestion.png)

Para ordenar por la lista de fuentes, seleccione **[!UICONTROL My sources]** y luego seleccione la categoría que desee en el menú desplegable. Por ejemplo, para centrarse en las almacenamiento en la nube, seleccione **[!UICONTROL Cloud storage]**

![ordenar por categoría](../assets/ui/monitor-sources/sort-by-category.png)

Para ver todos los flujos de datos existentes en todas las fuentes, seleccione **[!UICONTROL Flujos de datos]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Como alternativa, puede introducir una fuente en la barra de búsqueda para aislar una sola fuente. Una vez que haya identificado el origen, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) situado junto a él para ver una lista de sus flujos de datos activos.

![búsqueda](../assets/ui/monitor-sources/search.png)

Aparecerá una lista de flujos de datos. Para reducir la lista y centrarse en los flujos de datos con errores, seleccione **[!UICONTROL Mostrar solo errores]**.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Busque el flujo de datos que desea monitorizar y, a continuación, seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) que se encuentra junto a él para obtener más información sobre su estado de ejecución.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

La página de ejecución del flujo de datos muestra información sobre la fecha de inicio de la ejecución del flujo de datos, el tamaño de los datos, el estado y la duración del tiempo de procesamiento. Seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) situado junto al tiempo de inicio de la ejecución del flujo de datos para ver sus detalles de ejecución del flujo de datos.

![dataflow run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

La página [!UICONTROL Detalles de ejecución del flujo de datos] muestra información sobre los metadatos del flujo de datos, el estado de ingesta parcial y el resumen de errores. El resumen del error contiene el error específico de nivel superior que muestra en qué paso el proceso de ingesta encontró un error.

Desplácese hacia abajo para ver información más específica sobre el error que se ha producido.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

El panel [!UICONTROL Errores de ejecución de flujo de datos] muestra el error específico y el código de error que provocó el error de ingesta del flujo de datos. En este escenario, se produjo un error de transformación del asignador, que dio como resultado un error de 24 registros.

Seleccione **[!UICONTROL Files]** para obtener más información.

![dataflow run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

El panel [!UICONTROL Archivos] contiene información sobre el nombre y la ruta del archivo.

Para obtener una representación más granular del error, seleccione **[!UICONTROL Vista previa de diagnósticos de error]**.

![files](../assets/ui/monitor-sources/files.png)

Aparece la ventana [!UICONTROL Error diagnostic preview], que muestra una previsualización de hasta 100 errores en el flujo de datos. Puede seleccionar **[!UICONTROL Download]** para recuperar un comando curl, que luego le permite descargar los diagnósticos de error.

Cuando haya terminado, seleccione **[!UICONTROL Cerrar]**

![diagnóstico de errores](../assets/ui/monitor-sources/error-diagnostics.png)

Puede utilizar el sistema de rutas de exploración del encabezado superior para volver al tablero [!UICONTROL Monitoring]. Seleccione **[!UICONTROL Ejecutar inicio: 14/2/2021, 9:47 PM]** para volver a la página anterior y, a continuación, seleccione **[!UICONTROL Flujo de datos: Demostración de ingesta de datos de fidelidad: error]** al volver a la página de flujos de datos.

![rutas de exploración](../assets/ui/monitor-sources/breadcrumbs.png)

## Supervisión entre servicios

La parte superior del panel contiene una representación del flujo de ingesta desde el nivel de origen, hasta [!DNL Identity Service] y hasta [!DNL Profile]. Cada celda incluye un marcador de punto que indica la presencia de errores que se produjeron en esa fase de ingesta. Un punto verde significa una ingesta sin errores, mientras que un punto rojo significa que se ha producido un error en esa etapa concreta de ingesta.

![monitorización entre servicios](../assets/ui/monitor-sources/cross-service-monitoring.png)

En la página flujos de datos, busque un flujo de datos correcto y seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) que se encuentra junto a él para ver su información de ejecución del flujo de datos.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

La página [!UICONTROL Origen ingesta] contiene información que confirma la ingesta correcta del flujo de datos. Desde aquí, puede empezar a monitorizar el recorrido de su flujo de datos desde el nivel de origen, hasta [!DNL Identity Service] y luego hasta [!DNL Profile].

Seleccione **[!UICONTROL Identities]** para ver la ingesta en la etapa [!UICONTROL Identities].

![sources](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] métricas

La página [!UICONTROL Identity processing] contiene información sobre los registros ingestados a [!DNL Identity Service], incluido el número de identidades añadidas, los gráficos creados y los gráficos actualizados.

Seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) situado junto al tiempo de inicio de la ejecución del flujo de datos para ver más información sobre la ejecución del flujo de datos [!DNL Identity].

![identidades](../assets/ui/monitor-sources/identities.png)

| Métricas de identidad | Descripción |
| ---------------- | ----------- |
| [!UICONTROL Registros recibidos] | Número de registros recibidos de [!DNL Data Lake]. |
| [!UICONTROL Error de registros] | Número de registros que no se incorporaron en Platform debido a errores en los datos. |
| [!UICONTROL Registros omitidos] | El número de registros que se incorporaron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registro. |
| [!UICONTROL Registros ingestados] | Número de registros ingeridos en [!DNL Identity Service]. |
| [!UICONTROL Registros totales] | Recuento total de todos los registros, incluidos los registros con errores, los registros omitidos, los [!DNL Identities] agregados y los registros duplicados. |
| [!UICONTROL Identidades agregadas] | Número de identificadores nuevos netos agregados a [!DNL Identity Service]. |
| [!UICONTROL Gráficos creados] | Número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| [!UICONTROL Gráficos actualizados] | Número de gráficos de identidad existentes actualizados con bordes nuevos. |
| [!UICONTROL Se ejecutaron errores en el flujo de datos] | Número de ejecuciones de flujo de datos que han fallado. |
| [!UICONTROL Tiempo de procesamiento] | Marca de tiempo desde el inicio de la ingesta hasta la finalización. |
| [!UICONTROL Estado] | Define el estado general de un flujo de datos. Los valores de estado posibles son: <ul><li>`Success`: Indica que un flujo de datos está activo y que está incorporando datos según la programación proporcionada.</li><li>`Failed`: Indica que el proceso de activación de un flujo de datos se ha interrumpido debido a errores. </li><li>`Processing`: Indica que el flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos.</li></ul> |

La página [!UICONTROL Detalles de la ejecución del flujo de datos] muestra más información sobre la ejecución del flujo de datos [!DNL Identity], incluido su ID de organización de IMS y su ID de ejecución del flujo de datos. Esta página también muestra el código de error y el mensaje de error correspondientes proporcionados por [!DNL Identity Service], en caso de que se produzca algún error en el proceso de ingesta.

Seleccione **[!UICONTROL Ejecutar inicio: 14/2/2021, 9:47 PM]** para volver a la página anterior.

![identities-dataflow run](../assets/ui/monitor-sources/identities-dataflow-run.png)

En la página [!UICONTROL Identity processing], seleccione **[!UICONTROL Profiles]** para ver el estado de la ingesta de registros en la etapa [!UICONTROL Profiles].

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] métricas

La página [!UICONTROL Profile processing] contiene información sobre los registros ingestados a [!DNL Profile], incluido el número de fragmentos de perfil creados, los fragmentos de perfil actualizados y el número total de fragmentos de perfil.

Seleccione el icono de filtro ![filter](../assets/ui/monitor-sources/filter.png) situado junto al tiempo de inicio de la ejecución del flujo de datos para ver más información sobre la ejecución del flujo de datos [!DNL Profile].

![perfiles](../assets/ui/monitor-sources/profiles.png)

| Métricas de perfil | Descripción |
| --------------- | ----------- |
| [!UICONTROL Registros recibidos] | Número de registros recibidos de [!DNL Data Lake]. |
| [!UICONTROL Error de registros  ] | El número de registros que se incorporaron, pero no en [!DNL Profile] debido a errores. |
| [!UICONTROL Se han añadido fragmentos de perfil] | Número de nuevos fragmentos [!DNL Profile] netos añadidos. |
| [!UICONTROL Fragmentos de perfil actualizados] | El número de fragmentos existentes [!DNL Profile] actualizados |
| [!UICONTROL Fragmentos totales de perfil] | El número total de registros escritos en [!DNL Profile], incluidos todos los fragmentos [!DNL Profile] existentes actualizados y los nuevos fragmentos [!DNL Profile] creados. |
| [!UICONTROL Se ejecutaron errores en el flujo de datos] | Número de ejecuciones de flujo de datos que han fallado. |
| [!UICONTROL Tiempo de procesamiento] | Marca de tiempo desde el inicio de la ingesta hasta la finalización. |
| [!UICONTROL Estado] | Define el estado general de un flujo de datos. Los valores de estado posibles son: <ul><li>`Success`: Indica que un flujo de datos está activo y que está incorporando datos según la programación proporcionada.</li><li>`Failed`: Indica que el proceso de activación de un flujo de datos se ha interrumpido debido a errores. </li><li>`Processing`: Indica que el flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos.</li></ul> |

La página [!UICONTROL Detalles de la ejecución del flujo de datos] muestra más información sobre la ejecución del flujo de datos [!DNL Profile], incluido su ID de organización de IMS y su ID de ejecución del flujo de datos. Esta página también muestra el código de error y el mensaje de error correspondientes proporcionados por [!DNL Profile], en caso de que se produzca algún error en el proceso de ingesta.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Pasos siguientes

Al seguir este tutorial, ha monitorizado correctamente el flujo de datos de ingesta desde el nivel de origen, a [!DNL Identity Service] y a [!DNL Profile], utilizando el panel **[!UICONTROL Monitoring]**. También ha identificado correctamente los errores que han contribuido al error de los flujos de datos durante el proceso de ingesta. Consulte los siguientes documentos para obtener más información:

* [Resumen del perfil del cliente en tiempo real](../../profile/home.md)
* [Información general de Data Science Workspace](../../data-science-workspace/home.md)
