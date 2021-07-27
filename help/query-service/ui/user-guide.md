---
keywords: Experience Platform;inicio;temas populares;editor de consultas;editor de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del Editor de consultas
topic-legacy: query editor
description: El Editor de consultas es una herramienta interactiva que proporciona el servicio de consultas de Adobe Experience Platform, que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de usuario del Experience Platform. El Editor de consultas admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 7eaa808ecc644fdb9bc6b3fe1347c7651d54a33b
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 1%

---

# [!DNL Query Editor] Guía de la interfaz de usuario

[!DNL Query Editor] es una herramienta interactiva que proporciona Adobe Experience Platform  [!DNL Query Service], que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de  [!DNL Experience Platform] usuario. [!DNL Query Editor] admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en  [!DNL Experience Platform].

Para obtener más información sobre los conceptos y características de [!DNL Query Service], consulte la [Información general del servicio de consulta](../home.md). Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de consulta en [!DNL Platform], consulte la [Información general de la interfaz de usuario del servicio de consulta](./overview.md).

## Primeros pasos

[!DNL Query Editor] proporciona una ejecución flexible de consultas mediante la conexión a  [!DNL Query Service], y las consultas solo se ejecutarán mientras esta conexión esté activa.

### Conexión a [!DNL Query Service]

[!DNL Query Editor] tardan unos segundos en inicializarse y conectarse a  [!DNL Query Service] cuando se abre. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, se retrasa la ejecución hasta que se complete la conexión.

![Imagen](../images/ui/query-editor/connect.png)

### Cómo se ejecutan las consultas desde [!DNL Query Editor]

Las consultas ejecutadas desde [!DNL Query Editor] se ejecutan de forma interactiva. Esto significa que si cierra el explorador o se va, la consulta se cancela. Esto también se aplica a las consultas realizadas para generar conjuntos de datos a partir de resultados de consultas.

## Creación de consultas mediante [!DNL Query Editor]

Con [!DNL Query Editor], puede escribir, ejecutar y guardar consultas para datos de experiencia del cliente. Todas las consultas ejecutadas en [!DNL Query Editor], o guardadas, están disponibles para todos los usuarios de la organización con acceso a [!DNL Query Service].

### Acceso [!DNL Query Editor]

En la interfaz de usuario de [!DNL Experience Platform], seleccione **[!UICONTROL Consultas]** en el menú de navegación de la izquierda para abrir el espacio de trabajo de [!DNL Query Service]. A continuación, seleccione **[!UICONTROL Create Query]** en la parte superior derecha de la pantalla para comenzar a escribir consultas. Este vínculo está disponible desde cualquiera de las páginas del espacio de trabajo [!DNL Query Service] .

![Imagen](../images/ui/query-editor/create-query.png)

### Escritura de consultas

[!UICONTROL El ] Editor de consultas está organizado para que la escritura de consultas sea lo más fácil posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con el botón **Play** y el campo de entrada SQL resaltados.

