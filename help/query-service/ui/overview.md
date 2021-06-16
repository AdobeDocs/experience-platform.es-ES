---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta;editor de consultas;editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de consulta
topic-legacy: guide
description: El servicio de consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de la organización de IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 483bcea231ed5f25c76771d0acba7e0c62dfed16
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 3%

---

# [!DNL Query Service] guía

Adobe Experience Platform [!DNL Query Service] proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de su organización de IMS. Para acceder a la IU dentro de [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo.

## [!DNL Query Editor]

El [!DNL Query Editor] permite escribir y ejecutar consultas sin utilizar un cliente externo. Seleccione **[!UICONTROL Crear consulta]** para abrir la [!DNL Query Editor] y crear una nueva consulta. También puede acceder a [!DNL Query Editor] seleccionando una consulta en las pestañas **[!UICONTROL Log]** o **[!UICONTROL Browse]**. Si se selecciona una consulta guardada o ejecutada anteriormente, se abrirá [!DNL Query Editor] y se mostrará el SQL de la consulta seleccionada.

![Imagen](../images/ui/overview/overview.png)

[!DNL Query Editor] proporciona espacio de edición donde puede empezar a escribir una consulta. A medida que escribe, el editor completa automáticamente las palabras, tablas y nombres de campo reservados SQL en las tablas. Cuando termine de escribir la consulta, seleccione el botón **Play** para ejecutarla. La pestaña **[!UICONTROL Console]** debajo del editor muestra lo que [!DNL Query Service] está haciendo actualmente, lo que indica cuándo se ha devuelto una consulta. La pestaña **[!UICONTROL Result]**, junto a la consola, muestra los resultados de la consulta. Consulte la [guía del Editor de consultas](./user-guide.md) para obtener más información sobre el uso de [!DNL Query Editor].

![Imagen](../images/ui/overview/query-editor.png)

## Examinar

La pestaña **[!UICONTROL Browse]** muestra las consultas guardadas por los usuarios de su organización. Es útil considerar estos proyectos como proyectos de consulta, ya que las consultas guardadas aquí pueden estar aún en construcción. Las consultas mostradas en la pestaña **[!UICONTROL Browse]** también se muestran como consultas de ejecución en la pestaña **[!UICONTROL Log]** si ya las ha ejecutado [!DNL Query Service].

![Imagen](../images/ui/overview/browse.png)

| Columna | Descripción |
| --- | --- |
| Nombre | El nombre de consulta creado por el usuario. Puede seleccionar el nombre para abrir la consulta en el [!DNL Query Editor]. También puede utilizar la barra de búsqueda para buscar en el Nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| SQL | Los primeros caracteres de la consulta SQL. Al pasar el ratón por encima del código, se muestra la consulta completa. |
| Modificado por | El último usuario que modificó la consulta. Cualquier usuario de su organización con acceso a [!DNL Query Service] puede modificar consultas. |
| Última modificación | La fecha y hora de la última modificación de la consulta, en el huso horario del explorador. |

## Registro

La pestaña **[!UICONTROL Log]** proporciona una lista de consultas que se han ejecutado anteriormente. De forma predeterminada, el registro enumera las consultas en cronología inversa.

![Imagen](../images/ui/overview/log.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El nombre de la consulta, que consta de los primeros varios caracteres de la consulta SQL. Al seleccionar el nombre, se abre [!DNL Query Editor], lo que permite editar la consulta. Puede utilizar la barra de búsqueda para buscar en el Nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL Creado por]** | El nombre de la persona que creó la consulta. |
| **[!UICONTROL Cliente]** | El cliente utilizado para la consulta. |
| **[!UICONTROL Conjunto de datos]** | El conjunto de datos de entrada utilizado por la consulta. Seleccione el conjunto de datos para ir a la pantalla de detalles del conjunto de datos de entrada. |
| **[!UICONTROL Estado]** | Estado actual de la consulta. |
| **[!UICONTROL Última ejecución]** | La última vez que se ejecutó la consulta. Puede ordenar la lista en orden ascendente o descendente seleccionando la flecha sobre esta columna. |
| **[!UICONTROL Tiempo de ejecución]** | Cantidad de tiempo que se tardó en ejecutar la consulta. |

## Credenciales

La pestaña **[!UICONTROL Credentials]** muestra sus [!DNL Postgres] credenciales. Seleccione el icono **[!UICONTROL Copy]** situado junto a cualquier campo para almacenar su contenido en el búfer del teclado. Para obtener más información sobre cómo utilizar estas credenciales para conectarse con clientes externos, lea la [guía de conexión con clientes](../clients/overview.md).

![Imagen](../images/ui/overview/credentials.png)

## Pasos siguientes

Ahora que está familiarizado con la interfaz de usuario [!DNL Query Service] en [!DNL Platform], puede acceder a [!DNL Query Editor] para empezar a crear sus propios proyectos de consulta y compartirlos con otros usuarios de su organización. Para obtener más información sobre la creación y ejecución de consultas en [!DNL Query Editor], consulte la [Guía del usuario del Editor de consultas](./user-guide.md).