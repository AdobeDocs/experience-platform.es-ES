---
keywords: Experience Platform;inicio;temas populares;Editor de consultas;editor de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Guía de IU del Editor de consultas
description: El editor de consultas es una herramienta interactiva proporcionada por Adobe Experience Platform Query Service, que le permite escribir, validar y ejecutar consultas de datos de experiencia del cliente en la interfaz de usuario de Experience Platform. El Editor de consultas admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: ff4b528a0456f46d8c99e5921cfc99b197956ba6
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---

# [!DNL Query Editor] Guía de IU

[!DNL Query Editor] es una herramienta interactiva que proporciona Adobe Experience Platform [!DNL Query Service], que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente dentro de [!DNL Experience Platform] interfaz de usuario. [!DNL Query Editor] admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en [!DNL Experience Platform].

Para obtener más información acerca de los conceptos y características de [!DNL Query Service], consulte la [Introducción al servicio de consultas](../home.md). Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de consultas en [!DNL Platform], consulte la [Introducción a IU del servicio de consultas](./overview.md).

## Primeros pasos {#getting-started}

[!DNL Query Editor] proporciona una ejecución flexible de consultas conectándose a [!DNL Query Service]Las consultas, y solo se ejecutarán mientras esta conexión esté activa.

### Conectando con [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] tarda unos segundos en inicializarse y conectarse a [!DNL Query Service] cuando se abre. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, retrasará la ejecución hasta que se complete la conexión.

![Salida de consola del Editor de consultas tras la conexión inicial.](../images/ui/query-editor/connect.png)

### Ejecución de consultas desde [!DNL Query Editor] {#run-a-query}

Consultas ejecutadas desde [!DNL Query Editor] ejecutar de forma interactiva. Esto significa que si cierra el explorador o sale, la consulta se cancela. Esto también se aplica a las consultas realizadas para generar conjuntos de datos a partir de resultados de consultas.

## Creación de consultas mediante [!DNL Query Editor] {#query-authoring}

Uso de [!DNL Query Editor], puede escribir, ejecutar y guardar consultas para datos de experiencia del cliente. Todas las consultas ejecutadas o guardadas en [!DNL Query Editor] están disponibles para todos los usuarios de su organización con acceso a [!DNL Query Service].

### Acceso a [!DNL Query Editor] {#accessing-query-editor}

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Consultas]** en el menú de navegación de la izquierda para abrir [!DNL Query Service] workspace. A continuación, seleccione **[!UICONTROL Crear consulta]** en la parte superior derecha de la pantalla para empezar a escribir consultas. Este vínculo está disponible en cualquiera de las páginas del [!DNL Query Service] workspace.

![La pestaña Información general del espacio de trabajo Consultas con Crear consulta resaltada.](../images/ui/query-editor/create-query.png)

### Escritura de consultas {#writing-queries}

[!UICONTROL Editor de consultas] está organizado para que la escritura de consultas sea lo más sencilla posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con el campo de entrada SQL y **Reproducir** resaltado.

