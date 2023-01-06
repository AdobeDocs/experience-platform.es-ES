---
keywords: Experience Platform;inicio;temas populares;monitorizar identidades;monitorizar flujos de datos;flujos de datos;identidades;
description: El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos con identidades mediante la interfaz de usuario del Experience Platform.
title: Monitorizar flujos de datos para identidades en la interfaz de usuario
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---

# Monitorización de flujos de datos para identidades en la interfaz de usuario

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

El panel de monitorización proporciona una representación visual de la actividad de los datos dentro de las identidades, incluido el estado de las identidades de los datos. Este tutorial proporciona instrucciones sobre cómo utilizar el panel de monitorización para monitorizar las identidades de los datos mediante la interfaz de usuario del Experience Platform, lo que le permite realizar un seguimiento del estado del procesamiento de identidades.

## Primeros pasos {#getting-started}

- [Flujos de datos](../home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile]y [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración de frecuencia de los flujos de datos seleccionados.
- [Servicio de identidad](../../identity-service/home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Panel de identidades de monitorización {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Procesamiento de identidad"
>abstract="La vista de procesamiento de identidad contiene información sobre los registros ingestados al servicio de identidad, incluido el número de identidades añadidas, los gráficos creados y los gráficos actualizados. Consulte la guía de definición de métricas para obtener más información sobre métricas y gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Detalles de ejecución de flujo de datos"
>abstract="La página de detalles de ejecución del flujo de datos muestra más información sobre la ejecución del flujo de datos de identidad, incluido su ID de organización y el ID de ejecución del flujo de datos."

Para acceder a la **[!UICONTROL Identidades]** tablero, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. Una vez en el **[!UICONTROL Monitorización]** seleccione **[!UICONTROL Identidades]** tarjeta.

![La tarjeta Identidades . Información sobre el número de registros recibidos, el número de registros ingeridos y la tasa de éxito.](../assets/ui/monitor-identities/focus-card.png)

En el **[!UICONTROL Identidades]** tablero, **[!UICONTROL Identidades]** la tarjeta muestra información sobre el número total de registros recibidos, el número de registros introducidos, así como la tasa de éxito de la ingesta de registros.

El propio tablero contiene métricas sobre el procesamiento de identidad. De forma predeterminada, el panel muestra los detalles de procesamiento de identidad de las fuentes de su organización durante las últimas 24 horas.

![El panel Identidades . Se muestra información sobre el número de registros recibidos por fuente.](../assets/ui/monitor-identities/sources.png)

La variable [!UICONTROL Procesamiento de identidad] La página contiene información sobre los registros ingestados en [!DNL Identity Service], incluido el número de identidades añadidas, los gráficos creados y los gráficos actualizados.

Las siguientes métricas están disponibles para esta vista de tablero:

| Métricas de identidad | Descripción |
| ---------------- | ----------- |
| **[!UICONTROL Registros recibidos]** | Número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | Número de registros que no se incorporaron en Platform debido a errores en los datos. |
| **[!UICONTROL Registros omitidos]** | El número de registros introducidos, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Registros ingestados]** | El número de registros ingestados en [!DNL Identity Service]. |
| **[!UICONTROL Identidades agregadas]** | El número de identificadores nuevos netos agregados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos creados]** | El número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| **[!UICONTROL Gráficos actualizados]** | Número de gráficos de identidad existentes actualizados con bordes nuevos. |
| **[!UICONTROL Total de flujos de datos fallidos]** | Número de ejecuciones de flujo de datos que han fallado. |

Puede seleccionar el icono de filtro ![Icono de filtro](../assets/ui/monitor-identities/filter.png) junto al nombre del origen para ver la información de procesamiento de identidad para los flujos de datos de ese origen seleccionado.

![El icono de filtro se resalta. La selección de este icono permite ver los flujos de datos de la fuente seleccionada.](../assets/ui/monitor-identities/sources-filter.png)

También puede seleccionar **[!UICONTROL Flujos de datos]** del botón de alternancia para ver los detalles de procesamiento de identidad de los flujos de datos de su organización durante las últimas 24 horas.

![El panel Identidades . Se muestra información sobre el número de identidades recibidas por flujo de datos.](../assets/ui/monitor-identities/dataflows.png)

Las siguientes métricas están disponibles para esta vista de tablero:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Flujo de datos]** | Nombre del flujo de datos. |
| **[!UICONTROL Conjunto de datos]** | Nombre del conjunto de datos al que se inserta el flujo de datos. |
| **[!UICONTROL Nombre de origen]** | Nombre del origen al que pertenece el flujo de datos. |
| **[!UICONTROL Registros recibidos]** | Número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | Número de registros que no se incorporaron en Platform debido a errores en los datos. |
| **[!UICONTROL Registros omitidos]** | El número de registros introducidos, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Registros ingestados]** | El número de registros ingestados en [!DNL Identity Service]. |
| **[!UICONTROL Registros totales]** | Recuento total de todos los registros, incluidos los registros con errores, los registros omitidos, las identidades agregadas y los registros duplicados. |
| **[!UICONTROL Identidades agregadas]** | El número de identificadores nuevos netos agregados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos creados]** | El número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| **[!UICONTROL Gráficos actualizados]** | Número de gráficos de identidad existentes actualizados con bordes nuevos. |
| **[!UICONTROL Total de flujos de datos fallidos]** | Número de ejecuciones de flujo de datos que han fallado. |

