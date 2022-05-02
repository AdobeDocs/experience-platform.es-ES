---
keywords: Experience Platform;inicio;temas populares;editor de consultas;editor de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del Editor de consultas
topic-legacy: query editor
description: El Editor de consultas es una herramienta interactiva que proporciona el servicio de consultas de Adobe Experience Platform, que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de usuario del Experience Platform. El Editor de consultas admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: aa61cb696d647c5f039283ce5926d5fa1e901a13
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 1%

---

# [!DNL Query Editor] Guía de la interfaz de usuario

[!DNL Query Editor] es una herramienta interactiva que proporciona Adobe Experience Platform [!DNL Query Service], lo que le permite escribir, validar y ejecutar consultas para los datos de experiencia del cliente en el [!DNL Experience Platform] interfaz de usuario. [!DNL Query Editor] admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en [!DNL Experience Platform].

Para obtener más información sobre los conceptos y las características de [!DNL Query Service], consulte la [Información general del servicio de consultas](../home.md). Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de consulta en [!DNL Platform], consulte la [Información general sobre la interfaz de usuario del servicio de consulta](./overview.md).

## Primeros pasos {#getting-started}

[!DNL Query Editor] proporciona una ejecución flexible de consultas conectándose a [!DNL Query Service], y las consultas solo se ejecutarán mientras esta conexión esté activa.

### Conexión a [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] tarda unos segundos en inicializarse y conectarse a [!DNL Query Service] cuando se abra. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, se retrasa la ejecución hasta que se complete la conexión.

![Imagen](../images/ui/query-editor/connect.png)

### Cómo se ejecutan las consultas desde [!DNL Query Editor] {#run-a-query}

Consultas ejecutadas desde [!DNL Query Editor] se ejecuta de forma interactiva. Esto significa que si cierra el explorador o se va, la consulta se cancela. Esto también se aplica a las consultas realizadas para generar conjuntos de datos a partir de resultados de consultas.

## Creación de consultas mediante [!DNL Query Editor] {#query-authoring}

Uso [!DNL Query Editor], puede escribir, ejecutar y guardar consultas para datos de experiencias del cliente. Todas las consultas ejecutadas o guardadas en [!DNL Query Editor] están disponibles para todos los usuarios de su organización con acceso a [!DNL Query Service].

### Acceso [!DNL Query Editor] {#accessing-query-editor}

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Consultas]** en el menú de navegación de la izquierda para abrir [!DNL Query Service] espacio de trabajo. A continuación, seleccione **[!UICONTROL Crear consulta]** en la parte superior derecha de la pantalla para comenzar a escribir consultas. Este vínculo está disponible desde cualquiera de las páginas de la sección [!DNL Query Service] espacio de trabajo.

![Imagen](../images/ui/query-editor/create-query.png)

### Escritura de consultas {#writing-queries}

[!UICONTROL Editor de consultas] está organizado para que la escritura de consultas sea lo más sencilla posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con la variable **Play** y campo de entrada SQL resaltado.

![Imagen](../images/ui/query-editor/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar las consultas con límites en las filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, elimine los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida .

### Herramientas de escritura en [!DNL Query Editor] {#writing-tools}

- **Resaltado de sintaxis automático:** Facilita la lectura y organización de SQL.

![Imagen](../images/ui/query-editor/syntax-highlight.png)

- **Palabra clave SQL autocompletada:** Comience a escribir la consulta, utilice las teclas de flecha para ir al término deseado y pulse **Entrar**.

![Imagen](../images/ui/query-editor/syntax-auto.png)

- **Tabla y campo autocompletados:** Comience a escribir el nombre de tabla que desee `SELECT` en , utilice las teclas de flecha para desplazarse hasta la tabla que está buscando y pulse **Entrar**. Una vez seleccionada una tabla, el llenado automático reconocerá los campos de dicha tabla.

![Imagen](../images/ui/query-editor/tables-auto.png)

### Detección de errores {#error-detection}

[!DNL Query Editor] valida automáticamente una consulta a medida que la escribe, proporcionando validación SQL genérica y validación de ejecución específica. Si aparece un subrayado rojo debajo de la consulta (como se muestra en la imagen siguiente), representa un error dentro de la consulta.

![Imagen](../images/ui/query-editor/syntax-error-highlight.png)

Cuando se detectan errores, se pueden ver los mensajes de error específicos pasando el cursor sobre el código SQL.

![Imagen](../images/ui/query-editor/linting-error.png)

### Detalles de la consulta {#query-details}

Mientras está viendo una consulta en [!DNL Query Editor], el **[!UICONTROL Detalles de la consulta]** proporciona herramientas para administrar la consulta seleccionada.

![Imagen](../images/ui/query-editor/query-details.png)

Este panel le permite generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada y agregar una programación a la consulta.

Este panel también muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde. Para generar un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos de salida]**. La variable **[!UICONTROL Conjunto de datos de salida]** se abre. Introduzca un nombre y una descripción y, a continuación, seleccione **[!UICONTROL Ejecutar consulta]**. El nuevo conjunto de datos se muestra en la **[!UICONTROL Conjuntos de datos]** en la ficha [!DNL Query Service] interfaz de usuario activada [!DNL Platform].

### Consultas programadas {#scheduled-queries}

