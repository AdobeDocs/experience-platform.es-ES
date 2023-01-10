---
keywords: Experience Platform;inicio;temas populares;editor de consultas;editor de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del Editor de consultas
description: El Editor de consultas es una herramienta interactiva que proporciona el servicio de consultas de Adobe Experience Platform, que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de usuario del Experience Platform. El Editor de consultas admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 0%

---

# [!DNL Query Editor] Guía de la interfaz de usuario

[!DNL Query Editor] es una herramienta interactiva que proporciona Adobe Experience Platform [!DNL Query Service], lo que le permite escribir, validar y ejecutar consultas para los datos de experiencia del cliente en el [!DNL Experience Platform] interfaz de usuario. [!DNL Query Editor] admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en [!DNL Experience Platform].

Para obtener más información sobre los conceptos y las características de [!DNL Query Service], consulte la [Información general del servicio de consultas](../home.md). Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de consulta en [!DNL Platform], consulte la [Información general sobre la interfaz de usuario del servicio de consulta](./overview.md).

## Primeros pasos {#getting-started}

[!DNL Query Editor] proporciona una ejecución flexible de consultas conectándose a [!DNL Query Service], y las consultas solo se ejecutarán mientras esta conexión esté activa.

### Conexión a [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] tarda unos segundos en inicializarse y conectarse a [!DNL Query Service] cuando se abra. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, se retrasa la ejecución hasta que se complete la conexión.

![La salida de la consola del Editor de consultas tras la conexión inicial.](../images/ui/query-editor/connect.png)

### Cómo se ejecutan las consultas desde [!DNL Query Editor] {#run-a-query}

Consultas ejecutadas desde [!DNL Query Editor] se ejecuta de forma interactiva. Esto significa que si cierra el explorador o se va, la consulta se cancela. Esto también se aplica a las consultas realizadas para generar conjuntos de datos a partir de resultados de consultas.

## Creación de consultas mediante [!DNL Query Editor] {#query-authoring}

Uso [!DNL Query Editor], puede escribir, ejecutar y guardar consultas para datos de experiencias del cliente. Todas las consultas ejecutadas o guardadas en [!DNL Query Editor] están disponibles para todos los usuarios de su organización con acceso a [!DNL Query Service].

### Acceso a [!DNL Query Editor] {#accessing-query-editor}

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Consultas]** en el menú de navegación de la izquierda para abrir [!DNL Query Service] espacio de trabajo. A continuación, seleccione **[!UICONTROL Crear consulta]** en la parte superior derecha de la pantalla para comenzar a escribir consultas. Este vínculo está disponible desde cualquiera de las páginas de la sección [!DNL Query Service] espacio de trabajo.

![La pestaña Información general del espacio de trabajo Consultas con la opción Crear consulta resaltada.](../images/ui/query-editor/create-query.png)

### Escritura de consultas {#writing-queries}

[!UICONTROL Editor de consultas] está organizado para que la escritura de consultas sea lo más sencilla posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con el campo de entrada SQL y **Play** resaltado.