Seleccione el icono de filtro ![filter](../assets/ui/monitor-identities/filter.png) al lado del tiempo de inicio de ejecución del flujo de datos para ver más información sobre su [!DNL Identity] ejecute dataflow.

![El icono de filtro se resalta. Si selecciona este icono, podrá ver los detalles del flujo de datos seleccionado.](../assets/ui/monitor-identities/dataflows-filter.png)

La variable [!UICONTROL Detalles de ejecución de flujo de datos] la página muestra más información sobre [!DNL Identity] ejecución del flujo de datos, incluido su ID de organización y el ID de ejecución del flujo de datos. Esta página también muestra el código de error y el mensaje de error correspondientes proporcionados por [!DNL Identity Service], si se produce algún error en el proceso de ingesta.

![Se muestra un tablero que muestra información detallada sobre el flujo de datos seleccionado.](../assets/ui/monitor-identities/dataflow-run-details.png)

Las siguientes métricas están disponibles para esta vista de tablero:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Registros recibidos]** | Número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | Número de registros que no se incorporaron en Platform debido a errores en los datos. |
| **[!UICONTROL Registros omitidos]** | El número de registros introducidos, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Registros ingestados]** | El número de registros ingestados en [!DNL Identity Service]. |
| **[!UICONTROL Identidades agregadas]** | El número de identificadores nuevos netos agregados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos creados]** | El número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| **[!UICONTROL Gráficos actualizados]** | Número de gráficos de identidad existentes actualizados con bordes nuevos. |
| **[!UICONTROL Estado]** | Define el estado general de un flujo de datos. Los valores de estado posibles son: <ul><li>`Success`: Indica que un flujo de datos está activo y que está incorporando datos según la programación proporcionada.</li><li>`Failed`: Indica que el proceso de activación de un flujo de datos se ha interrumpido debido a errores. </li><li>`Processing`: Indica que el flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos.</li></ul> |
| **[!UICONTROL Inicio de la ejecución del flujo de datos]** | Fecha y hora en que comenzó a ejecutarse el flujo de datos. |
| **[!UICONTROL Última actualización]** | Fecha y hora de la última actualización del flujo de datos. |
| **[!UICONTROL Resumen de errores]** | Si se produce un error en la ejecución del flujo de datos, se muestra un código de error y un resumen de por qué ha fallado la ejecución del flujo de datos. |
| **[!UICONTROL ID de ejecución de flujo de datos]** | El ID de la ejecución del flujo de datos. |
| **[!UICONTROL ID de organización de IMS]** | El ID de organización al que pertenece la ejecución de flujo de datos. |

Además, puede seleccionar la opción para ver los registros en los que se han producido errores o los registros omitidos. La sección de errores incluye detalles sobre el código de error y el número de registros fallidos o excluidos.