![Imagen](../images/ui/query-editor/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar las consultas con límites en las filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, elimine los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado.

### Herramientas de escritura en [!DNL Query Editor]

- **Resaltado automático de sintaxis:**  facilita la lectura y organización de SQL.

![Imagen](../images/ui/query-editor/syntax-highlight.png)

- **Autocompletar palabra clave SQL:** empiece a escribir la consulta, utilice las teclas de flecha para ir al término deseado y pulse  **Intro**.

![Imagen](../images/ui/query-editor/syntax-auto.png)

- **Tabla y campo autocompletado:** empiece a escribir el nombre de tabla  `SELECT` desde el que desee, utilice las teclas de flecha para desplazarse a la tabla que busca y presione  **Intro**. Una vez seleccionada una tabla, el llenado automático reconocerá los campos de dicha tabla.

![Imagen](../images/ui/query-editor/tables-auto.png)

### Detección de errores

[!DNL Query Editor] valida automáticamente una consulta a medida que la escribe, proporcionando validación SQL genérica y validación de ejecución específica. Si aparece un subrayado rojo debajo de la consulta (como se muestra en la imagen siguiente), representa un error dentro de la consulta.

![Imagen](../images/ui/query-editor/syntax-error-highlight.png)

Cuando se detectan errores, se pueden ver los mensajes de error específicos pasando el cursor sobre el código SQL.

![Imagen](../images/ui/query-editor/linting-error.png)

### Detalles de la consulta

Mientras visualiza una consulta en [!DNL Query Editor], el panel **[!UICONTROL Detalles de la consulta]** proporciona herramientas para administrar la consulta seleccionada.

![Imagen](../images/ui/query-editor/query-details.png)

Este panel le permite generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada y agregar una programación a la consulta.

Este panel también muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde. Para generar un conjunto de datos, seleccione **[!UICONTROL Output Dataset]**. Aparece el cuadro de diálogo **[!UICONTROL Conjunto de datos de salida]**. Introduzca un nombre y una descripción y, a continuación, seleccione **[!UICONTROL Ejecutar consulta]**. El nuevo conjunto de datos se muestra en la pestaña **[!UICONTROL Datasets]** de la interfaz de usuario [!DNL Query Service] en [!DNL Platform].

### Consultas programadas {#scheduled-queries}

>[!NOTE]
>
> Solo puede añadir una programación a una consulta que ya se haya creado, guardado y ejecutado. Además, **not** podrá agregar una programación a una consulta parametrizada.

Para añadir una programación a una consulta, seleccione **[!UICONTROL Add schedule]**.

![Imagen](../images/ui/query-editor/add-schedule.png)

Aparece la página **[!UICONTROL Schedule details]**. En esta página, puede elegir la frecuencia de la consulta programada, las fechas en las que se ejecutará la consulta programada y el conjunto de datos al que exportar la consulta.

![Imagen](../images/ui/query-editor/schedule-details.png)

Puede elegir las siguientes opciones para **[!UICONTROL Frequency]**:

- **[!UICONTROL Por hora]**: La consulta programada se ejecutará cada hora para el período de fecha seleccionado.
- **[!UICONTROL Diario]**: La consulta programada se ejecutará cada X días a la hora y el periodo de fecha seleccionados. Tenga en cuenta que la hora seleccionada es **UTC** y no su zona horaria local.
- **[!UICONTROL Semanal]**: La consulta seleccionada se ejecutará en los días de la semana, la hora y el período de fecha seleccionado. Tenga en cuenta que la hora seleccionada es **UTC** y no su zona horaria local.
- **[!UICONTROL Mensual]**: La consulta seleccionada se ejecutará todos los meses del día, la hora y el período de fecha seleccionado. Tenga en cuenta que la hora seleccionada es **UTC** y no su zona horaria local.
- **[!UICONTROL Anual]**: La consulta seleccionada se ejecutará cada año en el día, mes, hora y período de fecha que haya seleccionado. Tenga en cuenta que la hora seleccionada es **UTC** y no su zona horaria local.

Para el conjunto de datos, tiene la opción de usar un conjunto de datos existente o crear un nuevo conjunto de datos.

>[!IMPORTANT]
>
> Como está utilizando un conjunto de datos existente o creando uno nuevo, **no** necesita incluir `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de la consulta, ya que los conjuntos de datos ya están establecidos. Si incluye `INSERT INTO` o `CREATE TABLE AS SELECT` como parte de las consultas programadas, se producirá un error.

Después de confirmar todos estos detalles, seleccione **[!UICONTROL Save]** para crear una programación.

La página de detalles de la consulta vuelve a aparecer y ahora muestra los detalles de la programación recién creada, incluido el ID de programación, la propia programación y el conjunto de datos de salida de la programación. Puede utilizar el ID de programación para buscar más información sobre las ejecuciones de la propia consulta programada. Para obtener más información, consulte la [guía de extremos de ejecución de consultas programadas](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> Solo puede programar **una** plantilla de consulta mediante la interfaz de usuario. Si desea agregar programaciones adicionales a una plantilla de consulta, deberá utilizar la API . Si ya se ha agregado una programación mediante la API, **no** se agregarán programaciones adicionales mediante la interfaz de usuario. Si ya hay varias programaciones adjuntas a una plantilla de consulta, solo se mostrará la programación más antigua. Para aprender a añadir programaciones usando la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).
>
> Además, debe actualizar la página si desea asegurarse de que tiene el estado más reciente de la programación que está viendo.

#### Eliminar una programación

Puede eliminar una programación seleccionando **[!UICONTROL Delete a schedule]**.

![Imagen](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> Si desea eliminar una programación para una consulta, primero debe deshabilitarla.

### Almacenamiento de consultas

[!DNL Query Editor] proporciona una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Para guardar una consulta, seleccione **[!UICONTROL Save]** en la esquina superior derecha de [!DNL Query Editor]. Para poder guardar una consulta, debe proporcionarse un nombre para la consulta mediante el panel **[!UICONTROL Detalles de la consulta]**.

### Búsqueda de consultas anteriores

Todas las consultas ejecutadas desde [!DNL Query Editor] se capturan en la tabla Registro. Puede utilizar la funcionalidad de búsqueda en la pestaña **[!UICONTROL Log]** para encontrar ejecuciones de consultas. Las consultas guardadas se enumeran en la pestaña **[!UICONTROL Browse]**.

Consulte la [Información general de la interfaz de usuario del servicio de consulta](./overview.md) para obtener más información.

>[!NOTE]
>
>El registro no guarda las consultas que no se ejecutan. Para que la consulta esté disponible en [!DNL Query Service], debe ejecutarse o guardarse en [!DNL Query Editor].

## Ejecución de consultas mediante el Editor de consultas

Para ejecutar una consulta en [!DNL Query Editor], puede introducir SQL en el editor o cargar una consulta anterior desde las pestañas **[!UICONTROL Log]** o **[!UICONTROL Browse]** y seleccionar **Play**. El estado de la ejecución de la consulta se muestra en la pestaña **[!UICONTROL Console]** a continuación y los datos de salida se muestran en la pestaña **[!UICONTROL Results]**.

### Consola

La consola proporciona información sobre el estado y el funcionamiento de [!DNL Query Service]. La consola muestra el estado de conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error que se deriven de esas consultas.

![Imagen](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La consola solo muestra los errores resultantes de la ejecución de una consulta. No muestra errores de validación de consultas antes de ejecutar una consulta.

### Resultados de la consulta

Una vez finalizada la consulta, los resultados se muestran en la pestaña **[!UICONTROL Results]**, junto a la pestaña **[!UICONTROL Console]**. Esta vista muestra el resultado tabular de la consulta, mostrando hasta 100 filas. Esta vista le permite verificar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, elimine los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con la salida. Consulte el [tutorial de generación de conjuntos de datos](./create-datasets.md) para obtener instrucciones sobre cómo generar un conjunto de datos a partir de resultados de consulta en [!DNL Query Editor].

![Imagen](../images/ui/query-editor/query-results.png)

## Ejecutar consultas con el tutorial en vídeo [!DNL Query Service]

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente PSQL. Además, se muestran el uso de propiedades individuales en un objeto XDM, el uso de funciones definidas por Adobe y el uso de CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Pasos siguientes

Ahora que sabe qué funciones están disponibles en [!DNL Query Editor] y cómo navegar por la aplicación, puede empezar a crear sus propias consultas directamente en [!DNL Platform]. Para obtener más información sobre la ejecución de consultas SQL con conjuntos de datos en [!DNL Data Lake], consulte la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).
