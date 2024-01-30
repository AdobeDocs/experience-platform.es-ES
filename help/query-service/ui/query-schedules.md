---
title: Horarios de consulta
description: Obtenga información sobre cómo automatizar las ejecuciones de consultas programadas, eliminar o deshabilitar una programación de consultas y utilizar las opciones de programación disponibles a través de la interfaz de usuario de Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 7d2027bf315ae6e354c906e4aabf6371a92e4148
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Programaciones de consultas

Puede automatizar las ejecuciones de consultas creando programaciones de consultas. Las consultas programadas se ejecutan en una cadencia personalizada para administrar los datos en función de la frecuencia, la fecha y la hora. También puede elegir un conjunto de datos de salida para los resultados si es necesario. Las consultas que se han guardado como plantilla se pueden programar desde el Editor de consultas.

>[!IMPORTANT]
>
>Solo puede agregar una programación a una consulta que ya se ha creado, guardado y ejecutado.

Todas las consultas programadas se agregan a la lista de la [!UICONTROL Consultas programadas] pestaña. Desde ese espacio de trabajo, puede monitorizar el estado de todos los trabajos de consulta programados a través de la interfaz de usuario. En el [!UICONTROL Consultas programadas] pestaña puede encontrar información importante sobre las ejecuciones de consultas y suscribirse a alertas. La información disponible incluye el estado, los detalles de la programación y los mensajes/códigos de error en caso de que falle una ejecución. Consulte la [Documento de supervisión de consultas programadas](./monitor-queries.md) para obtener más información.

Este flujo de trabajo cubre el proceso de programación en la interfaz de usuario del servicio de consultas. Para obtener información sobre cómo añadir programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).

## Creación de una programación de consultas {#create-schedule}

Para programar una consulta, seleccione una plantilla de consulta de la [!UICONTROL Plantillas] o la pestaña [!UICONTROL Plantilla] de la columna [!UICONTROL Consultas programadas] pestaña. Al seleccionar el nombre de la plantilla, accederá al Editor de consultas.

Si accede a una consulta guardada desde el Editor de consultas, puede crear una programación para la consulta o ver la programación de la consulta desde el panel de detalles.

>[!TIP]
>
>Seleccionar **[!UICONTROL Ver programación]** para desplazarse al espacio de trabajo programaciones y ver si alguna consulta programada se ejecuta de un vistazo.

![El editor de consultas con [!UICONTROL Ver programación] y [!UICONTROL Agregar programación] resaltado.](../images/ui/query-schedules/view-add-schedule.png)

Seleccionar **[!UICONTROL Agregar programación]** para ir al [página de detalles de programación](#schedule-details).

Como alternativa, seleccione la **[!UICONTROL Horarios]** debajo del nombre de la consulta.

![Editor de consultas con la ficha Programaciones resaltada.](../images/ui/query-schedules/schedules-tab.png)

Aparecerá el espacio de trabajo programaciones. Seleccionar **[!UICONTROL Agregar programación]** para crear una programación.

![Espacio de trabajo de programación del Editor de consultas con la opción Agregar programación resaltada.](../images/ui/query-schedules/add-schedule.png)

### Editar los detalles de programación {#schedule-details}

Aparecerá la página de detalles de la programación. En esta página, puede elegir la frecuencia de la consulta programada, la fecha de inicio y finalización, el día de la semana en que se ejecutará la consulta programada, así como a qué conjunto de datos exportar la consulta.

![Se ha resaltado el panel Detalles de programación.](../images/ui/query-schedules/schedule-details.png)

Puede elegir las siguientes opciones para **[!UICONTROL Frecuencia]**:

- **[!UICONTROL Por hora]**: la consulta programada se ejecutará cada hora para el período de fecha seleccionado.
- **[!UICONTROL Diario]**: la consulta programada se ejecutará cada X días a la hora y en el periodo de fecha seleccionados. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.
- **[!UICONTROL Semanalmente]**: la consulta seleccionada se ejecutará los días de la semana, la hora y el período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.
- **[!UICONTROL Mensual]**: la consulta seleccionada se ejecutará cada mes en el día, la hora y el período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.
- **[!UICONTROL Anual]**: la consulta seleccionada se ejecutará cada año en el día, el mes, la hora y el período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC**, y no su zona horaria local.

Para el conjunto de datos de salida, tiene la opción de utilizar Anexar a un conjunto de datos existente o crear y anexar a un nuevo conjunto de datos. La segunda opción significa que si ejecuta una consulta por primera vez y crea un conjunto de datos, cualquier ejecución posterior seguirá insertando datos en ese conjunto de datos.

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

## Ver ejecuciones de consulta programadas {#scheduled-query-runs}

Para ver una lista de las ejecuciones programadas de una plantilla de consulta, vaya al [!UICONTROL Consultas programadas] y seleccione un nombre de plantilla de la lista disponible.

![La pestaña Consultas programadas con una plantilla con nombre resaltada.](../images/ui/query-schedules/view-scheduled-runs.png)

Aparecerá la lista de ejecuciones de consulta para esa consulta programada.

![La sección de detalles del espacio de trabajo Consultas programadas con una lista de ejecuciones de consulta resaltada para una consulta programada.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Consulte la [guía de monitorización de consultas programadas](./monitor-queries.md#inline-actions) para obtener información completa sobre cómo monitorizar el estado de todos los trabajos de consulta a través de la interfaz de usuario.

## Eliminar o deshabilitar una programación {#delete-schedule}

Puede eliminar o deshabilitar una programación desde el espacio de trabajo de programaciones de una consulta concreta o desde el [!UICONTROL Consultas programadas] espacio de trabajo que enumera todas las consultas programadas.

Para acceder a [!UICONTROL Horarios] de la consulta elegida, debe seleccionar el nombre de una plantilla de consulta de la [!UICONTROL Plantillas] o la pestaña [!UICONTROL Consultas programadas] pestaña. Se desplaza al Editor de consultas de esa consulta. En el Editor de consultas, seleccione **[!UICONTROL Horarios]** para acceder al espacio de trabajo programaciones.

Seleccione una programación de las filas de programaciones disponibles. Puede utilizar la opción para deshabilitar o habilitar la consulta programada.

>[!IMPORTANT]
>
>Debe deshabilitar la programación para poder eliminar una programación de una consulta.

Seleccionar **[!UICONTROL Eliminar una programación]** para eliminar la programación deshabilitada.

![Espacio de trabajo de programaciones con las opciones Deshabilitar programación y Eliminar programación resaltadas.](../images/ui/query-schedules/delete-schedule.png)

Alternativamente, la variable [!UICONTROL Consultas programadas] ofrece una colección de acciones en línea para cada consulta programada. Las acciones en línea disponibles incluyen [!UICONTROL Desactivar programación] o [!UICONTROL Habilitar programación], [!UICONTROL Eliminar programación], y [!UICONTROL Suscribirse] a alertas para la consulta programada. Para obtener instrucciones completas sobre cómo eliminar o deshabilitar una consulta programada a través de la pestaña Consultas programadas, consulte la [guía de monitorización de consultas programadas](./monitor-queries.md#inline-actions).
