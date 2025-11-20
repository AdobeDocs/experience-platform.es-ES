---
keywords: Experience Platform;inicio;temas populares;monitorizar identidades;monitorizar flujos de datos;flujos de datos;identidades;
description: El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos con identidades mediante la interfaz de usuario de Experience Platform.
title: Monitorización de flujos de datos para identidades en la IU
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 9%

---

# Monitorización de flujos de datos para identidades en la IU

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

El panel de monitorización le proporciona una representación visual de la actividad de los datos dentro de las identidades, incluido el estado de las identidades de los datos. Este tutorial proporciona instrucciones sobre cómo puede utilizar el panel de monitorización para monitorizar las identidades de los datos mediante la interfaz de usuario de Experience Platform, lo que le permite rastrear el estado del procesamiento de identidades.

## Introducción {#getting-started}

- [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Experience Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
- [Servicio de identidad](../../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Panel de control de monitorización de identidades {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Procesamiento de identidad"
>abstract="La vista Procesamiento de identidad contiene información sobre los registros ingeridos en el servicio de identidad, incluido el número de identidades añadidas, los gráficos creados y los gráficos actualizados. Consulte la guía de definición de métricas para obtener más información sobre métricas y gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Detalles de ejecución del flujo de datos"
>abstract="La página Detalles de ejecución del flujo de datos muestra más información sobre la ejecución del flujo de datos de identidad, incluido su ID de organización y el ID de ejecución del flujo de datos."

Para acceder al panel **[!UICONTROL Identities]**, seleccione **[!UICONTROL Monitoring]** en el panel de navegación izquierdo. Una vez en la página **[!UICONTROL Monitoring]**, seleccione la tarjeta **[!UICONTROL Identities]**.

![La tarjeta Identidades. Se muestra información sobre el número de registros recibidos, el número de registros ingeridos y la tasa de éxito.](../assets/ui/monitor-identities/focus-card.png)

En el panel principal **[!UICONTROL Identities]**, la tarjeta **[!UICONTROL Identities]** muestra información sobre el número total de registros recibidos, el número de registros ingeridos y la tasa de éxito de la ingesta de registros.

El propio panel contiene métricas sobre el procesamiento de identidad. De forma predeterminada, el panel muestra los detalles de procesamiento de identidad de los orígenes de su organización durante las últimas 24 horas.

![Panel de identidades. Se muestra información sobre el número de registros recibidos por origen.](../assets/ui/monitor-identities/sources.png)

La página [!UICONTROL Identity processing] contiene información sobre los registros ingeridos en [!DNL Identity Service], incluyendo el número de identidades agregadas, gráficos creados y gráficos actualizados.

Las siguientes métricas están disponibles para esta vista de panel:

| Métricas de identidad | Descripción |
| ---------------- | ----------- |
| **[!UICONTROL Records received]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Records failed]** | El número de registros que no se ingirieron en Experience Platform debido a errores en los datos. |
| **[!UICONTROL Records skipped]** | El número de registros que se ingerieron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Records ingested]** | El número de registros ingeridos en [!DNL Identity Service]. |
| **[!UICONTROL Identities added]** | Número de identificadores nuevos de red agregados a [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Número de nuevos gráficos de identidad creados en [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | El número de gráficos de identidad existentes actualizados con nuevos extremos. |
| **[!UICONTROL Total failed dataflows]** | El número de ejecuciones de flujo de datos que fallaron. |

Puede seleccionar el icono de filtro ![Icono de filtro](/help/images/icons/filter.png) junto al nombre de origen para ver la información de procesamiento de identidad de los flujos de datos de ese origen seleccionado.

![El icono de filtro está resaltado. Si selecciona este icono, podrá ver los flujos de datos del origen seleccionado.](../assets/ui/monitor-identities/sources-filter.png)

También puede seleccionar **[!UICONTROL Dataflows]** en el conmutador para ver los detalles de procesamiento de identidad de los flujos de datos de su organización durante las últimas 24 horas.

![Panel de identidades. Se muestra información sobre el número de identidades recibidas por flujo de datos.](../assets/ui/monitor-identities/dataflows.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | Nombre del flujo de datos. |
| **[!UICONTROL Dataset]** | Nombre del conjunto de datos en el que se inserta el flujo de datos. |
| **[!UICONTROL Source name]** | Nombre de la fuente a la que pertenece el flujo de datos. |
| **[!UICONTROL Records received]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Records failed]** | El número de registros que no se ingirieron en Experience Platform debido a errores en los datos. |
| **[!UICONTROL Records skipped]** | El número de registros que se ingerieron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Records ingested]** | El número de registros ingeridos en [!DNL Identity Service]. |
| **[!UICONTROL Total records]** | Recuento total de todos los registros, incluidos los registros con errores, los registros omitidos, las identidades agregadas y los registros duplicados. |
| **[!UICONTROL Identities added]** | Número de identificadores nuevos de red agregados a [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Número de nuevos gráficos de identidad creados en [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | El número de gráficos de identidad existentes actualizados con nuevos extremos. |
| **[!UICONTROL Total failed dataflows]** | El número de ejecuciones de flujo de datos que fallaron. |

Seleccione el icono de filtro ![filter](/help/images/icons/filter.png) al lado del tiempo de inicio de la ejecución del flujo de datos para ver más información sobre la ejecución del flujo de datos [!DNL Identity].

![El icono de filtro está resaltado. Si selecciona este icono, podrá ver los detalles sobre el flujo de datos seleccionado.](../assets/ui/monitor-identities/dataflows-filter.png)

La página [!UICONTROL Dataflow run details] muestra más información sobre la ejecución del flujo de datos [!DNL Identity], incluido su ID de organización y el ID de ejecución del flujo de datos. Esta página también muestra el código de error y el mensaje de error correspondientes proporcionados por [!DNL Identity Service], en caso de que se produzca algún error en el proceso de ingesta.

![Se muestra un panel con información detallada sobre el flujo de datos seleccionado.](../assets/ui/monitor-identities/dataflow-run-details.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Records received]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Records failed]** | El número de registros que no se ingirieron en Experience Platform debido a errores en los datos. |
| **[!UICONTROL Records skipped]** | El número de registros que se ingerieron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Records ingested]** | El número de registros ingeridos en [!DNL Identity Service]. |
| **[!UICONTROL Identities added]** | Número de identificadores nuevos de red agregados a [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Número de nuevos gráficos de identidad creados en [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | El número de gráficos de identidad existentes actualizados con nuevos extremos. |
| **[!UICONTROL Status]** | Define el estado general de un flujo de datos. Los posibles valores de estado son: <ul><li>`Success`: indica que un flujo de datos está activo y está ingiriendo datos según la programación proporcionada.</li><li>`Failed`: indica que el proceso de activación de un flujo de datos se ha interrumpido debido a errores. </li><li>`Processing`: indica que el flujo de datos aún no está activo. Este estado suele encontrarse inmediatamente después de crear un nuevo flujo de datos.</li></ul> |
| **[!UICONTROL Dataflow run start]** | Fecha y hora en que comenzó a ejecutarse el flujo de datos. |
| **[!UICONTROL Last updated]** | Fecha y hora de la última actualización del flujo de datos. |
| **[!UICONTROL Error summary]** | Si la ejecución del flujo de datos falló, se muestra un código de error y un resumen de por qué falló la ejecución del flujo de datos. |
| **[!UICONTROL Dataflow run ID]** | El ID de ejecución del flujo de datos. |
| **[!UICONTROL IMS org ID]** | ID de organización al que pertenece la ejecución del flujo de datos. |

Además, puede seleccionar la opción para ver los registros que han fallado o los registros que se han omitido. La sección de errores incluye detalles sobre el código de error y el número de registros fallidos o excluidos.
