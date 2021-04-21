---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta;editor de consultas;editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de consulta
topic-legacy: guide
description: El servicio de consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de la organización de IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 2%

---

# [!DNL Query Service] guía

Adobe Experience Platform [!DNL Query Service] proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de su organización de IMS. Para acceder a la IU dentro de [Adobe Experience Platform][platform-ui], seleccione **[!UICONTROL Queries]** en el panel de navegación izquierdo.

## [!DNL Query Editor]

El [!DNL Query Editor] permite escribir y ejecutar consultas sin utilizar un cliente externo. Haga clic en **[!UICONTROL Create Query]** para abrir [!DNL Query Editor] y crear una nueva consulta. También puede acceder a [!DNL Query Editor] seleccionando una consulta en las pestañas **[!UICONTROL Log]** o **[!UICONTROL Browse]** . Si se selecciona una consulta guardada o ejecutada anteriormente, se abrirá [!DNL Query Editor] y se mostrará el SQL de la consulta seleccionada.

![Imagen](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] proporciona espacio de edición donde puede empezar a escribir una consulta. A medida que escribe, el editor completa automáticamente las palabras, tablas y nombres de campo reservados SQL dentro de las tablas. Cuando termine de escribir la consulta, haga clic en el botón **Play** para ejecutarla. La pestaña **[!UICONTROL Console]** situada debajo del editor muestra lo que [!DNL Query Service] está haciendo actualmente, lo que indica cuándo se ha devuelto una consulta. La pestaña **[!UICONTROL Result]**, junto a la consola, muestra los resultados de la consulta. Consulte la [guía del Editor de consultas][query-editor] para obtener más información sobre el uso de [!DNL Query Editor].

![Imagen](../images/queries/ui-overview/query-editor.png)

## Examinar

La pestaña **[!UICONTROL Browse]** muestra las consultas guardadas por los usuarios de su organización. Es útil considerar estos proyectos como proyectos de consulta, ya que las consultas guardadas aquí pueden estar aún en construcción. Las consultas mostradas en la pestaña **[!UICONTROL Browse]** también se muestran como consultas de ejecución en la pestaña **[!UICONTROL Log]** si ya las ha ejecutado [!DNL Query Service].

![Imagen](../images/queries/ui-overview/browse.png)

| Columna | Descripción |
| --- | --- |
| Nombre | El nombre de consulta creado por el usuario. Puede hacer clic en el nombre para abrir la consulta en [!DNL Query Editor]. También puede utilizar la barra de búsqueda para buscar en el Nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| SQL | Los primeros caracteres de la consulta SQL. Al pasar el ratón por encima del código, se muestra la consulta completa. |
| Modificado por | El último usuario que modificó la consulta. Cualquier usuario de su organización con acceso a [!DNL Query Service] puede modificar consultas. |
| Última modificación | La fecha y hora de la última modificación de la consulta, en el huso horario del explorador. |

## Registro

La pestaña **[!UICONTROL Log]** proporciona una lista de consultas que se han ejecutado anteriormente. De forma predeterminada, el registro enumera las consultas en cronología inversa.

![Imagen](../images/queries/ui-overview/log.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Name]** | El nombre de la consulta, que consta de los primeros varios caracteres de la consulta SQL. Al hacer clic en el nombre se abre [!DNL Query Editor], lo que permite editar la consulta. Puede utilizar la barra de búsqueda para buscar en el Nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL Created By]** | El nombre de la persona que creó la consulta. |
| **[!UICONTROL Client]** | El cliente utilizado para la consulta. |
| **[!UICONTROL Dataset]** | El conjunto de datos de entrada utilizado por la consulta. Haga clic en el conjunto de datos para ir a la pantalla de detalles del conjunto de datos de entrada. |
| **[!UICONTROL Status]** | Estado actual de la consulta. |
| **[!UICONTROL Last Run]** | La última vez que se ejecutó la consulta. Para ordenar la lista en orden ascendente o descendente, haga clic en la flecha situada sobre esta columna. |
| **[!UICONTROL Run Time]** | Cantidad de tiempo que se tardó en ejecutar la consulta. |

## Credenciales

La pestaña **[!UICONTROL Credentials]** muestra sus credenciales [!DNL Postgres]. Haga clic en el icono **[!UICONTROL Copy]** situado junto a cualquier campo para almacenar su contenido en el búfer del teclado. Para obtener más información sobre cómo utilizar estas credenciales para conectarse con clientes externos, lea la [guía de conexión con clientes][connect-clients].

![Imagen](../images/queries/ui-overview/credentials.png)

## Pasos siguientes

Ahora que está familiarizado con la interfaz de usuario [!DNL Query Service] en [!DNL Platform], puede acceder a [!DNL Query Editor] para empezar a crear sus propios proyectos de consulta y compartirlos con otros usuarios de su organización. Para obtener más información sobre la creación y ejecución de consultas en [!DNL Query Editor], consulte la [Guía del usuario del Editor de consultas][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
