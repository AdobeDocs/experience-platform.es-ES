---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;query;editor de consultas;Editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de IU del servicio de consultas
description: Adobe Experience Platform Query Service proporciona una interfaz de usuario que se puede utilizar para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a las guardadas por usuarios de su organización.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 1%

---

# Guía de la interfaz de usuario [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] proporciona una interfaz de usuario que se puede utilizar para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a las guardadas por usuarios de su organización. Para acceder a la interfaz de usuario en [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo.

## [!DNL Query Editor]

[!DNL Query Editor] le permite escribir y ejecutar consultas sin utilizar un cliente externo. Seleccione **[!UICONTROL Crear consulta]** para abrir [!DNL Query Editor] y crear una nueva consulta. También puede obtener acceso a [!DNL Query Editor] si selecciona una consulta en las fichas **[!UICONTROL Registro]** o **[!UICONTROL Plantillas]**. Si se selecciona una consulta guardada o ejecutada anteriormente, se abrirá [!DNL Query Editor] y se mostrará el SQL de la consulta seleccionada.

![Panel de consultas con Crear consulta resaltado.](../images/ui/overview/overview.png)

[!DNL Query Editor] proporciona espacio de edición donde puede empezar a escribir una consulta. A medida que escribe, el editor completa automáticamente las palabras reservadas de SQL, las tablas y los nombres de campo dentro de las tablas. Cuando termine de escribir la consulta, seleccione el botón **Reproducir** para ejecutarla. La ficha **[!UICONTROL Consola]** debajo del editor muestra lo que [!DNL Query Service] está haciendo actualmente, lo que indica cuándo se ha devuelto una consulta. La ficha **[!UICONTROL Result]**, junto a la Consola, muestra los resultados de la consulta. Consulte la [guía del editor de consultas](./user-guide.md) para obtener más información sobre cómo usar [!DNL Query Editor].

