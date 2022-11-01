---
title: Supervisar consultas
description: Obtenga información sobre cómo monitorizar consultas a través de la interfaz de usuario del servicio de consulta.
source-git-commit: 283c6ba323a327b0c525343a96a45a2412baa67b
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 1%

---

# Monitorizar consultas (versión limitada)

>[!IMPORTANT]
>
>Actualmente, esta función es una versión limitada y solo está disponible para un pequeño número de clientes.

Adobe Experience Platform proporciona una visibilidad mejorada para el estado de todos los trabajos de consulta a través de la interfaz de usuario. De [!UICONTROL Consultas programadas] ahora puede encontrar información importante sobre las ejecuciones de consultas que incluye el estado, los detalles de la programación y los mensajes/códigos de error si fallan. También puede suscribirse a alertas para consultas en función de su estado a través de la interfaz de usuario para cualquiera de estas consultas mediante [!UICONTROL Consultas programadas] pestaña .

## [!UICONTROL Consultas programadas]

La variable [!UICONTROL Consultas programadas] proporciona una descripción general de las consultas ejecutadas y programadas. El espacio de trabajo contiene todas las consultas de CTAS e ITAS que están programadas para ejecutarse o que se han ejecutado al menos una vez. Se pueden encontrar detalles de ejecución para todas las consultas programadas, así como códigos de error y mensajes para consultas fallidas.

Para ir a la [!UICONTROL Consultas programadas] , seleccione **[!UICONTROL Consultas]** desde la barra de navegación izquierda seguida de **[!UICONTROL Consultas programadas]**

![La ficha Consultas programadas del espacio de trabajo Consultas .](./images/monitor-queries/scheduled-queries.png)

La tabla siguiente describe cada columna disponible.

