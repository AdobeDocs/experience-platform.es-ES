---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de Consulta de Adobe Experience Platform
topic: guide
description: El servicio de Consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 3%

---


# [!DNL Query Service] guía

El Adobe Experience Platform [!DNL Query Service] proporciona una interfaz de usuario que se puede utilizar para escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS. Para acceder a la interfaz de usuario de [Adobe Experience Platform][platform-ui], seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo.

## [!DNL Query Editor]

El [!DNL Query Editor] permite escribir y ejecutar consultas sin utilizar un cliente externo. Haga clic en **[!UICONTROL Crear Consulta]** para abrir la [!DNL Query Editor] y crear una nueva consulta. También puede acceder al [!DNL Query Editor] seleccionando una consulta en las fichas **[!UICONTROL Registro]** o **[!UICONTROL Examinar]** . Al seleccionar una consulta previamente ejecutada o guardada, se abrirá el [!DNL Query Editor] y se mostrará el SQL para la consulta seleccionada.

![Imagen](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] proporciona espacio de edición en el que puede empezar a escribir una consulta. A medida que escribe, el editor completa automáticamente las palabras reservadas, tablas y nombres de campo SQL en las tablas. Cuando termine de escribir la consulta, haga clic en el botón **Reproducir** para ejecutar la consulta. La ficha **[!UICONTROL Consola]** debajo del editor muestra lo que [!DNL Query Service] se está haciendo actualmente, indicando cuándo se ha devuelto una consulta. La ficha **[!UICONTROL Resultado]** , junto a la consola, muestra los resultados de la consulta. Consulte la guía [del Editor de][query-editor] Consultas para obtener más información sobre el uso de [!DNL Query Editor].

![Imagen](../images/queries/ui-overview/query-editor.png)

## Examinar

La ficha **[!UICONTROL Examinar]** muestra las consultas guardadas por los usuarios de la organización. Es útil considerarlos proyectos de consulta, ya que las consultas guardadas aquí todavía pueden estar en construcción. Las consultas que se muestran en la ficha **[!UICONTROL Examinar]** también se muestran como consultas de ejecución en la ficha **[!UICONTROL Registro]** si ya las ha ejecutado anteriormente [!DNL Query Service].

![Imagen](../images/queries/ui-overview/browse.png)

| Columna | Descripción |
| --- | --- |
| Nombre | El nombre de la consulta creada por el usuario. Puede hacer clic en el nombre para abrir la consulta en la [!DNL Query Editor]. También puede utilizar la barra de búsqueda para buscar el nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| SQL | Los primeros caracteres de la consulta SQL. Al pasar el ratón sobre el código se muestra la consulta completa. |
| Modificado por | Último usuario que modificó la consulta. Cualquier usuario de su organización con acceso a [!DNL Query Service] puede modificar consultas. |
| Última modificación | Fecha y hora de la última modificación de la consulta, en el huso horario del explorador. |

## Registro

La ficha **[!UICONTROL Registro]** proporciona una lista de consultas que se han ejecutado anteriormente. De forma predeterminada, el registro lista las consultas en la cronología inversa.

![Imagen](../images/queries/ui-overview/log.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El nombre de la consulta, que consta de los primeros caracteres de la consulta SQL. Al hacer clic en el nombre, se abre el [!DNL Query Editor], lo que permite editar la consulta. Puede utilizar la barra de búsqueda para buscar el nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL Creado por]** | Nombre de la persona que creó la consulta. |
| **[!UICONTROL Cliente]** | El cliente utilizado para la consulta. |
| **[!UICONTROL Conjunto de datos]** | Conjunto de datos de entrada utilizado por la consulta. Haga clic en el conjunto de datos para ir a la pantalla de detalles del conjunto de datos de entrada. |
| **[!UICONTROL Estado]** | Estado actual de la consulta. |
| **[!UICONTROL Última ejecución]** | La última vez que se ejecutó la consulta. Puede ordenar la lista en orden ascendente o descendente haciendo clic en la flecha que hay sobre esta columna. |
| **[!UICONTROL Tiempo de ejecución]** | La cantidad de tiempo que tardó en ejecutarse la consulta. |

## Credenciales

La ficha **[!UICONTROL Credenciales]** muestra sus [!DNL Postgres] credenciales. Haga clic en el icono **[!UICONTROL Copiar]** situado junto a cualquier campo para almacenar su contenido en el búfer de teclado. Para obtener más información sobre cómo utilizar estas credenciales para conectarse con clientes externos, lea la guía [][connect-clients]Conectar con clientes.

![Imagen](../images/queries/ui-overview/credentials.png)

## Pasos siguientes

Ahora que está familiarizado con [!DNL Query Service] la interfaz de usuario en [!DNL Platform], puede acceder [!DNL Query Editor] a inicio creando sus propios proyectos de consulta para compartirlos con otros usuarios de su organización. Para obtener más información sobre la creación y ejecución de consultas en [!DNL Query Editor], consulte la guía [de usuario del Editor de][query-editor]Consultas.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
