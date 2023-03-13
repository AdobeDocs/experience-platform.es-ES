---
keywords: Experience Platform;inicio;temas populares;monitorizar perfiles;monitorizar flujos de datos;flujos de datos;perfil;perfil de cliente en tiempo real;
description: El perfil del cliente en tiempo real permite ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. Este tutorial proporciona instrucciones sobre cómo puede monitorizar los flujos de datos con Perfiles mediante la interfaz de usuario del Experience Platform.
title: Monitorización de flujos de datos para perfiles en la IU
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 3%

---

# Monitorización de flujos de datos para perfiles en la IU

El perfil del cliente en tiempo real permite ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

El panel de monitorización le proporciona una representación visual de la actividad de los datos dentro del perfil, incluido el estado de los perfiles de los datos. Este tutorial proporciona instrucciones sobre cómo puede utilizar el panel de monitorización para monitorizar los perfiles de los datos mediante la interfaz de usuario del Experience Platform, lo que le permite rastrear el estado del procesamiento de perfiles.

## Primeros pasos {#getting-started}

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
- [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Panel de monitorización de perfiles {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Procesamiento de perfiles"
>abstract="La vista Procesamiento de perfil contiene información sobre los registros introducidos en el servicio de perfil, incluido el número de fragmentos de perfil creados, los fragmentos de perfil actualizados y el número total de fragmentos de perfil."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Detalles de ejecución del flujo de datos"
>abstract="La página Detalles de ejecución del flujo de datos muestra más información sobre la ejecución del flujo de datos de perfil, incluido su ID de organización y el ID de ejecución del flujo de datos."

Para acceder a **[!UICONTROL Perfiles]** panel, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. Una vez en **[!UICONTROL Monitorización]** , seleccione la **[!UICONTROL Perfiles]** Tarjeta de.

![La tarjeta Perfiles. Se muestra información sobre el número de registros recibidos, el número de fragmentos de perfil creados y actualizados y la tasa de éxito.](../assets/ui/monitor-profiles/focus-card.png)

En la página principal **[!UICONTROL Perfiles]** panel, el **[!UICONTROL Perfiles]** Esta tarjeta muestra información sobre el número total de registros recibidos, el número de fragmentos de perfil creados y actualizados, así como la tasa de éxito de los fragmentos de perfil creados y actualizados.

El propio panel contiene métricas sobre el procesamiento de perfiles. De forma predeterminada, el panel mostrará los detalles de procesamiento del perfil para los orígenes de su organización durante las últimas 24 horas.

![El panel Perfiles. Se muestra información sobre el número de registros de perfil recibidos por origen.](../assets/ui/monitor-profiles/sources.png)

El [!UICONTROL Procesamiento de perfiles] contiene información sobre los registros introducidos en [!DNL Profile], incluido el número de fragmentos de perfil creados, los fragmentos de perfil actualizados y el número total de fragmentos de perfil.

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Nombre de origen]** | Nombre de la fuente. |
| **[!UICONTROL Registros recibidos]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | El número de registros que se ingirieron, pero no en [!DNL Profile] debido a errores. |
| **[!UICONTROL Fragmentos de perfil creados]** | Número de novedades netas [!DNL Profile] fragmentos añadidos. |
| **[!UICONTROL Fragmentos de perfil actualizados]** | El número de [!DNL Profile] fragmentos actualizados. |
| **[!UICONTROL Total de fragmentos de perfil]** | Número total de registros escritos en [!DNL Profile], incluidos todos los existentes [!DNL Profile] fragmentos actualizados y nuevos [!DNL Profile] fragmentos creados. |
| **[!UICONTROL Total de flujos de datos fallidos]** | El número de ejecuciones de flujo de datos que fallaron. |

Puede seleccionar el icono de filtro ![Icono de filtro](../assets/ui/monitor-profiles/filter.png) junto al nombre de origen para ver la información de procesamiento de perfil de los flujos de datos de ese origen seleccionado.

![El icono de filtro aparece resaltado. Si selecciona este icono, puede ver los flujos de datos de la fuente seleccionada.](../assets/ui/monitor-profiles/sources-filter.png)

Como alternativa, puede seleccionar **[!UICONTROL Flujos de datos]** Haga clic en el botón de alternancia para ver los detalles de procesamiento de perfil de los flujos de datos de su organización durante las últimas 24 horas.

![El panel Perfiles. Se muestra información sobre el número de registros de perfil recibidos por flujo de datos.](../assets/ui/monitor-profiles/dataflows.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Flujo de datos]** | Nombre del flujo de datos. |
| **[!UICONTROL Conjunto de datos]** | Nombre del conjunto de datos en el que se inserta el flujo de datos. |
| **[!UICONTROL Nombre de origen]** | Nombre de la fuente a la que pertenece el flujo de datos. |
| **[!UICONTROL Registros recibidos**] | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | El número de registros que se ingirieron, pero no en [!DNL Profile] debido a errores. |
| **[!UICONTROL Fragmentos de perfil creados]** | Número de novedades netas [!DNL Profile] fragmentos añadidos. |
| **[!UICONTROL Fragmentos de perfil actualizados]** | El número de [!DNL Profile] fragmentos actualizados |
| **[!UICONTROL Total de fragmentos de perfil]** | Número total de registros escritos en [!DNL Profile], incluidos todos los existentes [!DNL Profile] fragmentos actualizados y nuevos [!DNL Profile] fragmentos creados. |
| **[!UICONTROL Total de ejecuciones de flujo fallidas]** | El número de ejecuciones de flujo de datos que fallaron. |
| **[!UICONTROL Último activo]** | La marca de tiempo de la última ejecución del flujo de datos. |

Seleccione el icono de filtro ![filter](../assets/ui/monitor-profiles/filter.png) al lado del tiempo de inicio de ejecución del flujo de datos para ver más información sobre su [!DNL Profile] ejecución del flujo de datos.

![El icono de filtro aparece resaltado. Al seleccionar este icono, puede ver los detalles sobre el flujo de datos seleccionado.](../assets/ui/monitor-profiles/dataflows-filter.png)

El [!UICONTROL Detalles de ejecución del flujo de datos] La página muestra más información sobre su [!DNL Profile] ejecución del flujo de datos, incluidos su ID de organización y el ID de ejecución del flujo de datos. Esta página también muestra el código de error y el mensaje de error correspondientes proporcionados por [!DNL Profile], si se producen errores en el proceso de ingesta.

![Se muestra un panel con información detallada sobre el flujo de datos seleccionado.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| -------| ----------- |
| **[!UICONTROL Registros recibidos]** | El número de registros recibidos del lago de datos. |
| **[!UICONTROL Error de registros]** | El número de registros que se ingirieron, pero no en [!DNL Profile] debido a errores. |
| **[!UICONTROL Fragmentos de perfil creados]** | Número de novedades netas [!DNL Profile] fragmentos añadidos. |
| **[!UICONTROL Fragmentos de perfil actualizados]** | El número de [!DNL Profile] fragmentos actualizados. |
| **[!UICONTROL Estado]** | Define el estado general de un flujo de datos. Los posibles valores de estado son: <ul><li>`Success`: indica que un flujo de datos está activo y está ingiriendo datos según la programación proporcionada.</li><li>`Failed`: indica que el proceso de activación de un flujo de datos se ha interrumpido debido a errores. </li><li>`Processing`: indica que el flujo de datos aún no está activo. Este estado suele encontrarse inmediatamente después de crear un nuevo flujo de datos.</li></ul> |
| **[!UICONTROL Inicio de ejecución de flujo de datos]** | Fecha y hora en que comenzó a ejecutarse el flujo de datos. |
| **[!UICONTROL Última actualización]** | Fecha y hora de la última actualización del flujo de datos. |
| **[!UICONTROL Resumen de errores]** | Si la ejecución del flujo de datos falló, se muestra un código de error y un resumen de por qué falló la ejecución del flujo de datos. |
| **[!UICONTROL ID de ejecución de flujo de datos]** | El ID de ejecución del flujo de datos. |
| **[!UICONTROL ID de organización de IMS]** | ID de organización al que pertenece la ejecución del flujo de datos. |

Además, puede seleccionar la opción para ver los registros que han fallado o los registros que se han omitido. La sección de errores incluye detalles sobre el código de error y el número de registros fallidos o excluidos.
