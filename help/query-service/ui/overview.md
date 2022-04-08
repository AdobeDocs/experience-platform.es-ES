---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta;editor de consultas;editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de consulta
topic-legacy: guide
description: El servicio de consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de la organización de IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 2%

---

# [!DNL Query Service] Guía de la interfaz de usuario

Adobe Experience Platform [!DNL Query Service] proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de su organización de IMS. Para acceder a la IU dentro de [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo.

## [!DNL Query Editor]

La variable [!DNL Query Editor] permite escribir y ejecutar consultas sin utilizar un cliente externo. Select **[!UICONTROL Crear consulta]** para abrir el [!DNL Query Editor] y cree una nueva consulta. También puede acceder al [!DNL Query Editor] seleccionando una consulta en el **[!UICONTROL Registro]** o **[!UICONTROL Examinar]** pestañas. Si se selecciona una consulta guardada o ejecutada anteriormente, se abrirá la variable [!DNL Query Editor] y mostrar el SQL para la consulta seleccionada.

![El panel Consultas con la opción Crear consulta resaltada.](../images/ui/overview/overview.png)

[!DNL Query Editor] proporciona espacio de edición donde puede empezar a escribir una consulta. A medida que escribe, el editor completa automáticamente las palabras, tablas y nombres de campo reservados SQL en las tablas. Cuando termine de escribir la consulta, seleccione la **Play** para ejecutar la consulta. La variable **[!UICONTROL Consola]** debajo del editor se muestra qué [!DNL Query Service] está haciendo, lo que indica cuándo se ha devuelto una consulta. La variable **[!UICONTROL Resultado]** , junto a la consola, muestra los resultados de la consulta. Consulte la [Guía del Editor de consultas](./user-guide.md) para obtener más información sobre el uso de la variable [!DNL Query Editor].

![Un zoom en vista de la variable [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Examinar {#browse}

La variable **[!UICONTROL Examinar]** muestra las consultas guardadas por los usuarios de su organización. Es útil considerar estos proyectos como proyectos de consulta, ya que las consultas guardadas aquí pueden estar aún en construcción. Consultas mostradas en la **[!UICONTROL Examinar]** también se muestra como consultas de ejecución en la pestaña **[!UICONTROL Registro]** si ha sido ejecutado anteriormente por [!DNL Query Service].

![Se ha ampliado la vista de la pestaña Examinar del panel Consultas que muestra varias consultas guardadas.](../images/ui/overview/browse.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El nombre de consulta creado por el usuario. Puede seleccionar el nombre para abrir la consulta en el [!DNL Query Editor]. También puede utilizar la barra de búsqueda para buscar en el Nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL SQL]** | Los primeros caracteres de la consulta SQL. Al pasar el ratón por encima del código, se muestra la consulta completa. |
| **[!UICONTROL Modificado por]** | El último usuario que modificó la consulta. Cualquier usuario de su organización con acceso a [!DNL Query Service] puede modificar consultas. |
| **[!UICONTROL Última modificación]** | La fecha y hora de la última modificación de la consulta, en el huso horario del explorador. |

## Registro

La variable **[!UICONTROL Registro]** proporciona una lista de consultas que se han ejecutado anteriormente. De forma predeterminada, el registro enumera las consultas en cronología inversa.

![Se ha ampliado la vista de la ficha Registro del panel Consultas que muestra una lista de consultas en orden cronológico inverso.](../images/ui/overview/log.png)

| Columna | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | El nombre de la consulta, que consta de los primeros varios caracteres de la consulta SQL. Si se selecciona el nombre, se abre la variable [!DNL Query Editor], lo que le permite editar la consulta. Puede utilizar la barra de búsqueda para buscar en el Nombre de una consulta. Las búsquedas distinguen entre mayúsculas y minúsculas. |
| **[!UICONTROL Creado por]** | El nombre de la persona que creó la consulta. |
| **[!UICONTROL Cliente]** | El cliente utilizado para la consulta. |
| **[!UICONTROL Conjunto de datos]** | El conjunto de datos de entrada utilizado por la consulta. Seleccione el conjunto de datos para ir a la pantalla de detalles del conjunto de datos de entrada. |
| **[!UICONTROL Estado]** | Estado actual de la consulta. |
| **[!UICONTROL Última ejecución]** | La última vez que se ejecutó la consulta. Puede ordenar la lista en orden ascendente o descendente seleccionando la flecha sobre esta columna. |
| **[!UICONTROL Tiempo de ejecución]** | Cantidad de tiempo que se tardó en ejecutar la consulta. |

## Credenciales

La variable **[!UICONTROL Credenciales]** muestra las credenciales que caducan y las que no caducan. Para obtener más información sobre cómo utilizar estas credenciales para conectarse con clientes externos, lea la [guía de credenciales](../clients/overview.md).

![El panel Consultas con la pestaña Credenciales resaltada.](../images/ui/overview/credentials.png)

## Pasos siguientes

Ahora está familiarizado con [!DNL Query Service] interfaz de usuario activada [!DNL Platform], puede acceder a [!DNL Query Editor] para empezar a crear sus propios proyectos de consulta y compartirlos con otros usuarios de su organización. Para obtener más información sobre la creación y ejecución de consultas en [!DNL Query Editor], consulte la [[!DNL Query Editor] guía del usuario](./user-guide.md).