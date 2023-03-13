---
keywords: Experience Platform;inicio;temas populares;monitorizar identidades;monitorizar flujos de datos;flujos de datos;identidades;
description: El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos con identidades mediante la interfaz de usuario de Experience Platform.
title: Monitorización de flujos de datos para identidades en la IU
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---

# Monitorización de flujos de datos para identidades en la IU

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

El panel de monitorización le proporciona una representación visual de la actividad de los datos dentro de las identidades, incluido el estado de las identidades de los datos. Este tutorial proporciona instrucciones sobre cómo puede utilizar el panel de monitorización para monitorizar las identidades de los datos mediante la interfaz de usuario del Experience Platform, lo que le permite rastrear el estado del procesamiento de identidades.

## Primeros pasos {#getting-started}

- [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
- [Servicio de identidad](../../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento uniendo identidades entre dispositivos y sistemas.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Supervisión del panel de identidades {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Procesamiento de identidad"
>abstract="La vista Procesamiento de identidad contiene información sobre los registros introducidos en el servicio de identidad, incluido el número de identidades añadidas, los gráficos creados y los gráficos actualizados. Consulte la guía de definición de métricas para obtener más información sobre las métricas y los gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Detalles de ejecución del flujo de datos"
>abstract="La página Detalles de ejecución del flujo de datos muestra más información sobre la ejecución del flujo de datos de identidad, incluido su ID de organización y el ID de ejecución del flujo de datos."

Para acceder a **[!UICONTROL Identidades]** panel, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. Una vez en **[!UICONTROL Monitorización]** , seleccione la **[!UICONTROL Identidades]** Tarjeta de.

![La tarjeta Identidades. Se muestra información sobre el número de registros recibidos, el número de registros ingeridos y la tasa de éxito.](../assets/ui/monitor-identities/focus-card.png)

En la página principal **[!UICONTROL Identidades]** panel, el **[!UICONTROL Identidades]** La tarjeta muestra información sobre el número total de registros recibidos, el número de registros ingeridos y la tasa de éxito de la ingesta de registros.

El propio panel contiene métricas sobre el procesamiento de identidad. De forma predeterminada, el panel muestra los detalles de procesamiento de identidad de los orígenes de su organización durante las últimas 24 horas.

![El panel Identidades. Se muestra información sobre el número de registros recibidos por origen.](../assets/ui/monitor-identities/sources.png)

El [!UICONTROL Procesamiento de identidad] contiene información sobre los registros introducidos en [!DNL Identity Service], incluido el número de identidades añadidas, los gráficos creados y los gráficos actualizados.

Las siguientes métricas están disponibles para esta vista de panel:

| Métricas de identidad | Descripción |
| ---------------- | ----------- |
| **[!UICONTROL Registros recibidos]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | El número de registros que no se ingirieron en Platform debido a errores en los datos. |
| **[!UICONTROL Registros omitidos]** | El número de registros que se ingirieron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Registros ingeridos]** | El número de registros ingeridos en [!DNL Identity Service]. |
| **[!UICONTROL Identidades agregadas]** | El número de identificadores nuevos netos añadidos a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos creados]** | El número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| **[!UICONTROL Gráficos actualizados]** | El número de gráficos de identidad existentes actualizados con nuevos extremos. |
| **[!UICONTROL Total de flujos de datos fallidos]** | El número de ejecuciones de flujo de datos que fallaron. |

Puede seleccionar el icono de filtro ![Icono de filtro](../assets/ui/monitor-identities/filter.png) junto al nombre de origen para ver la información de procesamiento de identidad de los flujos de datos de ese origen seleccionado.

![El icono de filtro aparece resaltado. Si selecciona este icono, puede ver los flujos de datos de la fuente seleccionada.](../assets/ui/monitor-identities/sources-filter.png)

Como alternativa, puede seleccionar **[!UICONTROL Flujos de datos]** Haga clic en el botón de alternancia para ver los detalles de procesamiento de identidad de los flujos de datos de su organización durante las últimas 24 horas.

![El panel Identidades. Se muestra información sobre el número de identidades recibidas por flujo de datos.](../assets/ui/monitor-identities/dataflows.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Flujo de datos]** | Nombre del flujo de datos. |
| **[!UICONTROL Conjunto de datos]** | Nombre del conjunto de datos en el que se inserta el flujo de datos. |
| **[!UICONTROL Nombre de origen]** | Nombre de la fuente a la que pertenece el flujo de datos. |
| **[!UICONTROL Registros recibidos]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | El número de registros que no se ingirieron en Platform debido a errores en los datos. |
| **[!UICONTROL Registros omitidos]** | El número de registros que se ingirieron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Registros ingeridos]** | El número de registros ingeridos en [!DNL Identity Service]. |
| **[!UICONTROL Registros totales]** | Recuento total de todos los registros, incluidos los registros con errores, los registros omitidos, las identidades agregadas y los registros duplicados. |
| **[!UICONTROL Identidades agregadas]** | El número de identificadores nuevos netos añadidos a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos creados]** | El número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| **[!UICONTROL Gráficos actualizados]** | El número de gráficos de identidad existentes actualizados con nuevos extremos. |
| **[!UICONTROL Total de flujos de datos fallidos]** | El número de ejecuciones de flujo de datos que fallaron. |

