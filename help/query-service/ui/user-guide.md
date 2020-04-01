---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del editor de Consultas del servicio de Consulta de Adobe Experience Platform
topic: query editor
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Guía del usuario del Editor de Consultas

El Editor de Consultas es una herramienta interactiva proporcionada por el servicio de Consulta de la plataforma de experiencia de Adobe, que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de usuario de la plataforma de experiencia. El Editor de Consultas admite el desarrollo de consultas para la análisis y la exploración de datos, y permite ejecutar consultas interactivas para fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en la plataforma de experiencia.

Para obtener más información sobre los conceptos y las características del servicio de Consulta, consulte la descripción general [del servicio de][query-service-overview]Consulta. Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de Consulta en la plataforma, consulte la descripción general [de la interfaz de usuario del servicio de][query-service-ui]Consulta.

## Primeros pasos

El Editor de Consultas proporciona una ejecución flexible de consultas mediante la conexión al servicio de Consulta, y las consultas solo se ejecutarán mientras esta conexión esté activa.

### Conexión al servicio de Consulta

El Editor de Consultas tarda unos segundos en inicializarse y conectarse al servicio de Consulta cuando se abre. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, se retrasa la ejecución hasta que se complete la conexión.

![Imagen](../images/queries/query-editor-overview/initializing-connection.png)

### Ejecución de consultas desde el Editor de Consultas

Las Consultas ejecutadas desde el Editor de Consultas se ejecutan de forma interactiva. Esto significa que si cierra el explorador o se desplaza, la consulta se cancela. Esto también se aplica a las consultas realizadas para generar conjuntos de datos a partir de resultados de consulta.

## Creación de Consultas mediante el Editor de Consultas

Con el Editor de Consultas, puede escribir, ejecutar y guardar consultas para los datos de experiencia del cliente. Todas las consultas ejecutadas en el Editor de Consultas, o guardadas, están disponibles para todos los usuarios de la organización con acceso al servicio de Consulta.

### Acceso al Editor de Consultas

En la interfaz de usuario de la plataforma de experiencia, haga clic en **Consultas** en el menú de navegación de la izquierda para abrir el espacio de trabajo del servicio de Consulta. A continuación, haga clic en **Crear Consulta** en la parte superior derecha de la pantalla para escribir consultas en inicio. Este vínculo está disponible desde cualquiera de las páginas del espacio de trabajo del servicio de Consulta.

![Imagen](../images/queries/query-editor-overview/create-query.png)

### Escritura de consultas

El Editor de Consultas está organizado para que la escritura de consultas sea lo más fácil posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con el botón **Reproducir** y el campo de entrada SQL resaltados.

