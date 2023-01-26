---
title: Monitorizar consultas programadas
description: Obtenga información sobre cómo monitorizar consultas a través de la interfaz de usuario del servicio de consulta.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 95d3604a9589a4d0db7e426dd000ddec9cd4f2ce
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---

# Monitorización de consultas programadas

Adobe Experience Platform proporciona una visibilidad mejorada para el estado de todos los trabajos de consulta a través de la interfaz de usuario. De [!UICONTROL Consultas programadas] ahora puede encontrar información importante sobre las ejecuciones de consultas que incluye el estado, los detalles de la programación y los mensajes/códigos de error si fallan. También puede suscribirse a alertas para consultas en función de su estado a través de la interfaz de usuario para cualquiera de estas consultas mediante [!UICONTROL Consultas programadas] pestaña .

## [!UICONTROL Consultas programadas]

La variable [!UICONTROL Consultas programadas] proporciona una descripción general de todas sus consultas de CTAS e ITAS programadas. Se pueden encontrar detalles de ejecución para todas las consultas programadas, así como códigos de error y mensajes para cualquier consulta fallida.

Para ir a la [!UICONTROL Consultas programadas] , seleccione **[!UICONTROL Consultas]** desde la barra de navegación izquierda seguida de **[!UICONTROL Consultas programadas]**

![La ficha Consultas programadas del espacio de trabajo Consultas .](../images/ui/monitor-queries/scheduled-queries.png)

La tabla siguiente describe cada columna disponible.

