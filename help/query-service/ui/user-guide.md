---
keywords: Experience Platform;home;popular topics;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Guía del usuario del Editor de consultas
topic: query editor
description: El Editor de consultas es una herramienta interactiva proporcionada por el servicio de Consulta de Adobe Experience Platform, que le permite escribir, validar y ejecutar consultas para los datos de experiencia del cliente en la interfaz de usuario de Experience Platform. El Editor de consultas admite el desarrollo de consultas para la análisis y la exploración de datos, y permite ejecutar consultas interactivas para fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en Experience Platform.
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# [!DNL Query Editor] guía del usuario

[!DNL Query Editor] es una herramienta interactiva proporcionada por Adobe Experience Platform [!DNL Query Service], que le permite escribir, validar y ejecutar consultas para los datos de experiencia del cliente en la interfaz de [!DNL Experience Platform] usuario. [!DNL Query Editor] admite el desarrollo de consultas para la análisis y la exploración de datos, y le permite ejecutar consultas interactivas para fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en [!DNL Experience Platform].

Para obtener más información sobre los conceptos y las características de [!DNL Query Service], consulte la descripción general [del servicio de][query-service-overview]Consulta. Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de Consulta en [!DNL Platform], consulte la descripción general [de la interfaz de usuario del servicio de][query-service-ui]Consulta.

## Primeros pasos

[!DNL Query Editor] proporciona una ejecución flexible de consultas mediante la conexión a [!DNL Query Service], y las consultas solo se ejecutarán mientras esta conexión esté activa.

### Conexión a [!DNL Query Service]

[!DNL Query Editor] tarda unos segundos en inicializarse y conectarse [!DNL Query Service] cuando se abre. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, se retrasa la ejecución hasta que se complete la conexión.

![Imagen](../images/queries/query-editor-overview/initializing-connection.png)

### Cómo se ejecutan las consultas desde [!DNL Query Editor]

Consultas ejecutadas desde [!DNL Query Editor] ejecución interactiva. Esto significa que si cierra el explorador o se desplaza, la consulta se cancela. Esto también se aplica a las consultas realizadas para generar conjuntos de datos a partir de resultados de consulta.

## Creación de consultas mediante [!DNL Query Editor]

Con [!DNL Query Editor], puede escribir, ejecutar y guardar consultas para los datos de experiencia del cliente. Todas las consultas ejecutadas [!DNL Query Editor]o guardadas están disponibles para todos los usuarios de la organización con acceso a [!DNL Query Service].

### Acceso [!DNL Query Editor]

En la [!DNL Experience Platform] interfaz de usuario, haga clic en **[!UICONTROL Consultas]** en el menú de navegación de la izquierda para abrir el [!DNL Query Service] espacio de trabajo. A continuación, haga clic en **[!UICONTROL Crear Consulta]** en la parte superior derecha de la pantalla para escribir consultas en inicio. Este vínculo está disponible desde cualquiera de las páginas del [!DNL Query Service] espacio de trabajo.

![Imagen](../images/queries/query-editor-overview/create-query.png)

### Escritura de consultas

[!UICONTROL El Editor] de consultas está organizado para que la escritura de consultas sea lo más fácil posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con el botón **Reproducir** y el campo de entrada SQL resaltados.