Seleccione el icono de filtro ![filter](../assets/ui/monitor-identities/filter.png) al lado del tiempo de inicio de ejecución del flujo de datos para ver más información sobre su [!DNL Identity] ejecución del flujo de datos.

![El icono de filtro aparece resaltado. Al seleccionar este icono, puede ver los detalles sobre el flujo de datos seleccionado.](../assets/ui/monitor-identities/dataflows-filter.png)

El [!UICONTROL Detalles de ejecución del flujo de datos] La página muestra más información sobre su [!DNL Identity] ejecución del flujo de datos, incluidos su ID de organización y el ID de ejecución del flujo de datos. Esta página también muestra el código de error y el mensaje de error correspondientes proporcionados por [!DNL Identity Service], si se producen errores en el proceso de ingesta.

![Se muestra un panel con información detallada sobre el flujo de datos seleccionado.](../assets/ui/monitor-identities/dataflow-run-details.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Registros recibidos]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | El número de registros que no se ingirieron en Platform debido a errores en los datos. |
| **[!UICONTROL Registros omitidos]** | El número de registros que se ingirieron, pero no en [!DNL Identity Service] porque solo había un identificador en la fila de registros. |
| **[!UICONTROL Registros ingeridos]** | El número de registros ingeridos en [!DNL Identity Service]. |
| **[!UICONTROL Identidades agregadas]** | El número de identificadores nuevos netos añadidos a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos creados]** | El número de nuevos gráficos de identidad netos creados en [!DNL Identity Service]. |
| **[!UICONTROL Gráficos actualizados]** | El número de gráficos de identidad existentes actualizados con nuevos extremos. |
| **[!UICONTROL Estado]** | Define el estado general de un flujo de datos. Los posibles valores de estado son: <ul><li>`Success`: indica que un flujo de datos está activo y está ingiriendo datos según la programación proporcionada.</li><li>`Failed`: indica que el proceso de activación de un flujo de datos se ha interrumpido debido a errores. </li><li>`Processing`: indica que el flujo de datos aún no está activo. Este estado suele encontrarse inmediatamente después de crear un nuevo flujo de datos.</li></ul> |
| **[!UICONTROL Inicio de ejecución de flujo de datos]** | Fecha y hora en que comenzó a ejecutarse el flujo de datos. |
| **[!UICONTROL Última actualización]** | Fecha y hora de la última actualización del flujo de datos. |
| **[!UICONTROL Resumen de errores]** | Si la ejecución del flujo de datos falló, se muestra un código de error y un resumen de por qué falló la ejecución del flujo de datos. |
| **[!UICONTROL ID de ejecución de flujo de datos]** | El ID de ejecución del flujo de datos. |
| **[!UICONTROL ID de organización de IMS]** | ID de organización al que pertenece la ejecución del flujo de datos. |

Además, puede seleccionar la opción para ver los registros que han fallado o los registros que se han omitido. La sección de errores incluye detalles sobre el código de error y el número de registros fallidos o excluidos.