>[!NOTE]
>
>El icono de suscripciones de alerta está contenido en cada fila de una columna sin título. Consulte la [suscripciones de alerta](#alert-subscription) para obtener más información.

| Columna | Descripción |
|---|---|
| **[!UICONTROL Nombre]** | El campo de nombre es el nombre de la plantilla o los primeros caracteres de la consulta SQL. Cualquier consulta creada a través de la interfaz de usuario con el Editor de consultas recibe un nombre desde el principio. Si la consulta se creó mediante la API, su nombre se convierte en un fragmento del SQL inicial utilizado para crear la consulta. Seleccione cualquier elemento del [!UICONTROL Nombre] para ver una lista de todas las ejecuciones asociadas con la consulta. Para obtener más información, consulte [ejecución de consultas detalles de programación](#query-runs) para obtener más información. |
| **[!UICONTROL Plantilla]** | El nombre de plantilla de la consulta. Seleccione un nombre de plantilla para ir al Editor de consultas. La plantilla de consulta se muestra en el Editor de consultas para mayor comodidad. Si no hay ningún nombre de plantilla, la fila se marca con un guión y no se puede redirigir al Editor de consultas para ver la consulta. |
| **[!UICONTROL SQL]** | Un fragmento de la consulta SQL. |
| **[!UICONTROL Frecuencia de ejecución]** | Esta es la cadencia en la que se configura la ejecución de la consulta. Los valores disponibles son `Run once` y `Scheduled`. Las consultas se pueden filtrar según su frecuencia de ejecución. |
| **[!UICONTROL Creado por]** | Nombre del usuario que creó la consulta. |
| **[!UICONTROL Creado]** | Marca de tiempo cuando se creó la consulta, en formato UTC. |
| **[!UICONTROL Marca de tiempo de última ejecución]** | Marca de tiempo más reciente cuando se ejecutó la consulta. Esta columna resalta si una consulta se ha ejecutado según su programación actual. |
| **[!UICONTROL Último estado de ejecución]** | Estado de la ejecución de consulta más reciente. Los valores de estado son: `Success`, `Failed`, `In progress`y `No runs`. |

>[!TIP]
>
>Si va al Editor de consultas, puede seleccionar **[!UICONTROL Consultas]** para volver a la [!UICONTROL Plantillas] pestaña .

### Personalización de la configuración de tabla para consultas programadas

Puede ajustar las columnas en la [!UICONTROL Consultas programadas] a sus necesidades. Seleccione el icono de configuración (![Un icono de configuración.](../images/ui/monitor-queries/settings-icon.png)) para abrir el [!UICONTROL Personalizar tabla] cuadro de diálogo configuración y editar las columnas disponibles.

![El icono Personalizar configuración de tabla .](../images/ui/monitor-queries/customze-table-settings-icon.png)

Active las casillas de verificación correspondientes para eliminar o agregar una columna de tabla. A continuación, seleccione **[!UICONTROL Aplicar]** para confirmar las opciones.

>[!NOTE]
>
>Cualquier consulta creada a través de la interfaz de usuario se convierte en una plantilla con nombre como parte del proceso de creación. El nombre de la plantilla se ve en la columna plantilla . Si la consulta se creó a través de la API, la columna de la plantilla está en blanco.

![El cuadro de diálogo Personalizar configuración de tabla.](../images/ui/monitor-queries/customize-table-dialog.png)

### Suscripción a alertas {#alert-subscription}

Puede suscribirse a las alertas desde el [!UICONTROL Consultas programadas] pestaña . Seleccione el icono de notificación de alerta (![Un icono de alerta.](../images/ui/monitor-queries/alerts-icon.png)) junto al nombre de la consulta para abrir el [!UICONTROL Alertas] diálogo. La variable [!UICONTROL Alertas] se suscribe a las notificaciones de la interfaz de usuario y a las alertas de correo electrónico. Las alertas se basan en el estado de la consulta. Hay tres opciones disponibles: `start`, `success`y `failure`. Marque las casillas adecuadas y seleccione **[!UICONTROL Guardar]** para suscribirse.

![El cuadro de diálogo de suscripciones de alerta.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Consulte la [documentación de la API de suscripciones de alerta](../api/alert-subscriptions.md) para obtener más información.

### Filtrar consultas {#filter}

Puede filtrar consultas en función de la frecuencia de ejecución. En el [!UICONTROL Consultas programadas] , seleccione el icono de filtro (![Un icono de filtro](../images/ui/monitor-queries/filter-icon.png)) para abrir la barra lateral de filtro.

![La pestaña de consultas programadas con el icono de filtro resaltado.](../images/ui/monitor-queries/filter-queries.png)

Seleccione o bien **[!UICONTROL Programado]** o **[!UICONTROL Ejecutar una vez]** ejecute las casillas de verificación del filtro de frecuencia para filtrar la lista de consultas.

>[!NOTE]
>
>Cualquier consulta que se haya ejecutado pero no programada se califica como [!UICONTROL Ejecutar una vez].

![La pestaña de consultas programadas con la barra lateral de filtro resaltada.](../images/ui/monitor-queries/filter-sidebar.png)

Una vez habilitados los criterios de filtro, seleccione **[!UICONTROL Ocultar filtros]** para cerrar el panel de filtro.

## Consulta ejecuta detalles de programación {#query-runs}

Seleccione un nombre de consulta para ir a la página de detalles de la programación. Esta vista proporciona una lista de todas las ejecuciones ejecutadas como parte de esa consulta programada. La información proporcionada incluye la hora de inicio y finalización, el estado y el conjunto de datos utilizados.

![La página de detalles de la programación.](../images/ui/monitor-queries/schedule-details.png)

Esta información se proporciona en una tabla de cinco columnas. Cada fila indica una ejecución de consulta.

| El nombre de la columna | Descripción |
|---|---|
| **[!UICONTROL ID de ejecución de consulta]** | ID de ejecución de la consulta para la ejecución diaria. Seleccione el **[!UICONTROL ID de ejecución de consulta]** para navegar hasta el [!UICONTROL Información general de ejecución de consultas]. |
| **[!UICONTROL Inicio de la ejecución de consultas]** | Marca de tiempo cuando se ejecutó la consulta. Esto está en formato UTC. |
| **[!UICONTROL Finalización de la ejecución de consultas]** | Marca de tiempo cuando se completó la consulta. Esto está en formato UTC. |
| **[!UICONTROL Estado]** | Estado de la ejecución de consulta más reciente. Los tres valores de estado son: `successful` `failed` o `in progress`. |
| **[!UICONTROL Conjunto de datos]** | Conjunto de datos implicado en la ejecución. |

Los detalles de la consulta que se está programando se pueden ver en la [!UICONTROL Propiedades] panel. Este panel incluye el ID de consulta inicial, el tipo de cliente, el nombre de la plantilla, el SQL de consulta y la cadencia de la programación.

![La página de detalles de la programación con el panel de propiedades resaltado.](../images/ui/monitor-queries/properties-panel.png)

Seleccione un ID de ejecución de consulta para desplazarse a la página de detalles de ejecución y ver la información de consulta.

![La pantalla de detalles de la programación con un ID de ejecución resaltado.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Información general de ejecución de consultas {#query-run-overview}

La variable [!UICONTROL Información general de ejecución de consultas] proporciona información sobre ejecuciones individuales para esta consulta programada y un desglose más detallado del estado de ejecución. Esta página también incluye la información del cliente y detalles de cualquier error que pueda haber causado que la consulta falle.

![La pantalla de detalles de ejecución con la sección de información general resaltada.](../images/ui/monitor-queries/query-run-details.png)

La sección de estado de la consulta proporciona el código de error y el mensaje de error si la consulta ha fallado.

![La pantalla de detalles de ejecución con la sección de errores resaltada.](../images/ui/monitor-queries/failed-query.png)

Puede copiar el SQL de consulta en el portapapeles desde esta vista. Seleccione el icono de copia en la parte superior derecha del fragmento SQL para copiar la consulta. Un mensaje emergente confirma que el código se ha copiado.

![La pantalla de detalles de ejecución con el icono de copia SQL resaltado.](../images/ui/monitor-queries/copy-sql.png)

### (Versión limitada) Ejecute detalles para consultas con bloques anónimos {#anonymous-block-queries}

>[!IMPORTANT]
>
>La función de supervisión de consultas que muestra detalles de ejecución para consultas de bloques anónimas, se encuentra actualmente en una versión limitada y no está disponible para todos los clientes.

Las consultas que utilizan bloques anónimos para conformar sus sentencias SQL se separan en sus consultas individuales. Esto le permite inspeccionar individualmente los detalles de ejecución de cada bloque de consulta.

Los bloques anónimos se identifican mediante el uso de un `$$` antes de la consulta. Consulte la [documento de bloque anónimo](../essential-concepts/anonymous-block.md) para obtener más información sobre los bloques anónimos en el servicio de consulta.

Las consultas de bloque anónimas tienen pestañas a la izquierda del estado de ejecución. Seleccione una pestaña para mostrar los detalles de ejecución.

![La descripción general de la ejecución de consultas muestra una consulta de bloque anónima. Se resaltan las múltiples pestañas de consulta.](../images/ui/monitor-queries/anonymous-block-overview.png)

En caso de que falle una consulta de bloque anónima, puede encontrar el código de error para ese bloque en particular a través de esta interfaz de usuario.

![La descripción general de la ejecución de la consulta muestra una consulta de bloque anónima con el código de error de un solo bloque resaltado.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Select **[!UICONTROL Consulta]** para volver a la pantalla de detalles de la programación, o **[!UICONTROL Consultas programadas]** para volver a la [!UICONTROL Consultas programadas] pestaña .

![La pantalla de detalles de ejecución con Query resaltado.](../images/ui/monitor-queries/return-navigation.png)