![El Editor de consultas con el campo de entrada SQL y Play resaltado.](../images/ui/query-editor/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar las consultas con límites en las filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, elimine los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida .

### Herramientas de escritura en [!DNL Query Editor] {#writing-tools}

- **Resaltado de sintaxis automático:** Facilita la lectura y organización de SQL.

![Instrucción SQL en el Editor de consultas que muestra el resaltado del color de la sintaxis.](../images/ui/query-editor/syntax-highlight.png)

- **Palabra clave SQL autocompletada:** Comience a escribir la consulta, utilice las teclas de flecha para ir al término deseado y pulse **Entrar**.

![Algunos caracteres de SQL con el menú desplegable autocompletado que proporciona las opciones del Editor de consultas.](../images/ui/query-editor/syntax-auto.png)

- **Tabla y campo autocompletados:** Comience a escribir el nombre de tabla que desee `SELECT` en , utilice las teclas de flecha para desplazarse hasta la tabla que está buscando y pulse **Entrar**. Una vez seleccionada una tabla, el llenado automático reconocerá los campos de dicha tabla.

![La entrada del Editor de consultas muestra las sugerencias de nombre de tabla desplegable.](../images/ui/query-editor/tables-auto.png)

### (Versión limitada) Alternación de configuración de la interfaz de usuario de autocompletar {#auto-complete}

>[!IMPORTANT]
>
>La opción de configuración de la interfaz de usuario de autocompletar está actualmente en una versión limitada y no está disponible para todos los clientes.

La variable [!DNL Query Editor] sugiere automáticamente posibles palabras clave SQL junto con detalles de tabla o columna para la consulta mientras la escribe. La función de autocompletar está activada de forma predeterminada y se puede deshabilitar o habilitar en cualquier momento seleccionando la opción [!UICONTROL Autocompletar sintaxis] alternar a la parte superior derecha del Editor de consultas.

La configuración de autocompletar es por usuario y se recuerda para los inicios de sesión consecutivos de ese usuario.

![Editor de consultas con la opción de completado automático de sintaxis resaltada.](../images/ui/query-editor/auto-complete-toggle.png)

Al desactivar esta función, se evitan que se procesen varios comandos de metadatos y se ofrecen recomendaciones que normalmente mejoran la velocidad del autor al editar consultas.

Al utilizar el botón de alternancia para habilitar la función de autocompletar, las sugerencias recomendadas para nombres de columnas y tablas, así como palabras clave SQL, estarán disponibles después de una breve pausa. Un mensaje de éxito en la consola, debajo del Editor de consultas, indica que la función está activa.

Si desactiva la función de autocompletar, es necesario actualizar la página para que la función surta efecto. Aparece un cuadro de diálogo de confirmación con tres opciones al desactivar el [!UICONTROL Autocompletar sintaxis] alternar :

- [!UICONTROL Cancelar]
- [!UICONTROL Guardar cambios y actualizar]
- [!UICONTROL Actualizar sin guardar cambios]

>[!IMPORTANT]
>
>Si está escribiendo o editando una consulta al deshabilitar esta función, debe guardar los cambios en la consulta antes de actualizar la página o se perderá todo el progreso.

![El cuadro de diálogo de confirmación para desactivar la función de autocompletar.](../images/ui/query-editor/confirmation-dialog.png)

Seleccione la opción adecuada para desactivar la función de autocompletar.

### Detección de errores {#error-detection}

[!DNL Query Editor] valida automáticamente una consulta a medida que la escribe, proporcionando validación SQL genérica y validación de ejecución específica. Si aparece un subrayado rojo debajo de la consulta (como se muestra en la imagen siguiente), representa un error dentro de la consulta.

![La entrada del Editor de consultas muestra SQL subrayado en rojo para indicar un error.](../images/ui/query-editor/syntax-error-highlight.png)

Cuando se detectan errores, se pueden ver los mensajes de error específicos pasando el cursor sobre el código SQL.

![Cuadro de diálogo con un mensaje de error.](../images/ui/query-editor/linting-error.png)

### Detalles de la consulta {#query-details}

Seleccione cualquier plantilla guardada de la variable [!UICONTROL Plantillas] para verlo en el Editor de consultas. El panel de detalles de la consulta proporciona más información y herramientas para administrar la consulta seleccionada.

![El Editor de consultas con el panel de detalles de la consulta resaltado.](../images/ui/query-editor/query-details.png)

Este panel le permite generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada y agregar una programación a la consulta.

Este panel también muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde. Para generar un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos de salida]**. La variable **[!UICONTROL Conjunto de datos de salida]** se abre. Introduzca un nombre y una descripción y, a continuación, seleccione **[!UICONTROL Ejecutar consulta]**. El nuevo conjunto de datos se muestra en la **[!UICONTROL Conjuntos de datos]** en la ficha [!DNL Query Service] interfaz de usuario activada [!DNL Platform].

### Consultas programadas {#scheduled-queries}