![Editor de consultas con el campo de entrada SQL y Reproducir resaltado.](../images/ui/query-editor/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar las consultas con límites en las filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, quite los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida.

### Herramientas de escritura en [!DNL Query Editor] {#writing-tools}

- **Resaltado automático de sintaxis:** Facilita la lectura y organización de SQL.

![Instrucción SQL en el Editor de consultas que muestra el resaltado de color de sintaxis.](../images/ui/query-editor/syntax-highlight.png)

- **Palabra clave SQL autocompletada:** Empiece a escribir la consulta y, a continuación, utilice las teclas de flecha para desplazarse hasta el término deseado y pulse **Entrar**.

![Algunos caracteres de SQL con el menú desplegable de autocompletar que proporciona opciones del Editor de consultas.](../images/ui/query-editor/syntax-auto.png)

- **Autocompletar tabla y campo:** Empiece a escribir el nombre de tabla que desea `SELECT` en, utilice las teclas de flecha para desplazarse a la tabla que está buscando y pulse **Entrar**. Una vez seleccionada una tabla, el completado automático reconocerá los campos de esa tabla.

![La entrada del Editor de consultas muestra sugerencias de nombres de tablas desplegables.](../images/ui/query-editor/tables-auto.png)

### Opción de configuración de IU de autocompletar {#auto-complete}

El [!DNL Query Editor] sugiere automáticamente palabras clave SQL potenciales junto con detalles de tabla o columna para la consulta a medida que la escribe. La función de autocompletar está habilitada de forma predeterminada y se puede deshabilitar o habilitar en cualquier momento seleccionando la opción [!UICONTROL Sintaxis autocompletada] en la parte superior derecha del Editor de consultas.

La configuración de autocompletar es por usuario y se recuerda por los inicios de sesión consecutivos de ese usuario.

![Editor de consultas con la opción de sintaxis autocompletada resaltada.](../images/ui/query-editor/auto-complete-toggle.png)

Al deshabilitar esta función, se detienen varios comandos de metadatos y se proporcionan recomendaciones que generalmente benefician la velocidad del autor al editar consultas.

Al utilizar la opción para habilitar la función de autocompletar, las sugerencias recomendadas para nombres de tablas y columnas, así como las palabras clave SQL, están disponibles después de una breve pausa. Un mensaje de éxito en la consola debajo del Editor de consultas indica que la función está activa.

Si deshabilita la característica de autocompletar, se requiere una actualización de la página para que la característica surta efecto. Aparecerá un cuadro de diálogo de confirmación con tres opciones cuando desactive la [!UICONTROL Sintaxis autocompletada] alternar :

- [!UICONTROL Cancelar]
- [!UICONTROL Guardar cambios y actualizar]
- [!UICONTROL Actualizar sin guardar los cambios]

>[!IMPORTANT]
>
>Si está escribiendo o editando una consulta al deshabilitar esta función, debe guardar los cambios realizados en la consulta antes de actualizar la página o se perderá todo el progreso.

![El cuadro de diálogo de confirmación para deshabilitar la función de autocompletar.](../images/ui/query-editor/confirmation-dialog.png)

Seleccione la opción adecuada para deshabilitar la función de autocompletar.

### Detección de errores {#error-detection}

[!DNL Query Editor] valida automáticamente una consulta a medida que la escribe, proporcionando validación SQL genérica y validación de ejecución específica. Si aparece una línea roja de subrayado debajo de la consulta (como se muestra en la imagen siguiente), representa un error dentro de la consulta.

![La entrada del Editor de consultas muestra SQL subrayado en rojo para indicar un error.](../images/ui/query-editor/syntax-error-highlight.png)

Cuando se detectan errores, puede ver los mensajes de error específicos pasando el ratón por encima del código SQL.

![Cuadro de diálogo con un mensaje de error.](../images/ui/query-editor/linting-error.png)

### Detalles de consulta {#query-details}

Seleccione cualquier plantilla guardada del [!UICONTROL Plantillas] para verlo en el Editor de consultas. El panel de detalles de la consulta proporciona más información y herramientas para administrar la consulta seleccionada.

![El editor de consultas con el panel de detalles de la consulta resaltado.](../images/ui/query-editor/query-details.png)

Este panel le permite generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada y agregar una programación a la consulta.

Este panel también muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde. Para generar un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos de salida]**. El **[!UICONTROL Conjunto de datos de salida]** aparece el cuadro de diálogo. Introduzca un nombre y una descripción y, a continuación, seleccione **[!UICONTROL Ejecutar consulta]**. El nuevo conjunto de datos se muestra en la **[!UICONTROL Conjuntos de datos]** de la pestaña [!DNL Query Service] interfaz de usuario en [!DNL Platform].

### Consultas programadas {#scheduled-queries}

Las consultas que se han guardado como plantilla se pueden programar desde el Editor de consultas. Esto le permite automatizar las ejecuciones de consulta que se ejecutan en una cadencia personalizada. Puede programar consultas en función de la frecuencia, la fecha y la hora, y también elegir un conjunto de datos de salida para los resultados si es necesario. Las programaciones de consultas también se pueden deshabilitar o eliminar a través de la interfaz de usuario.

Las programaciones se establecen en el Editor de consultas. Al utilizar el Editor de consultas, sólo puede agregar una programación a una consulta que ya se ha creado, guardado y ejecutado. Esto no se aplica al [!DNL Query Service] API:

Consulte la documentación de programaciones de consultas para obtener información sobre cómo [crear programaciones de consultas en la interfaz de usuario](./query-schedules.md). También puede aprender a añadir programaciones mediante la API leyendo el [guía de extremo de consultas programadas](../api/scheduled-queries.md).