![Imagen](../images/queries/query-editor-overview/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar sus consultas con límites en las filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, elimine los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado.

### Escritura de herramientas en el Editor de Consultas

- **Resaltado de sintaxis automático:** Facilita la lectura y organización de SQL.

![Imagen](../images/queries/query-editor-overview/syntax-highlight.png)

- **Autocompletar palabra clave de SQL:** Inicio escribiendo la consulta y, a continuación, utilice las teclas de flecha para desplazarse hasta el término deseado y pulse **Intro**.

![Imagen](../images/queries/query-editor-overview/syntax-auto.png)

- **Autocompletar tabla y campo:** Inicio escribiendo el nombre de la tabla desde la que desea `SELECT` escribir, utilice las teclas de flecha para desplazarse a la tabla que está buscando y pulse **Intro**. Una vez seleccionada una tabla, el llenado automático reconocerá los campos de esa tabla.

![Imagen](../images/queries/query-editor-overview/tables-auto.png)

### Detección de errores

El Editor de Consultas valida automáticamente una consulta a medida que la escribe, proporcionando una validación genérica de SQL y una validación de ejecución específica. Si aparece un subrayado rojo debajo de la consulta (como se muestra en la imagen siguiente), representa un error dentro de la consulta.

![Imagen](../images/queries/query-editor-overview/syntax-error-highlight.png)

Cuando se detectan errores, puede realizar la vista de los mensajes de error específicos pasando el ratón sobre el código SQL.

![Imagen](../images/queries/query-editor-overview/linting-error.png)

### Detalles de Consulta

Mientras visualiza una consulta en el Editor de Consultas, el panel Detalles *de la* Consulta proporciona herramientas para administrar la consulta seleccionada.

![Imagen](../images/queries/query-editor-overview/query-details.png)

Este panel le permite generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada y realizar la vista del código SQL en un formato fácil de copiar en la ficha Consulta ** SQL. Este panel también muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde. Para generar un conjunto de datos, haga clic en **Conjunto de datos** de salida. Aparecerá el cuadro de diálogo *Conjunto de datos* de salida. Escriba un nombre y una descripción y, a continuación, haga clic en **Ejecutar Consulta**. El nuevo conjunto de datos se muestra en la ficha *Conjuntos* de datos de la interfaz de usuario del servicio de Consulta en la plataforma.

### Guardar consultas

El Editor de Consultas proporciona una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Para guardar una consulta, haga clic en **Guardar** en la esquina superior derecha del Editor de Consultas. Antes de guardar una consulta, debe proporcionar un nombre para la consulta mediante el panel Detalles *de* Consulta.

### Cómo encontrar consultas anteriores

Todas las consultas ejecutadas desde el Editor de Consultas se capturan en la tabla Registro. Puede utilizar la funcionalidad de búsqueda de la ficha *Registro* para buscar ejecuciones de consulta. Las consultas guardadas se muestran en la ficha *Examinar* .

Consulte la descripción general [de la interfaz de usuario del servicio de][query-service-ui] Consulta para obtener más información.

>[!NOTE] El registro no guarda las Consultas que no se ejecutan. Para que la consulta esté disponible en el servicio de Consulta, debe ejecutarse o guardarse en el Editor de Consultas.

## Ejecución de consultas mediante el Editor de Consultas

Para ejecutar una consulta en el Editor de Consultas, puede introducir SQL en el editor o cargar una consulta anterior desde la ficha *Registro* o *Examinar* y hacer clic en **Reproducir**. El estado de la ejecución de la consulta se muestra en la ficha *Consola* que aparece a continuación y los datos de salida se muestran en la ficha *Resultados* .

### Consola

La consola proporciona información sobre el estado y el funcionamiento del servicio de Consulta. La consola muestra el estado de la conexión al servicio de Consulta, las operaciones de consulta que se están ejecutando y los mensajes de error que se derivan de dichas consultas.

![Imagen](../images/queries/query-editor-overview/console.png)

>[!NOTE] La consola solo muestra los errores que se han producido al ejecutar una consulta. No muestra errores de validación de consulta antes de ejecutar una consulta.

### Resultados de Consulta

Una vez finalizada la consulta, los resultados se muestran en la ficha *Resultados* , junto a la ficha *Consola* . Esta vista muestra el resultado tabular de la consulta, mostrando hasta 100 filas. Esta vista le permite comprobar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, elimine los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado. Consulte el tutorial [][query-service-create-datasets] Generación de conjuntos de datos para obtener instrucciones sobre cómo generar un conjunto de datos a partir de resultados de consulta en el Editor de Consultas.

![Imagen](../images/queries/query-editor-overview/query-results.png)

## Pasos siguientes

Ahora que sabe qué funciones están disponibles en el Editor de Consultas y cómo navegar por la aplicación, puede crear inicios para sus propias consultas directamente en Platform. Para obtener más información sobre cómo ejecutar consultas SQL con conjuntos de datos en Data Lake, consulte la guía sobre cómo [ejecutar consultas][query-service-running-queries]. Para obtener consultas SQL de muestra para trabajar con datos de Adobe Analytics y Adobe Destinatario, consulte la referencia [de consultas de][query-service-sample-queries]ejemplo.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
