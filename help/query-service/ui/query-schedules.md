---
title: Programaciones de consultas
description: Obtenga información sobre cómo automatizar las ejecuciones de consultas programadas, eliminar o deshabilitar una programación de consultas y utilizar las opciones de programación disponibles a través de la interfaz de usuario de Adobe Experience Platform.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Programaciones de consultas

Puede automatizar las ejecuciones de consultas mediante la creación de programaciones de consultas. Las consultas programadas se ejecutan en una cadencia personalizada para administrar los datos en función de la frecuencia, la fecha y la hora. También puede elegir un conjunto de datos de salida para sus resultados si es necesario. Las consultas que se han guardado como plantilla se pueden programar desde el Editor de consultas.

>[!IMPORTANT]
>
>A continuación se muestra una lista de limitaciones para las consultas programadas al utilizar el Editor de consultas. No se aplican al [!DNL Query Service] API:<br/>Solo puede añadir una programación a una consulta que ya se haya creado, guardado y ejecutado.<br/>You **cannot** agregue una programación a una consulta parametrizada.<br/>Consultas programadas **cannot** contiene un bloque anónimo.

Todas las consultas programadas se agregan a la lista en la [!UICONTROL Consultas programadas] pestaña . Desde ese espacio de trabajo, puede supervisar el estado de todos los trabajos de consulta programados a través de la interfaz de usuario. En el [!UICONTROL Consultas programadas] puede encontrar información importante sobre las ejecuciones de consultas y suscribirse a alertas. La información disponible incluye el estado, los detalles de la programación y los mensajes/códigos de error en caso de que falle una ejecución. Consulte la [Monitorizar documento de consultas programadas](./monitor-queries.md) para obtener más información.

## Creación de programaciones de consultas {#create-schedule}

Para agregar una programación a una consulta, seleccione una plantilla de consulta desde la [!UICONTROL Plantillas] o [!UICONTROL Consultas programadas] para ir al Editor de consultas.

Para aprender a añadir programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).

Cuando se accede a una consulta guardada desde el Editor de consultas, la variable [!UICONTROL Programaciones] aparece debajo del nombre de la consulta. Select **[!UICONTROL Programaciones]**.

![El Editor de consultas con la ficha Programas resaltada.](../images/ui/query-schedules/schedules-tab.png)

Aparecerá el espacio de trabajo de programaciones. Select **[!UICONTROL Agregar programación]** para crear una programación.

![Espacio de trabajo Programar del Editor de consultas con la opción Agregar programación resaltada.](../images/ui/query-schedules/add-schedule.png)

Aparecerá la página de detalles de la programación. En esta página, puede elegir la frecuencia de la consulta programada, la fecha de inicio y finalización, el día de la semana en que se ejecutará la consulta programada, así como el conjunto de datos al que exportar la consulta.

![El panel Detalles del programa está resaltado.](../images/ui/query-schedules/schedule-details.png)

Puede elegir las siguientes opciones para **[!UICONTROL Frecuencia]**:

- **[!UICONTROL Por hora]**: La consulta programada se ejecutará cada hora para el período de fecha seleccionado.
- **[!UICONTROL Diario]**: La consulta programada se ejecutará cada X días a la hora y el periodo de fecha seleccionados. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.
- **[!UICONTROL Semanal]**: La consulta seleccionada se ejecutará en los días de la semana, la hora y el período de fecha seleccionado. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.
- **[!UICONTROL Mensual]**: La consulta seleccionada se ejecutará todos los meses del día, la hora y el período de fecha seleccionado. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.
- **[!UICONTROL Anual]**: La consulta seleccionada se ejecutará cada año en el día, mes, hora y período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.

Para el conjunto de datos de salida, tiene la opción de usar un conjunto de datos existente o crear un nuevo conjunto de datos.

>[!IMPORTANT]
>
> Como está utilizando un conjunto de datos existente o creando uno nuevo, sí lo hace **not** debe incluir: `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de la consulta, ya que los conjuntos de datos ya están establecidos. Incluyendo: `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de las consultas programadas, se producirá un error.

Después de confirmar todos estos detalles, seleccione **[!UICONTROL Guardar]** para crear una programación. Volverá al espacio de trabajo de programaciones , que muestra detalles de la programación recién creada, incluido el ID de programación, la propia programación y el conjunto de datos de salida de la programación. Puede utilizar el ID de programación para buscar más información sobre las ejecuciones de la propia consulta programada. Para obtener más información, lea la [guía de extremos de ejecución de consultas programadas](../api/runs-scheduled-queries.md).

![El espacio de trabajo de programaciones con la programación recién creada resaltada.](../images/ui/query-schedules/schedules-workspace.png)

## Eliminar o deshabilitar una programación {#delete-schedule}

Puede eliminar o desactivar una programación del espacio de trabajo de programaciones. Debe seleccionar una plantilla de consulta desde la [!UICONTROL Plantillas] o [!UICONTROL Consultas programadas] para ir al Editor de consultas y seleccionar **[!UICONTROL Programación]** para acceder al espacio de trabajo de programaciones.

Seleccione una programación de las filas de programaciones disponibles. Puede utilizar el botón de alternancia para deshabilitar o habilitar la consulta programada.

>[!IMPORTANT]
>
>Debe desactivar la programación para poder eliminar una programación de una consulta.

Select **[!UICONTROL Eliminar una programación]** para eliminar la programación deshabilitada.

![El espacio de trabajo de programaciones con Desactivar programación y Eliminar programación resaltado.](../images/ui/query-schedules/delete-schedule.png)