>[!IMPORTANT]
>
>A continuación se muestra una lista de limitaciones para las consultas programadas al utilizar el Editor de consultas. No se aplican al [!DNL Query Service] API:<br/>Solo puede añadir una programación a una consulta que ya se haya creado, guardado y ejecutado.<br/>You **cannot** agregue una programación a una consulta parametrizada.<br/>Consultas programadas **cannot** contiene un bloque anónimo.

Las programaciones se configuran desde el Editor de consultas. Sin embargo, solo se pueden programar las consultas que ya se han guardado como plantilla. Para agregar una programación a una consulta, seleccione una plantilla de consulta desde la [!UICONTROL Plantillas] o [!UICONTROL Consultas programadas] para ir al Editor de consultas.

Para aprender a añadir programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).

Cuando se accede a una consulta guardada desde el Editor de consultas, la variable [!UICONTROL Programaciones] aparece debajo del nombre de la consulta. Select **[!UICONTROL Programaciones]**.

![El Editor de consultas con la ficha Programas resaltada.](../images/ui/query-editor/schedules-tab.png)

Aparecerá el espacio de trabajo de programaciones. Select **[!UICONTROL Agregar programación]** para crear una programación.

![Espacio de trabajo Programar del Editor de consultas con la opción Agregar programación resaltada.](../images/ui/query-editor/add-schedule.png)

Aparecerá la página de detalles de la programación. En esta página, puede elegir la frecuencia de la consulta programada, la fecha de inicio y finalización, el día de la semana en que se ejecutará la consulta programada, así como el conjunto de datos al que exportar la consulta.

![El panel Detalles del programa está resaltado.](../images/ui/query-editor/schedule-details.png)

Puede elegir las siguientes opciones para **[!UICONTROL Frecuencia]**:

- **[!UICONTROL Por hora]**: La consulta programada se ejecutará cada hora para el período de fecha seleccionado.
- **[!UICONTROL Diario]**: La consulta programada se ejecutará cada X días a la hora y el periodo de fecha seleccionados. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.
- **[!UICONTROL Semanal]**: La consulta seleccionada se ejecutará en los días de la semana, la hora y el período de fecha seleccionado. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.
- **[!UICONTROL Mensual]**: La consulta seleccionada se ejecutará todos los meses del día, la hora y el período de fecha seleccionado. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.
- **[!UICONTROL Anual]**: La consulta seleccionada se ejecutará cada año en el día, mes, hora y período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada está en **UTC** y no su zona horaria local.

Para el conjunto de datos, tiene la opción de usar un conjunto de datos existente o crear un nuevo conjunto de datos.

>[!IMPORTANT]
>
> Como está utilizando un conjunto de datos existente o creando uno nuevo, sí lo hace **not** debe incluir: `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de la consulta, ya que los conjuntos de datos ya están establecidos. Incluyendo: `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de las consultas programadas, se producirá un error.

Después de confirmar todos estos detalles, seleccione **[!UICONTROL Guardar]** para crear una programación. Volverá al espacio de trabajo de programaciones , que muestra detalles de la programación recién creada, incluido el ID de programación, la propia programación y el conjunto de datos de salida de la programación. Puede utilizar el ID de programación para buscar más información sobre las ejecuciones de la propia consulta programada. Para obtener más información, lea la [guía de extremos de ejecución de consultas programadas](../api/runs-scheduled-queries.md).

![El espacio de trabajo de programaciones con la programación recién creada resaltada.](../images/ui/query-editor/schedules-workspace.png)

#### Eliminar o deshabilitar una programación {#delete-schedule}

Puede eliminar o desactivar una programación del espacio de trabajo de programaciones. Debe seleccionar una plantilla de consulta desde la [!UICONTROL Plantillas] o [!UICONTROL Consultas programadas] para ir al Editor de consultas y seleccionar **[!UICONTROL Programación]** para acceder al espacio de trabajo de programaciones.

Seleccione una programación de las filas de programaciones disponibles. Puede utilizar el botón de alternancia para deshabilitar o habilitar la consulta programada.

