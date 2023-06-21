---
title: Horarios de consulta
description: Obtenga información sobre cómo automatizar las ejecuciones de consultas programadas, eliminar o deshabilitar una programación de consultas y utilizar las opciones de programación disponibles a través de la interfaz de usuario de Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: a0f826a2e5fcdfc2f9e08221f30ba01470c9b3be
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# Programaciones de consultas

Puede automatizar las ejecuciones de consultas creando programaciones de consultas. Las consultas programadas se ejecutan en una cadencia personalizada para administrar los datos en función de la frecuencia, la fecha y la hora. También puede elegir un conjunto de datos de salida para los resultados si es necesario. Las consultas que se han guardado como plantilla se pueden programar desde el Editor de consultas.

>[!IMPORTANT]
>
>A continuación se muestra una lista de limitaciones para las consultas programadas al utilizar el Editor de consultas. No se aplican al [!DNL Query Service] API:<br/>Solo puede agregar una programación a una consulta que ya se ha creado, guardado y ejecutado.<br/>Usted **no puede** añada una programación a una consulta parametrizada.<br/>Consultas programadas **no puede** contiene un bloque anónimo.

Todas las consultas programadas se agregan a la lista de la [!UICONTROL Consultas programadas] pestaña. Desde ese espacio de trabajo, puede monitorizar el estado de todos los trabajos de consulta programados a través de la interfaz de usuario. En el [!UICONTROL Consultas programadas] pestaña puede encontrar información importante sobre las ejecuciones de consultas y suscribirse a alertas. La información disponible incluye el estado, los detalles de la programación y los mensajes/códigos de error en caso de que falle una ejecución. Consulte la [Documento de supervisión de consultas programadas](./monitor-queries.md) para obtener más información.

## Creación de programaciones de consultas {#create-schedule}

Para añadir una programación a una consulta, seleccione una plantilla de consulta de la [!UICONTROL Plantillas] o la pestaña [!UICONTROL Consultas programadas] para desplazarse al Editor de consultas.

Para obtener información sobre cómo añadir programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).

Cuando se accede a una consulta guardada desde el Editor de consultas, la variable [!UICONTROL Horarios] aparece debajo del nombre de la consulta. Seleccionar **[!UICONTROL Horarios]**.

![Editor de consultas con la ficha Programaciones resaltada.](../images/ui/query-schedules/schedules-tab.png)

Aparecerá el espacio de trabajo programaciones. Seleccionar **[!UICONTROL Agregar programación]** para crear una programación.

![Espacio de trabajo de programación del Editor de consultas con la opción Agregar programación resaltada.](../images/ui/query-schedules/add-schedule.png)

Aparecerá la página de detalles de la programación. En esta página, puede elegir la frecuencia de la consulta programada, la fecha de inicio y finalización, el día de la semana en que se ejecutará la consulta programada, así como a qué conjunto de datos exportar la consulta.

![Se ha resaltado el panel Detalles de programación.](../images/ui/query-schedules/schedule-details.png)

Puede elegir las siguientes opciones para **[!UICONTROL Frecuencia]**:

- **[!UICONTROL Por hora]**: la consulta programada se ejecutará cada hora para el período de fecha seleccionado.
- **[!UICONTROL Diario]**: la consulta programada se ejecutará cada X días a la hora y en el periodo de fecha seleccionados. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.
- **[!UICONTROL Semanalmente]**: la consulta seleccionada se ejecutará los días de la semana, la hora y el período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.
- **[!UICONTROL Mensual]**: la consulta seleccionada se ejecutará cada mes en el día, la hora y el período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.
- **[!UICONTROL Anual]**: la consulta seleccionada se ejecutará cada año en el día, el mes, la hora y el período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.

Para el conjunto de datos de salida, tiene la opción de utilizar un conjunto de datos existente o crear uno nuevo.

>[!IMPORTANT]
>
> Dado que está utilizando un conjunto de datos existente o está creando uno nuevo, puede hacer lo siguiente **no** debe incluir lo siguiente `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de la consulta, ya que los conjuntos de datos ya están configurados. Incluyendo cualquiera `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de las consultas programadas, producirá un error.

Si no tiene acceso a las consultas parametrizadas, continúe con el [eliminar o deshabilitar una programación](#delete-schedule) sección.

### Definir parámetros para una consulta parametrizada programada {#set-parameters}

>[!IMPORTANT]
>
>La función de IU de consulta parametrizada está disponible actualmente en un **solo versión limitada** y no está disponible para todos los clientes.

Si está creando una consulta programada para una consulta parametrizada, debe establecer los valores de parámetro para estas ejecuciones de consulta.

![La sección Detalles del programa del flujo de trabajo de creación del programa con la sección Parámetros de consulta resaltada.](../images/ui/query-schedules/scheduled-query-parameter.png)

Después de confirmar todos estos detalles, seleccione **[!UICONTROL Guardar]** para crear una programación. Volverá al espacio de trabajo de programaciones que muestra los detalles de la programación recién creada, incluido el ID de programación, la propia programación y el conjunto de datos de salida de la programación. Puede utilizar el ID de programación para buscar más información sobre las ejecuciones de la propia consulta programada. Para obtener más información, lea la [guía de extremos de ejecución de consulta programada](../api/runs-scheduled-queries.md).

![Espacio de trabajo de programaciones con la programación recién creada resaltada.](../images/ui/query-schedules/schedules-workspace.png)

## Eliminar o deshabilitar una programación {#delete-schedule}

Puede eliminar o deshabilitar una programación del espacio de trabajo de programaciones. Debe seleccionar una plantilla de consulta de la [!UICONTROL Plantillas] o la pestaña [!UICONTROL Consultas programadas] para ir al Editor de consultas y seleccionar **[!UICONTROL Programación]** para acceder al espacio de trabajo programaciones.

Seleccione una programación de las filas de programaciones disponibles. Puede utilizar la opción para deshabilitar o habilitar la consulta programada.

>[!IMPORTANT]
>
>Debe deshabilitar la programación para poder eliminar una programación de una consulta.

Seleccionar **[!UICONTROL Eliminar una programación]** para eliminar la programación deshabilitada.

![Espacio de trabajo de programaciones con las opciones Deshabilitar programación y Eliminar programación resaltadas.](../images/ui/query-schedules/delete-schedule.png)
