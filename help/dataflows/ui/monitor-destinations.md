---
description: Descubra cómo puede monitorizar los flujos de datos de sus destinos mediante la interfaz de usuario de Experience Platform.
solution: Experience Platform
title: Monitorización de flujos de datos para destinos en la IU
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: c024637ab73a3a1c3d2512f9879303b4e4d830a9
workflow-type: tm+mt
source-wordcount: '3484'
ht-degree: 10%

---

# Monitorización de flujos de datos para destinos en la IU

Utilice los distintos destinos del catálogo de Experience Platform para activar los datos de Experience Platform en innumerables socios externos. Experience Platform facilita el proceso de seguimiento del flujo de datos a sus destinos al proporcionar transparencia con los flujos de datos.

El panel de monitorización le proporciona una representación visual del recorrido de un flujo de datos, incluido el destino al que se activan los datos, el tipo de datos que está viendo, los datos exportados por ejecución de flujo de datos y mucho más.

Este tutorial proporciona instrucciones sobre cómo puede supervisar los flujos de datos directamente en el espacio de trabajo de destinos o utilizar el panel de monitorización para supervisar los flujos de datos de sus destinos mediante la interfaz de usuario de Experience Platform.

## Introducción {#getting-started}

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Experience Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
- [Destinos](../../destinations/home.md): los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Experience Platform para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Monitorización de flujos de datos en el espacio de trabajo Destinos {#monitor-dataflows-in-the-destinations-workspace}

En el área de trabajo **[!UICONTROL Destinations]** dentro de la interfaz de usuario de Experience Platform, vaya a la pestaña **[!UICONTROL Browse]** y seleccione el nombre de un destino que desee ver.

![Seleccionar vista de destino con una conexión de destino resaltada](../assets/ui/monitor-destinations/select-destination.png)

Aparecerá una lista de flujos de datos existentes. En esta página hay una lista de flujos de datos visibles, que incluye información sobre su destino, nombre de usuario, número de flujos de datos y estado.

Consulte la siguiente tabla para obtener más información sobre los estados:

| Estado | Descripción |
| ------ | ----------- |
| Habilitado | El estado `Enabled` indica que un flujo de datos está activo y está exportando datos de acuerdo con la programación que se proporcionó. |
| Desactivado | El estado `Disabled` indica que un flujo de datos está inactivo y no se está exportando ningún dato. |
| Procesamiento | El estado `Processing` indica que un flujo de datos aún no está activo. Este estado suele encontrarse inmediatamente después de crear un nuevo flujo de datos. |
| Error | El estado `Error` indica que el proceso de activación de un flujo de datos se ha interrumpido. |

### El flujo de datos se ejecuta para destinos de streaming {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Detalles de ejecución del flujo de datos"
>abstract="Los detalles de ejecución del flujo de datos de destino contienen información sobre el estado de activación de un público y las métricas obtenidas del perfil del cliente en tiempo real para generar identidades únicas. Para obtener más información, consulte la guía de definiciones de métricas."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Perfiles recibidos"
>abstract="Número total de perfiles recibidos en el flujo de datos. Este valor se actualiza cada 60 minutos."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identidades activadas"
>abstract="Recuento de identidades de perfil individuales activadas correctamente en el destino seleccionado. Esta métrica incluye las identidades creadas, actualizadas y eliminadas de los públicos exportados."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identidades excluidas"
>abstract="Recuento de registros de perfil individuales excluidos de la activación para el destino seleccionado en función de atributos que faltan y de la infracción de consentimiento."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Error de identidades"
>abstract="Recuento de identidades de perfiles individuales que fallaron para el destino seleccionado. Consulte los diagnósticos de errores para obtener más información."

Para los destinos de streaming, la pestaña [!UICONTROL Dataflow runs] proporciona una actualización por hora para los datos de métricas en las ejecuciones del flujo de datos. Las estadísticas más destacadas etiquetadas son para identidades.

Las identidades representan las diferentes facetas de un perfil. Por ejemplo, si un perfil contiene un número de teléfono y una dirección de correo electrónico, ese perfil tiene dos identidades.

Se muestra una lista de ejecuciones individuales y sus métricas particulares, junto con los siguientes totales de identidades:

- **[!UICONTROL Identities activated]**: el número total de identidades de perfil activadas correctamente en el destino seleccionado. Esta métrica incluye las identidades creadas, actualizadas y eliminadas de los públicos exportados.
- **[!UICONTROL Identities excluded]**: el número total de identidades de perfil que se omiten para la activación en función de los atributos que faltan y la infracción de consentimiento.
- **[!UICONTROL Identities failed]**: el número total de identidades de perfil que no se activaron en el destino debido a errores.

![El flujo de datos ejecuta detalles para los destinos de flujo continuo.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Cada ejecución de flujo de datos individual muestra los siguientes detalles:

- **[!UICONTROL Dataflow run start]**: hora a la que se inició la ejecución del flujo de datos. Para las ejecuciones de flujo de datos de flujo continuo, Experience Platform captura métricas basadas en el inicio de la ejecución del flujo de datos en forma de métricas por hora. Esto significa que, para las ejecuciones de flujo de datos de streaming, si una ejecución de flujo de datos comenzó, por ejemplo, a las 10:30PM, la métrica muestra la hora de inicio a las 10:00 p.m. en la interfaz de usuario.
- **[!UICONTROL Processing time]**: cantidad de tiempo que tardó la ejecución del flujo de datos en procesarse.
   - Para las ejecuciones de **[!UICONTROL completed]**, la métrica de tiempo de procesamiento siempre muestra una hora.
   - Para las ejecuciones de flujo de datos que siguen en estado **[!UICONTROL processing]**, la ventana para capturar todas las métricas permanece abierta durante más de una hora para procesar todas las métricas que corresponden a la ejecución de flujo de datos. Por ejemplo, una ejecución de flujo de datos que se inició a las 9:30 a. m. podría permanecer en un estado de procesamiento durante una hora y treinta minutos para capturar y procesar todas las métricas. La duración del tiempo de procesamiento se ve directamente afectada por los reintentos realizados como resultado de la respuesta fallida del destino. Entonces, una vez que se cierre la ventana de procesamiento y el estado de ejecución del flujo de datos se actualice a **completado**, el tiempo de procesamiento mostrado se cambia a una hora.
- **[!UICONTROL Profiles received]**: el número total de perfiles recibidos en el flujo de datos.
- **[!UICONTROL Identities activated]**: el número total de identidades de perfil que se activaron correctamente en el destino seleccionado como parte de la ejecución del flujo de datos. Esta métrica incluye las identidades creadas, actualizadas y eliminadas de los públicos exportados.
- **[!UICONTROL Identities excluded]**: el número total de identidades de perfil que se excluyen de la activación en función de los atributos que faltan y la infracción de consentimiento.
- **[!UICONTROL Identities failed]**: el número total de identidades de perfil que no se activaron en el destino debido a errores.

  >[!IMPORTANT]
  >
  > Desde marzo de 2025, Adobe está implementando gradualmente una actualización para aumentar la precisión de la creación de informes en los destinos de streaming. Esta mejora garantiza una mejor alineación entre los informes de Experience Platform y las plataformas de destino.
  >
  > Antes de esta actualización, **[!UICONTROL Identities failed]** incluía todos los reintentos de activación. Después de esta actualización, solo se incluye el último reintento de activación en el recuento total.
  > 
  > Esta mejora se aplica a todos los destinos de flujo continuo.
  > Tras esta mejora, es posible que los usuarios de destinos de flujo continuo vean una caída esperada en su recuento de **[!UICONTROL Identities failed]**.


- **[!UICONTROL Activation rate]**: porcentaje de identidades recibidas que se activaron correctamente. La fórmula siguiente muestra cómo se calcula este valor:
  ![Fórmula de tasa de activación.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: representa el estado en el que se encuentra el flujo de datos: [!UICONTROL Completed] o [!UICONTROL Processing]. [!UICONTROL Completed] significa que todas las identidades de la ejecución del flujo de datos correspondiente se exportaron dentro del período de una hora. [!UICONTROL Processing] significa que la ejecución del flujo de datos aún no ha finalizado.

Para ver los detalles de una ejecución de flujo de datos determinada, seleccione la hora de inicio de la ejecución en la lista.

La página de detalles de una ejecución de flujo de datos contiene información adicional, como el número de perfiles recibidos, el número de identidades activadas, el número de identidades fallidas y el número de identidades excluidas.

![Detalles de flujo de datos para destinos de flujo continuo.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

La página de detalles también muestra una lista de identidades que fallaron y las identidades que se excluyeron. Se muestra información tanto para las identidades fallidas como para las excluidas, incluido el código de error, el recuento de identidades y la descripción. De forma predeterminada, la lista muestra las identidades fallidas. Para mostrar las identidades omitidas, seleccione la opción **[!UICONTROL Identities excluded]**.

![Registros de flujo de datos para destinos de flujo continuo con un mensaje de error resaltado.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### Monitorización de ejecución de flujo de datos de nivel de audiencia para destinos de streaming {#audience-level-dataflow-runs-for-streaming-destinations}

Puede ver información sobre las identidades activadas, excluidas o fallidas desglosada a nivel de audiencia para cada audiencia que forme parte del flujo de datos.

La monitorización a nivel de audiencia para destinos de streaming solo está disponible para ciertos destinos. Consulte la sección [vista de nivel de audiencia](#audience-level-view) para obtener una lista de los destinos admitidos.

![Supervisión a nivel de audiencia para destinos de flujo continuo.](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>Es posible que el número **[!UICONTROL Profiles received]** de la pestaña **[!UICONTROL Audiences]** no siempre coincida con el número de perfiles recibidos para la ejecución del flujo de datos. Esto se debe a que un perfil determinado puede formar parte de más de una audiencia que se activa en la ejecución del flujo de datos.

### El flujo de datos se ejecuta para destinos de lote {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Detalles de ejecución del flujo de datos"
>abstract="Los detalles de ejecución del flujo de datos de destino contienen información sobre el estado de activación de un público y las métricas obtenidas del perfil del cliente en tiempo real para generar identidades únicas. Para obtener más información, consulte la guía de definiciones de métricas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html?lang=es#dataflow-runs-for-streaming-destinations" text="El flujo de datos se ejecuta para destinos de streaming"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Perfiles recibidos"
>abstract="Número total de perfiles recibidos en el flujo de datos. Este valor se actualiza cada 60 minutos."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identidades activadas"
>abstract="Recuento de identidades de perfil individuales activadas correctamente en el destino seleccionado. Esta métrica incluye las identidades creadas, actualizadas y eliminadas de los públicos exportados."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identidades excluidas"
>abstract="Recuento de registros de perfil individuales excluidos de la activación para el destino seleccionado en función de atributos que faltan y de la infracción de consentimiento."

Para los destinos por lotes, la pestaña [!UICONTROL Dataflow runs] proporciona datos de métricas sobre las ejecuciones del flujo de datos. Se muestra una lista de ejecuciones individuales y sus métricas particulares, junto con los siguientes totales de identidades:

- **[!UICONTROL Identities activated]**: el número total de identidades de perfil activadas correctamente en el destino seleccionado. Esta métrica incluye las identidades creadas, actualizadas y eliminadas de los públicos exportados.
- **[!UICONTROL Identities excluded]**: el recuento de identidades de perfil individuales excluidas de la activación para el destino seleccionado, en función de los atributos que faltan y la infracción de consentimiento.

![El flujo de datos ejecuta la vista para destinos por lotes.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Cada ejecución de flujo de datos individual muestra los siguientes detalles:

- **[!UICONTROL Dataflow run start]**: hora a la que se inició la ejecución del flujo de datos.
- **[!UICONTROL Audience]**: nombre de la audiencia asociada con cada ejecución de flujo de datos.
- **[!UICONTROL Processing time]**: cantidad de tiempo que tardó la ejecución del flujo de datos en procesarse.
- **[!UICONTROL Profiles received]**: el número total de perfiles recibidos en el flujo de datos. Este valor se actualiza cada 60 minutos.
- **[!UICONTROL Identities activated]**: el número total de identidades de perfil que se activaron correctamente en el destino seleccionado como parte de la ejecución del flujo de datos. Esta métrica incluye las identidades creadas, actualizadas y eliminadas de los públicos exportados.
- **[!UICONTROL Identities excluded]**: el número total de identidades de perfil que se excluyen de la activación en función de los atributos que faltan y la infracción de consentimiento.
- **[!UICONTROL Status]**: representa el estado en el que se encuentra el flujo de datos. Este puede ser uno de los tres estados: [!UICONTROL Success], [!UICONTROL Failed] y [!UICONTROL Processing]. [!UICONTROL Success] significa que el flujo de datos está activo y está exportando datos de acuerdo con la programación proporcionada. [!UICONTROL Failed] significa que la activación de datos se ha suspendido debido a errores. [!UICONTROL Processing] significa que el flujo de datos aún no está activo y se suele encontrar cuando se crea un nuevo flujo de datos.

Para ver los detalles de una ejecución de flujo de datos específica, seleccione la hora de inicio de la ejecución en la lista.

>[!NOTE]
>
>Las ejecuciones del flujo de datos se generan en función de la frecuencia de programación del flujo de datos de destino. Se ejecuta un flujo de datos por separado para cada [política de combinación](../../profile/merge-policies/overview.md) aplicada a una audiencia.

La página de detalles de un flujo de datos, además de los detalles que se muestran en la lista de flujos de datos, muestra información más específica sobre el flujo de datos:

- **[!UICONTROL Size of data]**: tamaño del flujo de datos que se está exportando.
- **[!UICONTROL Total files]**: número total de archivos exportados en el flujo de datos.
- **[!UICONTROL Last updated]**: hora a la que se ejecutó el flujo de datos por última vez.

![Detalles de ejecución del flujo de datos para destinos por lotes.](../assets/ui/monitor-destinations/dataflow-batch.png)

La página de detalles también muestra una lista de identidades que fallaron y las identidades que se excluyeron. Se muestra información tanto para las identidades fallidas como para las excluidas, incluido el código de error y la descripción. De forma predeterminada, la lista muestra las identidades fallidas. Para mostrar las identidades excluidas, seleccione la opción **[!UICONTROL Identities excluded]**.

![Registros de flujo de datos para destinos por lotes con un mensaje de error resaltado.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### Ver en monitorización {#view-in-monitoring}

También puede seleccionar ver información enriquecida sobre un flujo de datos determinado y su flujo de datos se ejecuta en el panel de monitorización. Para ver información sobre un flujo de datos en el panel de control:

1. Vaya a la pestaña **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**
2. Vaya al flujo de datos que desee inspeccionar.
3. Seleccione el símbolo de puntos suspensivos y el ![icono de supervisión](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]**.

![Seleccione Ver en la supervisión del flujo de trabajo de destinos para obtener más información sobre un flujo de datos.](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>Ahora puede ver información sobre el flujo de datos y sus ejecuciones de flujo de datos asociadas en el panel de monitorización. Lea la sección siguiente para obtener más información.

## Panel de control de monitorización de destinos {#monitoring-destinations-dashboard}

>[!NOTE]
>
>Actualmente, la funcionalidad de supervisión de destinos es compatible con todos los destinos de Experience Platform *excepto* los destinos de [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) y [Personalización personalizada](/help/destinations/catalog/personalization/custom-personalization.md).

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="La vista de activación de destino contiene información sobre el estado de activación de un público y las métricas obtenidas del perfil del cliente en tiempo real para generar identidades únicas."

Para acceder al panel [!UICONTROL Monitoring], seleccione **[!UICONTROL Monitoring]** (![icono de supervisión](/help/images/icons/monitoring.png)) en el panel de navegación izquierdo. Una vez en la página [!UICONTROL Monitoring], seleccione [!UICONTROL Destinations]. El panel [!UICONTROL Monitoring] contiene métricas e información sobre los trabajos de ejecución de destino.

Utilice el panel [!UICONTROL Destinations] para obtener una idea general del estado de los flujos de activación. Comience por obtener perspectivas en un nivel agregado para todos los destinos de lote y flujo continuo y, a continuación, explore las vistas detalladas de flujos de datos, ejecuciones de flujos de datos y audiencias activadas para obtener una vista detallada de los datos de activación. Las pantallas del panel [!UICONTROL Monitoring] proporcionan información procesable a través de métricas y descripciones de error que le ayudarán a solucionar cualquier problema que pueda surgir en sus escenarios de activación.

Puede filtrar la información mostrada por tipo de datos: clientes, cuentas (solo para Adobe Real-Time CDP B2B edition), clientes potenciales y enriquecimiento de cuentas. Obtenga más información sobre estas opciones en la [guía de supervisión del panel](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![Filtro de tipo de datos resaltado en la vista del panel de supervisión.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

En el centro del tablero se encuentra el panel [!UICONTROL Activation], que contiene métricas y gráficos que muestran datos sobre la velocidad de activación de los datos que se exportan a destinos de flujo continuo, así como sobre las ejecuciones de flujo de datos por lotes fallidas a destinos por lotes.

![Gráficos de activación por lotes y de transmisión resaltados en la vista de supervisión.](../assets/ui/monitor-destinations/dashboard-graph.png)


De forma predeterminada, los datos mostrados contienen la información de activación de las últimas 24 horas. Seleccione **[!UICONTROL Last 24 hours]** para ajustar el lapso de tiempo de los registros mostrados. Las opciones disponibles son **[!UICONTROL Last 24 hours]**, **[!UICONTROL Last 7 days]** y **[!UICONTROL Last 30 days]**. También puede seleccionar las fechas en la ventana emergente de calendario que aparece. Una vez seleccionadas las fechas, seleccione **[!UICONTROL Apply]** para ajustar el lapso de tiempo de la información mostrada.

>[!NOTE]
>
>La siguiente captura de pantalla muestra la tasa de activación y las ejecuciones del flujo de datos por lotes durante los últimos 30 días en lugar de las últimas 24 horas. Puede ajustar el lapso de tiempo seleccionando **[!UICONTROL Last 30 days]**.

![Cambiar el control de intervalo de fecha retrospectiva resaltado para los destinos activados](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Utilice el icono de flecha (![icono de flecha](/help/images/icons/chevron-up.png)) para expandir o descartar las tarjetas en la parte superior de la pantalla, que muestran información rápida sobre los detalles de activación, según el tipo de destino: flujo continuo o lote:

- **[!UICONTROL Streaming activation rate]**: representa el porcentaje de identidades recibidas que se activaron u omitieron correctamente. La fórmula utilizada para calcular este porcentaje se describe más arriba en esta página, en la sección [Flujo de datos se ejecuta para destinos de flujo continuo](#dataflow-runs-for-streaming-destinations).
- **[!UICONTROL Batch failed dataflow runs]**: representa el número de ejecuciones de flujo de datos fallidas en el intervalo de tiempo seleccionado.

![Mostrar o descartar tarjetas en la parte superior de la página.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

El gráfico **[!UICONTROL Activation]** se muestra de manera predeterminada y puede deshabilitarlo para expandir la lista de destinos siguiente. Seleccione el conmutador **[!UICONTROL Metrics and graphs]** para deshabilitar los gráficos.

El panel **[!UICONTROL Activation]** muestra una lista de destinos que contienen al menos una cuenta existente. Esta lista también incluye información sobre los perfiles recibidos, las identidades activadas, las identidades fallidas, las identidades excluidas, la tasa de activación, el total de flujos de datos fallidos y la última fecha de actualización de estos destinos. No todas las métricas están disponibles para todos los tipos de destino. En la tabla siguiente se describen las métricas y la información disponible por tipo de destino.

| Métrica | Tipo de destino |
|--------------------------------------|-----------------------|
| **[!UICONTROL Records received]** | Transmisión y lote |
| **[!UICONTROL Records activated]** | Transmisión y lote |
| **[!UICONTROL Records failed]** | Streaming |
| **[!UICONTROL Records skipped]** | Transmisión y lote |
| **[!UICONTROL Data type]** | Transmisión y lote |
| **[!UICONTROL Activation rate]** | Streaming |
| **[!UICONTROL Total failed dataflows]** | Lote |
| **[!UICONTROL Last updated]** | Transmisión y lote |

{style="table-layout:auto"}

![Panel de monitorización con todos los destinos activados resaltados.](../assets/ui/monitor-destinations/dashboard-destinations.png)

También puede filtrar la lista de destinos para mostrar solo la categoría de destinos seleccionada. Seleccione el menú desplegable **[!UICONTROL My destinations]** y seleccione la [categoría de destino](/help/destinations/destination-types.md#categories) a la que desee aplicar el filtro.

![Filtrar destinos usando el selector desplegable](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Además, puede introducir un destino en la barra de búsqueda para aislar a un solo destino. Si desea ver los flujos de datos del destino, puede seleccionar el filtro ![filter](/help/images/icons/filter-add.png) que está junto a él para ver una lista de sus flujos de datos activos.

![Filtrar destinos usando la barra de búsqueda resaltada en la vista de supervisión.](../assets/ui/monitor-destinations/filtered-destinations.png)

Si desea ver todos los flujos de datos existentes en todos los destinos, seleccione **[!UICONTROL Dataflows]**.

Aparecerá una lista de flujos de datos, ordenados por la última ejecución del flujo de datos. Puede ver detalles adicionales de un flujo de datos específico localizando el destino que desea monitorizar, seleccionando el filtro ![filter](/help/images/icons/filter-add.png) al lado y, a continuación, seleccionando el filtro ![filter](/help/images/icons/filter-add.png) al lado del flujo de datos del que desea obtener más información.

![Todos los flujos de datos resaltados en el panel de supervisión.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Una vez que seleccione un flujo de datos para realizar una inspección adicional, la página de detalles del flujo de datos contiene un conmutador que le permite ver los datos activados en el flujo de datos, desglosados por ejecuciones de flujo de datos o audiencias.

### Vista de ejecuciones de flujo de datos {#dataflow-runs-view}

Cuando se selecciona **[!UICONTROL Dataflow runs]**, puede ver una lista de ejecuciones de flujo de datos para el flujo de datos seleccionado y más información sobre cada ejecución.

>[!INFO]
>
>Para los flujos de datos a destinos de flujo continuo, una ejecución de flujo de datos se desglosa en ventanas por hora. Cada ventana por hora genera un ID de ejecución de flujo de datos correspondiente.
>
>Para los flujos de datos a destinos por lotes, cada audiencia tiene generado una ejecución de flujo de datos correspondiente, en función de la frecuencia programada de activación de audiencia. Por ejemplo, si configura una activación programada diaria para cinco audiencias en el mismo flujo de datos de destino, se generarán cinco ejecuciones de flujo de datos independientes cada día.

![El flujo de datos ejecuta el panel con varias ejecuciones resaltadas.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Utilice la opción **[!UICONTROL Show failures only]** para mostrar solo las ejecuciones fallidas de un flujo de datos.

![El flujo de datos ejecuta la vista con la opción de mostrar solo los errores resaltada](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Vista de nivel de audiencia {#segment-level-view}

Cuando se selecciona **[!UICONTROL Audiences]**, se muestra una lista de las audiencias que se activaron en el flujo de datos seleccionado, dentro del intervalo de tiempo seleccionado. Esta pantalla incluye información a nivel de audiencia sobre los registros activados, los registros excluidos, así como el estado y la hora de la última ejecución del flujo de datos. Al revisar las métricas de los registros excluidos y activados, puede verificar si una audiencia se ha activado correctamente o no.

Por ejemplo, está activando una audiencia denominada &quot;Miembros socio en California&quot; en un destino de Amazon S3 denominado &quot;Miembros socio California diciembre&quot;. Supongamos que hay 100 perfiles en la audiencia seleccionada, pero solo 80 de 100 registros contienen atributos de ID de fidelidad y que ha definido las reglas de asignación de exportación como `loyalty.id` es obligatorio. En este caso, a nivel de audiencia, verá 80 registros activados y 20 registros excluidos.

>[!IMPORTANT]
>
>Tenga en cuenta las limitaciones actuales relacionadas con las métricas de nivel de audiencia:
>
>- La vista a nivel de audiencia está disponible actualmente para los destinos enumerados a continuación. Se ha planificado el despliegue para más destinos de flujo continuo.
>
>   - [[!DNL (API) Oracle Eloqua] conexión](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)
>   - [[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)
>   - [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)
>   - [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md)
>   - [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)
>   - [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)
>   - [[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)
>   - [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)
>   - [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)
>   - [[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)
>   - [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)
>   - [[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)
>   - [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md)
>   - [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)
>   - [[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)
>   - [[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)
>   - [[!DNL Pega CDH Realtime Audience (V1)]](../../destinations/catalog/personalization/pega.md)
>   - [[!DNL Pega CDH Realtime Audience (V2)]](../../destinations/catalog/personalization/pega-v2.md)
>   - [[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)
>   - [[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)
>   - [[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)
>   - [[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)
>   - [[!DNL Salesforce Marketing Cloud] (API)](../../destinations/catalog/email-marketing/salesforce-marketing-cloud.md)
>   - [[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)
>   - [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md)
>   - [[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)
>   - [[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)
>   - [[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)
>   - Destinos por lotes (basados en archivos)
> 
>- En el caso de los destinos por lotes, las métricas de nivel de audiencia solo se registran actualmente para ejecuciones de flujo de datos correctas. No se registran para ejecuciones de flujo de datos fallidas y registros excluidos. Para las ejecuciones de flujo de datos a destinos de flujo continuo, las métricas se capturan y se muestran para los registros activados y excluidos.

![Audiencias resaltadas en el panel de flujo de datos.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

En la vista a nivel de audiencia, las métricas se agregan en varias ejecuciones de flujo de datos dentro del intervalo de tiempo seleccionado. Si hay varias ejecuciones de flujo de datos, puede explorar en profundidad el nivel de audiencia para ver el desglose de cada ejecución de flujo de datos, filtrado por la audiencia seleccionada.
Utilice el botón de filtro ![filter](/help/images/icons/filter-add.png) para explorar en profundidad la vista de ejecuciones de flujo de datos para cada audiencia en el flujo de datos.

### Página de ejecuciones de flujo de datos {#dataflow-runs-page}

La página ejecuciones de flujo de datos muestra información sobre las ejecuciones de flujo de datos, incluido el tiempo de inicio de la ejecución del flujo de datos, el tiempo de procesamiento, los registros recibidos, los registros activados, los registros excluidos, los registros fallidos, la tasa de activación y el estado.

Cuando explora la página de ejecuciones de flujo de datos desde la [vista de nivel de audiencia](#segment-level-view), tiene la opción de filtrar las ejecuciones de flujo de datos según las siguientes opciones:

- **[!UICONTROL Dataflow runs with failed records]**: para la audiencia seleccionada, esta opción enumera todas las ejecuciones de flujo de datos que no se pudieron activar. Para inspeccionar por qué fallaron los registros en una ejecución de flujo de datos determinada, consulte la [página de detalles de ejecución de flujo de datos](#dataflow-run-details-page) para esa ejecución de flujo de datos.
- **[!UICONTROL Dataflow runs with excluded records]**: para la audiencia seleccionada, esta opción enumera todas las ejecuciones de flujo de datos en las que algunos de los registros no se activaron completamente y en las que se omitieron algunos perfiles. Para inspeccionar por qué se omitieron los registros en una determinada ejecución de flujo de datos, consulte la [página de detalles de ejecución de flujo de datos](#dataflow-run-details-page) para esa ejecución de flujo de datos.
- **[!UICONTROL Dataflow runs with activated records]**: para la audiencia seleccionada, esta opción enumera todas las ejecuciones de flujo de datos que tienen registros que se activaron correctamente.

![Botones de radio que muestran cómo filtrar las ejecuciones de flujo de datos para las audiencias.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Para ver más detalles sobre una ejecución de flujo de datos específica, seleccione el filtro ![filter](/help/images/icons/filter-add.png) junto al tiempo de inicio de la ejecución de flujo de datos para ver la página de detalles de la ejecución de flujo de datos.

![Flujo de datos ejecuta el filtro en el panel de supervisión para obtener más información para una determinada ejecución de flujo de datos.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Página Detalles de ejecución del flujo de datos {#dataflow-run-details-page}

La página de detalles de ejecución del flujo de datos, además de los detalles que se muestran en la lista de ejecuciones del flujo de datos, muestra información más específica sobre el flujo de datos:

- **[!UICONTROL Dataflow run ID]**: ID del flujo de datos.
- **[!UICONTROL IMS org ID]**: organización a la que pertenece el flujo de datos.
- **[!UICONTROL Last updated]**: hora a la que se ejecutó el flujo de datos por última vez.

La página de detalles también tiene un conmutador para cambiar entre los errores de ejecución del flujo de datos y las audiencias. Esta opción solo está disponible para ejecuciones de flujo de datos en destinos por lotes y para el destino de flujo continuo [Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md).

La vista de errores de ejecución del flujo de datos muestra una lista de los registros que han fallado y los que se han omitido. Se muestra información tanto de los registros fallidos como de los omitidos, incluido el código de error, el recuento de identidades y la descripción. De forma predeterminada, la lista muestra los registros con errores. Para mostrar los registros omitidos, seleccione la opción **[!UICONTROL Records skipped]**.

![Alternativa de identidades excluidas resaltada en la vista de supervisión](../assets/ui/monitor-destinations/identities-excluded.png)

Cuando se selecciona **[!UICONTROL Audiences]**, se muestra una lista de las audiencias que se activaron durante la ejecución del flujo de datos seleccionado. Esta pantalla incluye información a nivel de audiencia sobre los registros activados, los registros excluidos, así como el estado y la hora de la última ejecución del flujo de datos.

![Vista de audiencias en la pantalla de detalles de ejecución del flujo de datos.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Próximos pasos {#next-steps}

Al seguir esta guía, ahora sabe cómo monitorizar los flujos de datos tanto para los destinos por lotes como para los de flujo continuo, incluida toda la información relevante, como el tiempo de procesamiento, la tasa de activación y el estado. Para obtener más información sobre los flujos de datos en Experience Platform, lea la [descripción general de los flujos de datos](../home.md). Para obtener más información acerca de los destinos, lea la [descripción general de los destinos](../../destinations/home.md).