Todas las consultas programadas se agregan a la lista de la [!UICONTROL Consultas programadas] pestaña. Desde ese espacio de trabajo, puede monitorizar el estado de todos los trabajos de consulta programados a través de la interfaz de usuario. En el [!UICONTROL Consultas programadas] pestaña puede encontrar información importante sobre las ejecuciones de consultas y suscribirse a alertas. La información disponible incluye el estado, los detalles de la programación y los mensajes/códigos de error en caso de que falle una ejecución. Consulte la [Documento de supervisión de consultas programadas](./monitor-queries.md) para obtener más información.

### Guardar consultas {#saving-queries}

El [!DNL Query Editor] proporciona una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Para guardar una consulta, seleccione **[!UICONTROL Guardar]** en la esquina superior derecha de [!DNL Query Editor]. Para poder guardar una consulta, debe proporcionar un nombre para la consulta utilizando **[!UICONTROL Detalles de consulta]** panel.

>[!NOTE]
>
>Las consultas con nombre y guardadas en mediante el Editor de consultas están disponibles como plantillas en el panel de consultas [!UICONTROL Plantillas] pestaña. Consulte la [documentación de plantillas](./query-templates.md) para obtener más información.

### Cómo encontrar consultas anteriores {#previous-queries}

Todas las consultas ejecutadas desde [!DNL Query Editor] se capturan en la Tabla de registro. Puede utilizar la funcionalidad de búsqueda en la **[!UICONTROL Registro]** para buscar ejecuciones de consulta. Las consultas guardadas se enumeran en la variable **[!UICONTROL Plantillas]** pestaña.

Si se ha programado una consulta, la variable [!UICONTROL Consultas programadas] proporciona una visibilidad mejorada a través de la interfaz de usuario para esos trabajos de consulta. Consulte la [documentación de monitorización de consultas](./monitor-queries.md) para obtener más información.

>[!NOTE]
>
>El registro no guarda las consultas que no se ejecutan. Para que la consulta esté disponible en [!DNL Query Service], debe ejecutarse o guardarse en [!DNL Query Editor].

## Ejecución de consultas mediante el Editor de consultas {#executing-queries}

Para ejecutar una consulta en [!DNL Query Editor], puede introducir SQL en el editor o cargar una consulta anterior desde el **[!UICONTROL Registro]** o **[!UICONTROL Plantillas]** y seleccione. **Reproducir**. El estado de ejecución de la consulta se muestra en la variable **[!UICONTROL Consola]** , los datos de salida se muestran en la pestaña **[!UICONTROL Resultados]** pestaña.

### Consola {#console}

La consola proporciona información sobre el estado y el funcionamiento de [!DNL Query Service]. La consola muestra el estado de la conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error resultantes de esas consultas.

![La pestaña Consola de la consola del Editor de consultas.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La consola solo muestra los errores resultantes de la ejecución de una consulta. No muestra errores de validación de consultas antes de ejecutar una consulta.

### Resultados de consulta {#query-results}

Una vez completada la consulta, los resultados se muestran en la variable **[!UICONTROL Resultados]** , junto a la pestaña **[!UICONTROL Consola]** pestaña. Esta vista muestra el resultado tabular de la consulta, con un máximo de 100 filas. Esta vista le permite comprobar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, quite los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida. Consulte la [tutorial de generación de conjuntos de datos](./create-datasets.md) para obtener instrucciones sobre cómo generar un conjunto de datos a partir de los resultados de la consulta en [!DNL Query Editor].

![La pestaña Resultados de la consola del Editor de consultas muestra los resultados de una ejecución de consulta.](../images/ui/query-editor/query-results.png)

## Ejecutar consultas con [!DNL Query Service] tutorial en vídeo {#query-tutorial-video}

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente SQL. Además, se muestra el uso de propiedades individuales en un objeto XDM, el uso de funciones definidas por el Adobe y el uso de CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Pasos siguientes

Ahora que sabe qué funciones están disponibles en [!DNL Query Editor] y cómo navegar por la aplicación, puede empezar a crear sus propias consultas directamente en [!DNL Platform]. Para obtener más información sobre la ejecución de consultas SQL en conjuntos de datos en [!DNL Data Lake], consulte la guía de [ejecución de consultas](../best-practices/writing-queries.md).