![Imagen](../images/queries/query-editor-overview/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar sus consultas con límites en las filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, elimine los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado.

### Escritura de herramientas en [!DNL Query Editor]

- **Resaltado de sintaxis automático:** Facilita la lectura y organización de SQL.

![Imagen](../images/queries/query-editor-overview/syntax-highlight.png)

- **Autocompletar palabra clave de SQL:** Inicio escribiendo la consulta y, a continuación, utilice las teclas de flecha para desplazarse hasta el término deseado y pulse **Intro**.

![Imagen](../images/queries/query-editor-overview/syntax-auto.png)

- **Autocompletar tabla y campo:** Inicio escribiendo el nombre de la tabla desde la que desea `SELECT` escribir, utilice las teclas de flecha para desplazarse a la tabla que está buscando y pulse **Intro**. Una vez seleccionada una tabla, el llenado automático reconocerá los campos de esa tabla.

![Imagen](../images/queries/query-editor-overview/tables-auto.png)

### Detección de errores

[!DNL Query Editor] valida automáticamente una consulta a medida que la escribe, proporcionando una validación genérica de SQL y una validación de ejecución específica. Si aparece un subrayado rojo debajo de la consulta (como se muestra en la imagen siguiente), representa un error dentro de la consulta.

![Imagen](../images/queries/query-editor-overview/syntax-error-highlight.png)

Cuando se detectan errores, puede realizar la vista de los mensajes de error específicos pasando el ratón sobre el código SQL.

![Imagen](../images/queries/query-editor-overview/linting-error.png)

### Detalles de consulta

Mientras visualiza una consulta en [!DNL Query Editor], el panel Detalles **[!UICONTROL de la]** Consulta proporciona herramientas para administrar la consulta seleccionada.

![Imagen](../images/queries/query-editor-overview/query-details.png)

Este panel le permite generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada y realizar la vista del código SQL en un formato fácil de copiar en la ficha Consulta **** SQL. Este panel también muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde. Para generar un conjunto de datos, haga clic en **[!UICONTROL Conjunto de datos]** de salida. Aparecerá el cuadro de diálogo **[!UICONTROL Conjunto de datos]** de salida. Escriba un nombre y una descripción y, a continuación, haga clic en **[!UICONTROL Ejecutar Consulta]**. El nuevo conjunto de datos se muestra en la ficha **[!UICONTROL Conjuntos]** de datos de la interfaz de [!DNL Query Service] usuario de [!DNL Platform].

### Guardar consultas

[!DNL Query Editor] proporciona una función save que le permite guardar una consulta y trabajar en ella más tarde. Para guardar una consulta, haga clic en **[!UICONTROL Guardar]** en la esquina superior derecha de [!DNL Query Editor]. Antes de guardar una consulta, debe proporcionar un nombre para la consulta mediante el panel Detalles **[!UICONTROL de]** Consulta.

### Cómo encontrar consultas anteriores

Todas las consultas ejecutadas desde [!DNL Query Editor] se capturan en la tabla Registro. Puede utilizar la funcionalidad de búsqueda de la ficha **[!UICONTROL Registro]** para buscar ejecuciones de consulta. Las consultas guardadas se muestran en la ficha **[!UICONTROL Examinar]** .

Consulte la descripción general [de la interfaz de usuario del servicio de][query-service-ui] Consulta para obtener más información.

>[!NOTE]
>
>El registro no guarda las consultas que no se ejecutan. Para que la consulta esté disponible en [!DNL Query Service], debe ejecutarse o guardarse en [!DNL Query Editor].

## Ejecución de consultas mediante el Editor de Consultas

Para ejecutar una consulta en [!DNL Query Editor], puede introducir SQL en el editor o cargar una consulta anterior desde la ficha **[!UICONTROL Registro]** o **[!UICONTROL Examinar]** y hacer clic en **Reproducir**. El estado de la ejecución de la consulta se muestra en la ficha **[!UICONTROL Consola]** que aparece a continuación y los datos de salida se muestran en la ficha **[!UICONTROL Resultados]** .

### Consola

La consola proporciona información sobre el estado y el funcionamiento de [!DNL Query Service]. La consola muestra el estado de la conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error que se derivan de dichas consultas.

![Imagen](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>La consola solo muestra los errores que se han producido al ejecutar una consulta. No muestra errores de validación de consulta antes de ejecutar una consulta.

### Resultados de consulta

Una vez finalizada la consulta, los resultados se muestran en la ficha **[!UICONTROL Resultados]** , junto a la ficha **[!UICONTROL Consola]** . Esta vista muestra el resultado tabular de la consulta, mostrando hasta 100 filas. Esta vista le permite comprobar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, elimine los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado. Consulte el tutorial [][query-service-create-datasets] Generación de conjuntos de datos para obtener instrucciones sobre cómo generar un conjunto de datos a partir de resultados de consulta en [!DNL Query Editor].

![Imagen](../images/queries/query-editor-overview/query-results.png)

## Ejecución de consultas con [!DNL Query Service] vídeo de tutorial

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente PSQL. Además, se muestran el uso de propiedades individuales en un objeto XDM, el uso de funciones definidas por Adobe y el uso de CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Pasos siguientes

Ahora que sabe en qué funciones se encuentran disponibles [!DNL Query Editor] y cómo navegar por la aplicación, puede crear inicios para crear sus propias consultas directamente en [!DNL Platform]. Para obtener más información sobre cómo ejecutar consultas SQL con conjuntos de datos en [!DNL Data Lake], consulte la guía sobre cómo [ejecutar consultas][query-service-running-queries]. Para obtener consultas SQL de muestra para trabajar con datos de Adobe Analytics y Adobe Target, consulte la referencia [de consultas de][query-service-sample-queries]ejemplo.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