![Se ha ampliado la imagen en vista de [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Consultas programadas {#scheduled-queries}

Las consultas que ya se han guardado como plantilla se pueden programar para ejecutarse en una cadencia normal. Al programar una consulta, puede elegir la frecuencia de ejecuciones, la fecha de inicio y finalización, el día de la semana en que se ejecuta la consulta programada, así como el conjunto de datos al que exportar la consulta. Las programaciones de consultas se establecen mediante el Editor de consultas.

Para obtener información sobre cómo programar una consulta a través de la interfaz de usuario, consulte la [guía de consultas programadas](./user-guide.md#scheduled-queries). Para obtener información sobre cómo agregar programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).

Una vez programada una consulta, aparece en la lista de consultas programadas de la ficha [!UICONTROL Consultas programadas]. Para obtener todos los detalles sobre la consulta, las ejecuciones, el creador y los tiempos, seleccione una consulta programada en la lista.

![Área de trabajo Consultas con la ficha Consultas programadas resaltada y que muestra filas de programaciones de consultas.](../images/ui/overview/scheduled-queries.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El campo de nombre es el nombre de la plantilla o los primeros caracteres de la consulta SQL. Cualquier consulta creada a través de la interfaz de usuario con el Editor de consultas recibe el nombre al principio. Si la consulta se creó a través de la API, el nombre de la consulta es un fragmento del SQL inicial utilizado para crear la consulta. |
| **[!UICONTROL Plantilla]** | Nombre de plantilla de la consulta. Seleccione un nombre de plantilla para navegar hasta el Editor de consultas. La plantilla de consulta se muestra en el Editor de consultas para mayor comodidad. Si no hay ningún nombre de plantilla, la fila se marca con un guión y no se puede redirigir al Editor de consultas para ver la consulta. |
| **[!UICONTROL SQL]** | Un fragmento de la consulta SQL. |
| **[!UICONTROL Frecuencia de ejecución]** | Cadencia con la que se configura la ejecución de la consulta. Los valores disponibles son `Run once` y `Scheduled`. Las consultas se pueden filtrar según su frecuencia de ejecución. |
| **[!UICONTROL Creado por]** | El nombre del usuario que creó la consulta. |
| **[!UICONTROL Creado]** | La marca de tiempo cuando se creó la consulta, en formato UTC. |
| **[!UICONTROL Marca de tiempo de la última ejecución]** | La marca de tiempo más reciente cuando se ejecutó la consulta. Esta columna resalta si una consulta se ha ejecutado según su programación actual. |
| **[!UICONTROL Último estado de ejecución]** | El estado de la ejecución de consulta más reciente. Los tres valores de estado son: `successful` `failed` o `in progress`. |

Consulte la documentación para obtener más información sobre cómo [supervisar consultas a través de la IU del servicio de consultas](./monitor-queries.md).

## Plantillas {#browse}

La ficha **[!UICONTROL Plantillas]** muestra las consultas guardadas por los usuarios de su organización. Es útil considerarlas como proyectos de consulta, ya que las consultas guardadas aquí pueden estar aún en construcción. Las consultas mostradas en la ficha **[!UICONTROL Plantillas]** también se muestran como consultas de ejecución en la ficha **[!UICONTROL Registro]** si [!DNL Query Service] las ha ejecutado anteriormente.

![Se ha ampliado la vista de la ficha Plantillas del panel Consultas que muestra varias consultas guardadas.](../images/ui/overview/templates.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El campo de nombre es el nombre de la consulta creado por el usuario o los primeros caracteres de la consulta SQL. Cualquier consulta creada a través de la interfaz de usuario con el Editor de consultas recibe el nombre al principio. Si la consulta se creó a través de la API, el nombre de la consulta es un fragmento del SQL inicial utilizado para crear la consulta. Puede seleccionar el nombre de la consulta para abrirla en [!DNL Query Editor]. También puede usar la barra de búsqueda para buscar [!UICONTROL Name] de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL SQL]** | Los primeros caracteres de la consulta SQL. Al pasar el ratón por encima del código, se muestra la consulta completa. |
| **[!UICONTROL Modificado por]** | El último usuario que modificó la consulta. Cualquier usuario de su organización con acceso a [!DNL Query Service] puede modificar consultas. |
| **[!UICONTROL Última modificación]** | La fecha y la hora de la última modificación de la consulta, en el huso horario del explorador. |

Consulte la documentación de [plantillas de consulta](./query-templates.md) para obtener más información sobre las plantillas en la interfaz de usuario de Platform.

## Registro {#log}

La pestaña **[!UICONTROL Log]** proporciona una lista de consultas que se han ejecutado anteriormente. De forma predeterminada, el registro muestra las consultas en cronología inversa.

![Se ha ampliado la vista de la ficha Registro del panel Consultas que muestra una lista de consultas en orden cronológico inverso.](../images/ui/overview/log.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El nombre de la consulta, que consta de los primeros caracteres de la consulta SQL. Seleccione el nombre de la plantilla para abrir la vista [!UICONTROL Detalles del registro de consultas] para esa ejecución. Puede utilizar la barra de búsqueda para buscar el nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL Hora de inicio]** | Hora a la que se ejecutó la consulta. |
| **[!UICONTROL Tiempo completo]** | Hora a la que se completó la ejecución de la consulta. |
| **[!UICONTROL Estado]** | El estado actual de la consulta. |
| **[!UICONTROL Conjunto de datos]** | Conjunto de datos de entrada utilizado por la consulta. Seleccione el conjunto de datos para ir a la pantalla de detalles del conjunto de datos de entrada. |
| **[!UICONTROL Cliente]** | El cliente utilizado para la consulta. |
| **[!UICONTROL Creado por]** | El nombre de la persona que creó la consulta. |

>
>
>Seleccione el icono de lápiz (![Un icono de lápiz.](/help/images/icons/edit.png)) desde cualquier fila del registro de consultas para navegar hasta [!DNL Query Editor]. La consulta se rellena previamente para facilitar la edición.

Consulte la [documentación de registros de consulta](./query-logs.md) para obtener más información sobre los archivos de registro generados automáticamente por un evento de consulta.

## Credenciales

La ficha **[!UICONTROL Credenciales]** muestra tanto las credenciales que caducan como las que no caducan. Para obtener más información sobre cómo usar estas credenciales para conectarse con clientes externos, lea la [guía de credenciales](../clients/overview.md).

![Panel de consultas con la ficha Credenciales resaltada.](../images/ui/overview/credentials.png)

## Pasos siguientes

Ahora que está familiarizado con la interfaz de usuario de [!DNL Query Service] en [!DNL Platform], puede acceder a [!DNL Query Editor] para empezar a crear sus propios proyectos de consulta y compartirlos con otros usuarios de su organización. Para obtener más información sobre la creación y ejecución de consultas en [!DNL Query Editor], consulte la [[!DNL Query Editor] guía del usuario](./user-guide.md).