>[!IMPORTANT]
>
>Debe desactivar la programación para poder eliminar una programación de una consulta.

Select **[!UICONTROL Eliminar una programación]** para eliminar la programación deshabilitada.

![El espacio de trabajo de programaciones con Desactivar programación y Eliminar programación resaltado.](../images/ui/query-editor/delete-schedule.png)

### Almacenamiento de consultas {#saving-queries}

La variable [!DNL Query Editor] proporciona una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Para guardar una consulta, seleccione **[!UICONTROL Guardar]** en la esquina superior derecha de [!DNL Query Editor]. Para poder guardar una consulta, debe proporcionarse un nombre para la consulta mediante la variable **[!UICONTROL Detalles de la consulta]** panel.

>[!NOTE]
>
>Las consultas con nombre y guardadas con el Editor de consultas están disponibles como plantillas en el panel Consulta [!UICONTROL Plantillas] pestaña . Consulte la [documentación de plantillas](./query-templates.md) para obtener más información.

### Búsqueda de consultas anteriores {#previous-queries}

Todas las consultas ejecutadas desde [!DNL Query Editor] se capturan en la tabla Registro . Puede utilizar la funcionalidad de búsqueda en la variable **[!UICONTROL Registro]** para buscar ejecuciones de consulta. Las consultas guardadas se enumeran en el **[!UICONTROL Plantillas]** pestaña .

Si se programó una consulta, entonces la variable [!UICONTROL Consultas programadas] proporciona una visibilidad mejorada a través de la interfaz de usuario para esos trabajos de consulta. Consulte la [documentación de monitorización de consultas](../monitor-queries.md) para obtener más información.

>[!NOTE]
>
>El registro no guarda las consultas que no se ejecutan. Para que la consulta esté disponible en [!DNL Query Service], debe ejecutarse o guardarse en [!DNL Query Editor].

## Ejecución de consultas mediante el Editor de consultas {#executing-queries}

Para ejecutar una consulta en [!DNL Query Editor], puede introducir SQL en el editor o cargar una consulta anterior desde el **[!UICONTROL Registro]** o **[!UICONTROL Plantillas]** y seleccione **Play**. El estado de la ejecución de la consulta se muestra en la variable **[!UICONTROL Consola]** y los datos de salida se muestran en la pestaña **[!UICONTROL Resultados]** pestaña .

### Consola {#console}

La consola proporciona información sobre el estado y el funcionamiento de [!DNL Query Service]. La consola muestra el estado de conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error que resulten de esas consultas.

![La ficha Consola de la consola del Editor de consultas.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La consola solo muestra los errores resultantes de la ejecución de una consulta. No muestra errores de validación de consultas antes de ejecutar una consulta.

### Resultados de la consulta {#query-results}

Una vez completada la consulta, los resultados se muestran en la variable **[!UICONTROL Resultados]** junto a la pestaña **[!UICONTROL Consola]** pestaña . Esta vista muestra el resultado tabular de la consulta, mostrando hasta 100 filas. Esta vista le permite verificar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, elimine los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida . Consulte la [tutorial generación de conjuntos de datos](./create-datasets.md) para obtener instrucciones sobre cómo generar un conjunto de datos a partir de resultados de consulta en [!DNL Query Editor].

![La ficha Resultados de la consola del Editor de consultas muestra los resultados de una ejecución de consulta.](../images/ui/query-editor/query-results.png)

## Ejecutar consultas con [!DNL Query Service] videotutorial {#query-tutorial-video}

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente PSQL. Además, se muestran el uso de propiedades individuales en un objeto XDM, el uso de funciones definidas por Adobe y el uso de CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Pasos siguientes

Ahora sabe qué características están disponibles en [!DNL Query Editor] y cómo navegar por la aplicación, puede empezar a crear sus propias consultas directamente en [!DNL Platform]. Para obtener más información sobre cómo ejecutar consultas SQL con conjuntos de datos en [!DNL Data Lake], consulte la guía de [ejecución de consultas](../best-practices/writing-queries.md).