>[!NOTE]
>
>El icono de suscripciones de alerta está contenido en cada fila de una columna sin título. Consulte la [suscripciones de alerta](#alert-subscription) para obtener más información.

| Columna | Descripción |
|---|---|
| Nombre | El campo de nombre es el nombre de la plantilla o los primeros caracteres de la consulta SQL. Cualquier consulta creada a través de la interfaz de usuario con el Editor de consultas recibe un nombre desde el principio. Si la consulta se creó mediante la API, el nombre de la consulta es un fragmento del SQL inicial utilizado para crear la consulta. |
| Plantilla | El nombre de plantilla de la consulta. Seleccione un nombre de plantilla para ir al Editor de consultas. La plantilla de consulta se muestra en el Editor de consultas para mayor comodidad. Si no hay ningún nombre de plantilla, la fila se marca con un guión y no se puede redirigir al Editor de consultas para ver la consulta. |
| SQL | Un fragmento de la consulta SQL. |
| Frecuencia de ejecución | Esta es la cadencia en la que se configura la ejecución de la consulta. Los valores disponibles son `Run once` y `Scheduled`. Las consultas se pueden filtrar según su frecuencia de ejecución. |
| Creado por | Nombre del usuario que creó la consulta. |
| Creado | Marca de tiempo cuando se creó la consulta, en formato UTC. |
| Marca de tiempo de última ejecución | Marca de tiempo más reciente cuando se ejecutó la consulta. Esta columna resalta si una consulta se ha ejecutado según su programación actual. |
| Último estado de ejecución | Estado de la ejecución de consulta más reciente. Los tres valores de estado son: `successful` `failed` o `in progress`. |

>[!TIP]
>
>Si va al Editor de consultas, puede seleccionar **[!UICONTROL Consultas]** para volver a la [!UICONTROL Plantillas] pestaña .

### Personalización de la configuración de tabla para consultas programadas

Puede ajustar las columnas en la [!UICONTROL Consultas programadas] a sus necesidades. Seleccione el icono de configuración (![Un icono de configuración.](./images/monitor-queries/settings-icon.png)) para abrir el [!UICONTROL Personalizar tabla] cuadro de diálogo configuración y editar las columnas disponibles.

![El icono Personalizar configuración de tabla .](./images/monitor-queries/customze-table-settings-icon.png)

Active las casillas de verificación correspondientes para eliminar o agregar una columna de tabla. A continuación, seleccione **[!UICONTROL Aplicar]** para confirmar las opciones.

>[!NOTE]
>
>Cualquier consulta creada a través de la interfaz de usuario se convierte en una plantilla con nombre como parte del proceso de creación. El nombre de la plantilla se ve en la columna plantilla . Si la consulta se creó a través de la API, la columna de la plantilla está en blanco.

![El cuadro de diálogo Personalizar configuración de tabla.](./images/monitor-queries/customize-table-dialog.png)

### Suscripción a alertas {#alert-subscription}

Puede suscribirse a las alertas desde el [!UICONTROL Consultas programadas] pestaña . Seleccione el icono de notificación de alerta (![Un icono de alerta.](./images/monitor-queries/alerts-icon.png)) junto al nombre de la consulta para abrir el [!UICONTROL Alertas] diálogo. La variable [!UICONTROL Alertas] se suscribe a las notificaciones de la interfaz de usuario y a las alertas de correo electrónico. Las alertas se basan en el estado de la consulta. Hay tres opciones disponibles: `start`, `success`y `failure`. Marque las casillas adecuadas y seleccione **[!UICONTROL Guardar]** para suscribirse.

<!-- This dialog will be updated before release. THe image below will need to be updated inline with these changes. -->

![El cuadro de diálogo de suscripciones de alerta.](./images/monitor-queries/alert-subscription-dialog.png)

<!-- Link to alert subscriptions doc when available -->

### Filtrar consultas

Puede filtrar consultas en función de la frecuencia de ejecución. En el [!UICONTROL Consultas programadas] , seleccione el icono de filtro (![Un icono de filtro](./images/monitor-queries/filter-icon.png)) para abrir la barra lateral de filtro.

![La pestaña de consultas programadas con el icono de filtro resaltado.](./images/monitor-queries/filter-queries.png)

Seleccione o bien **[!UICONTROL Programado]** o **[!UICONTROL Ejecutar una vez]** ejecute las casillas de verificación del filtro de frecuencia para filtrar la lista de consultas.

>[!NOTE]
>
>Cualquier consulta que se haya ejecutado pero no programada se califica como [!UICONTROL Ejecutar una vez].

![La pestaña de consultas programadas con la barra lateral de filtro resaltada.](./images/monitor-queries/filter-sidebar.png)

Una vez habilitados los criterios de filtro, seleccione **[!UICONTROL Ocultar filtros]** para cerrar el panel de filtro.

## Consulta ejecuta Detalles del programa

Seleccione un nombre de consulta para ir a la página de detalles de la programación. Esta vista proporciona una lista de todas las ejecuciones ejecutadas como parte de esa consulta programada. La información proporcionada incluye la hora de inicio y finalización, el estado y el conjunto de datos utilizados.

![La página de detalles de la programación.](./images/monitor-queries/schedule-details.png)

Esta información se proporciona en una tabla de cinco columnas. Cada fila indica una ejecución de consulta.

| El nombre de la columna | Descripción |
|---|---|
| ID de ejecución de consulta | ID de ejecución de la consulta para la ejecución diaria. |
| Inicio de la ejecución de consultas | Marca de tiempo cuando se ejecutó la consulta. Esto está en formato UTC. |
| Finalización de la ejecución de consultas | Marca de tiempo cuando se completó la consulta. Esto está en formato UTC. |
| Estado | Estado de la ejecución de consulta más reciente. Los tres valores de estado son: `successful` `failed` o `in progress`. |
| Conjunto de datos | Conjunto de datos implicado en la ejecución. |

Los detalles de la consulta que se está programando se pueden ver en la [!UICONTROL Propiedades] panel. Este panel incluye el ID de consulta inicial, el tipo de cliente, el nombre de la plantilla, el SQL de consulta y la cadencia de la programación.

![La página de detalles de la programación con el panel de propiedades resaltado.](./images/monitor-queries/properties-panel.png)

### Ejecutar detalles

Seleccione un ID de ejecución de consulta para desplazarse a la página de detalles de ejecución y ver la información de consulta.

![La pantalla de detalles de la programación con un ID de ejecución resaltado.](./images/monitor-queries/navigate-to-run-details.png)

Esta vista proporciona información sobre ejecuciones individuales para esta consulta programada y un desglose más detallado del estado de ejecución. Esta página también incluye la información del cliente y detalles de cualquier error que haya causado que la consulta falle.

![La pantalla de detalles de ejecución con la sección de información general resaltada.](./images/monitor-queries/query-run-details.png)

La sección de estado de la consulta proporciona el código de error y el mensaje de error si la consulta ha fallado.

![La pantalla de detalles de ejecución con la sección de errores resaltada.](./images/monitor-queries/failed-query.png)

Puede copiar el SQL de consulta en el portapapeles desde esta vista. Seleccione el icono de copia en la parte superior derecha del fragmento SQL para copiar la consulta. Un mensaje emergente confirma que el código se ha copiado.

![La pantalla de detalles de ejecución con el icono de copia SQL resaltado.](./images/monitor-queries/copy-sql.png)

Select **[!UICONTROL Consulta]** para volver a la pantalla de detalles de la programación, o **[!UICONTROL Consultas programadas]** para volver a la [!UICONTROL Consultas programadas] pestaña .

![La pantalla de detalles de ejecución con Query resaltado.](./images/monitor-queries/return-navigation.png)

