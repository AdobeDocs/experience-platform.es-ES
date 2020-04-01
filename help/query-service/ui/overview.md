---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de Consulta de Adobe Experience Platform
topic: guide
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Guía del servicio de Consulta

El servicio de Consulta de la plataforma de experiencia de Adobe proporciona una interfaz de usuario que se puede utilizar para escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS. Para acceder a la interfaz de usuario dentro de [Adobe Experience Platform][platform-ui], seleccione **Consultas** en el panel de navegación izquierdo.

## Editor de Consultas

El Editor de Consultas permite escribir y ejecutar consultas sin utilizar un cliente externo. Haga clic en **Crear Consulta** para abrir el Editor de Consultas y crear una nueva consulta. También puede acceder al Editor de Consultas seleccionando una consulta en las fichas *Registro* o *Examinar* . Al seleccionar una consulta previamente ejecutada o guardada, se abrirá el Editor de Consultas y se mostrará el SQL de la consulta seleccionada.

![Imagen](../images/queries/ui-overview/overview.png)

El Editor de Consultas proporciona un espacio de edición en el que puede empezar a escribir una consulta. A medida que escribe, el editor completa automáticamente las palabras reservadas, tablas y nombres de campo SQL en las tablas. Cuando termine de escribir la consulta, haga clic en **Reproducir** para ejecutar la consulta. La ficha *Consola* que se encuentra debajo del editor muestra qué está haciendo actualmente el servicio de Consulta, indicando cuándo se ha devuelto una consulta. La ficha *Resultado* , junto a la consola, muestra los resultados de la consulta. Consulte la guía [Editor de][query-editor] Consultas para obtener más información sobre el uso del editor de consultas.

![Imagen](../images/queries/ui-overview/query-editor.png)

## Examinar

La ficha *Examinar* muestra las consultas guardadas por los usuarios de la organización. Es útil considerarlos proyectos de consulta, ya que las consultas guardadas aquí todavía pueden estar en construcción. Las Consultas que se muestran en la ficha *Examinar* también se muestran como consultas de ejecución en la ficha *Registro* si el servicio de Consulta las ha ejecutado anteriormente.

![Imagen](../images/queries/ui-overview/browse.png)

| Columna | Descripción |
| --- | --- |
| Nombre | El nombre de la consulta creada por el usuario. Puede hacer clic en el nombre para abrir la consulta en el Editor de Consultas. También puede utilizar la barra de búsqueda para buscar el nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| SQL | Los primeros caracteres de la consulta SQL. Al pasar el ratón sobre el código se muestra la consulta completa. |
| Modificado por | Último usuario que modificó la consulta. Cualquier usuario de su organización con acceso al servicio de Consulta puede modificar consultas. |
| Última modificación | Fecha y hora de la última modificación de la consulta, en el huso horario del explorador. |

## Registro

La ficha *Registro* proporciona una lista de consultas que se han ejecutado anteriormente. De forma predeterminada, el registro lista las consultas en la cronología inversa.

![Imagen](../images/queries/ui-overview/log.png)

| Columna | Descripción |
| --- | --- |
| Nombre | El nombre de la consulta, que consta de los primeros caracteres de la consulta SQL. Al hacer clic en el nombre, se abre el Editor de Consultas, que permite editar la consulta. Puede utilizar la barra de búsqueda para buscar el nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| Creado por | Nombre de la persona que creó la consulta. |
| Cliente | El cliente utilizado para la consulta. |
| Conjunto de datos | Conjunto de datos de entrada utilizado por la consulta. Haga clic en el conjunto de datos para ir a la pantalla de detalles del conjunto de datos de entrada. |
| Estado | Estado actual de la consulta. |
| Última ejecución | La última vez que se ejecutó la consulta. Puede ordenar la lista en orden ascendente o descendente haciendo clic en la flecha que hay sobre esta columna. |
| Tiempo de ejecución | La cantidad de tiempo que tardó en ejecutarse la consulta. |

## Credenciales

La ficha *Credenciales* muestra las credenciales de Postgres. Haga clic en el icono **Copiar** situado junto a cualquier campo para almacenar su contenido en el búfer de teclado. Para obtener más información sobre cómo utilizar estas credenciales para conectarse con clientes externos, lea la guía [][connect-clients]Conectar con clientes.

![Imagen](../images/queries/ui-overview/credentials.png)

## Pasos siguientes

Ahora que está familiarizado con la interfaz de usuario del servicio de Consulta en la plataforma, puede acceder al Editor de Consultas para que inicio cree sus propios proyectos de consulta para compartirlos con otros usuarios de la organización. Para obtener más información sobre la creación y ejecución de consultas en el Editor de Consultas, consulte la guía del usuario del Editor de [Consultas][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