>[!IMPORTANT]
>
>A continuación se muestra una lista de limitaciones para las consultas programadas al utilizar el Editor de consultas. No se aplican al [!DNL Query Service] API:<br/>Solo puede añadir una programación a una consulta que ya se haya creado, guardado y ejecutado.<br/>You **cannot** agregue una programación a una consulta parametrizada.<br/>Consultas programadas **cannot** contiene un bloque anónimo.

Para añadir una programación a una consulta, seleccione **[!UICONTROL Agregar programación]**.

![Imagen](../images/ui/query-editor/add-schedule.png)

La variable **[!UICONTROL Detalles de la programación]** se abre. En esta página, puede elegir la frecuencia de la consulta programada, las fechas en las que se ejecutará la consulta programada y el conjunto de datos al que exportar la consulta.

![Imagen](../images/ui/query-editor/schedule-details.png)

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

Después de confirmar todos estos detalles, seleccione **[!UICONTROL Guardar]** para crear una programación.

La página de detalles de la consulta vuelve a aparecer y ahora muestra los detalles de la programación recién creada, incluido el ID de programación, la propia programación y el conjunto de datos de salida de la programación. Puede utilizar el ID de programación para buscar más información sobre las ejecuciones de la propia consulta programada. Para obtener más información, lea la [guía de extremos de ejecución de consultas programadas](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> Solo se puede programar **one** plantilla de consulta mediante la interfaz de usuario. Si desea agregar programaciones adicionales a una plantilla de consulta, deberá utilizar la API . Si ya se ha agregado una programación mediante la API de , **not** poder agregar programaciones adicionales mediante la interfaz de usuario de . Si ya hay varias programaciones adjuntas a una plantilla de consulta, solo se mostrará la programación más antigua. Para aprender a añadir programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).
>
> Además, debe actualizar la página si desea asegurarse de que tiene el estado más reciente de la programación que está viendo.

#### Eliminar una programación {#delete-schedule}

Para eliminar una programación, seleccione **[!UICONTROL Eliminar una programación]**.

![Imagen](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> Si desea eliminar una programación para una consulta, primero debe deshabilitarla.

### Almacenamiento de consultas {#saving-queries}

[!DNL Query Editor] proporciona una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Para guardar una consulta, seleccione **[!UICONTROL Guardar]** en la esquina superior derecha de [!DNL Query Editor]. Para poder guardar una consulta, debe proporcionarse un nombre para la consulta mediante la variable **[!UICONTROL Detalles de la consulta]** panel.

### Búsqueda de consultas anteriores {#previous-queries}

Todas las consultas ejecutadas desde [!DNL Query Editor] se capturan en la tabla Registro . Puede utilizar la funcionalidad de búsqueda en la variable **[!UICONTROL Registro]** para buscar ejecuciones de consulta. Las consultas guardadas se enumeran en el **[!UICONTROL Examinar]** pestaña .

Consulte la [Información general sobre la interfaz de usuario del servicio de consulta](./overview.md) para obtener más información.

>[!NOTE]
>
>El registro no guarda las consultas que no se ejecutan. Para que la consulta esté disponible en [!DNL Query Service], debe ejecutarse o guardarse en [!DNL Query Editor].

## Ejecución de consultas mediante el Editor de consultas {#executing-queries}

Para ejecutar una consulta en [!DNL Query Editor], puede introducir SQL en el editor o cargar una consulta anterior desde el **[!UICONTROL Registro]** o **[!UICONTROL Examinar]** y seleccione **Play**. El estado de la ejecución de la consulta se muestra en la variable **[!UICONTROL Consola]** y los datos de salida se muestran en la pestaña **[!UICONTROL Resultados]** pestaña .

### Consola {#console}

La consola proporciona información sobre el estado y el funcionamiento de [!DNL Query Service]. La consola muestra el estado de conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error que resulten de esas consultas.

![Imagen](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La consola solo muestra los errores resultantes de la ejecución de una consulta. No muestra errores de validación de consultas antes de ejecutar una consulta.

### Resultados de la consulta {#query-results}

Una vez finalizada la consulta, los resultados se muestran en la variable **[!UICONTROL Resultados]** junto a la pestaña **[!UICONTROL Consola]** pestaña . Esta vista muestra el resultado tabular de la consulta, mostrando hasta 100 filas. Esta vista le permite verificar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, elimine los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida . Consulte la [tutorial generación de conjuntos de datos](./create-datasets.md) para obtener instrucciones sobre cómo generar un conjunto de datos a partir de resultados de consulta en [!DNL Query Editor].

![Imagen](../images/ui/query-editor/query-results.png)

## Ejecutar consultas con [!DNL Query Service] videotutorial {#query-tutorial-video}

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente PSQL. Además, se muestran el uso de propiedades individuales en un objeto XDM, el uso de funciones definidas por Adobe y el uso de CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Pasos siguientes

Ahora sabe qué características están disponibles en [!DNL Query Editor] y cómo navegar por la aplicación, puede empezar a crear sus propias consultas directamente en [!DNL Platform]. Para obtener más información sobre cómo ejecutar consultas SQL con conjuntos de datos en [!DNL Data Lake], consulte la guía de [ejecución de consultas](../best-practices/writing-queries.md).
