---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Power BI;power bi;conexión al servicio de consulta;
solution: Experience Platform
title: Conectar Power BI al servicio de consulta
description: Este documento recorre los pasos para conectar la Power BI con el servicio de consulta de Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# Connect [!DNL Power BI] al servicio de consultas

Este documento cubre los pasos para la conexión [!DNL Power BI] Escritorio con el servicio de consulta de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere que ya tenga acceso al [!DNL Power BI] aplicación de escritorio y están familiarizados con cómo navegar por su interfaz. Para descargar [!DNL Power BI] Escritorio o para obtener más información, consulte la [oficial [!DNL Power BI] documentación](https://docs.microsoft.com/es-ES/power-bi/).

>[!IMPORTANT]
>
> La variable [!DNL Power BI] la aplicación de escritorio es **only** disponible en dispositivos Windows.

Para adquirir las credenciales necesarias para la conexión [!DNL Power BI] para Experience Platform, debe tener acceso al espacio de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de la organización IMS si actualmente no tiene acceso al espacio de trabajo Consultas .

Después de instalar [!DNL Power BI], deberá instalar `Npgsql`, un paquete de controladores .NET para PostgreSQL. Puede encontrar más información sobre Npgsql en la [Documentación Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Debe descargar la versión 4.0.10 o anterior, ya que las versiones más recientes dan como resultado errores.

En &quot;[!DNL Npgsql GAC Installation]&quot; en la pantalla de configuración personalizada, seleccione **[!DNL Will be installed on local hard drive]**.

Para asegurarse de que Npgsql se haya instalado correctamente, reinicie el equipo antes de seguir los pasos siguientes.

## Connect [!DNL Power BI] al servicio de consultas {#connect-power-bi}

Para conectar [!DNL Power BI] a Query Service, abra [!DNL Power BI] y seleccione **[!DNL Get Data]** en la cinta de opciones del menú superior.

![La variable [!DNL Power BI] ficha Inicio del tablero con Obtener datos resaltados.](../images/clients/power-bi/open-power-bi.png)

Escriba &quot;[!DNL PostgreSQL]&quot; en la barra de búsqueda para reducir la lista de fuentes de datos. En los resultados que aparecen, seleccione **[!DNL PostgreSQL database]**, seguido de **[!DNL Connect]**.

![El cuadro de diálogo Obtener datos con [!DNL PostgreSQL] base de datos y Connect resaltados.](../images/clients/power-bi/get-data.png)

La variable [!DNL PostgreSQL] aparece el cuadro de diálogo base de datos, solicitando valores para el servidor y la base de datos. Estos valores se toman de sus credenciales de Adobe Experience Platform. Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md).

![El espacio de trabajo Consultas del Experience Platform con la ficha Credenciales y las credenciales de caducidad resaltadas.](../images/clients/power-bi/query-service-credentials-page.png)

Para la variable **[!DNL Server]** en Power BI, introduzca el valor del host que se encuentra en la sección Credenciales del servicio de consulta . Para la producción, agregue el puerto `:80` al final de la cadena host. Por ejemplo, `made-up.platform-query.adobe.io:80`.

La variable **[!DNL Database]** puede ser &quot;all&quot; o un nombre de tabla de conjunto de datos. Por ejemplo, `prod:all`.

>[!IMPORTANT]
>
>Las estructuras de datos anidadas en herramientas de BI de terceros se pueden aplanar para mejorar su capacidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos. Consulte la documentación de[`FLATTEN` función](../best-practices/flatten-nested-data.md) para obtener instrucciones sobre cómo activar esta configuración al conectarse a una base de datos.

![La variable [!DNL Power BI] tablero con los campos de entrada del servidor y la base de datos resaltados.](../images/clients/power-bi/postgresql-database-dialog.png)

### Modo de conectividad de datos

A continuación, puede seleccionar su **[!DNL Data Connectivity mode]**. Select **[!DNL Import]** seguido de **[!DNL OK]** para mostrar una lista de todas las tablas disponibles, o seleccione **[!DNL DirectQuery]** para consultar el origen de datos directamente sin importar ni copiar datos directamente en [!DNL Power BI].

Para obtener más información sobre **[!DNL Import]** , lea la sección en [importación de una tabla](#import). Para obtener más información sobre **[!DNL DirectQuery]** , lea la sección en [consulta de un conjunto de datos sin importar datos](#direct-query).

Select **[!DNL OK]** después de confirmar los detalles de la base de datos.

![La variable [!DNL PostgreSQL] cuadro de diálogo de base de datos con el modo Conectividad de datos resaltado.](../images/clients/power-bi/connectivity-mode.png)

### Autenticación

Aparecerá una solicitud de confirmación que solicita su nombre de usuario, contraseña y configuración de la aplicación. El nombre de usuario en este caso es su ID de organización y la contraseña es su token de autenticación. Ambas se encuentran en la página de credenciales del servicio de consulta .

Complete estos detalles y seleccione **[!DNL Connect]** para continuar con el siguiente paso.

![El cuadro de diálogo de base de datos con el menú desplegable Nombre de usuario, Contraseña y Configuración de aplicación resaltado.](../images/clients/power-bi/import-mode.png)

## Importar una tabla {#import}

Seleccione la **[!DNL Import]** [!DNL Data Connectivity mode], se importa el conjunto de datos completo, lo que le permite utilizar las tablas y columnas seleccionadas dentro de la variable [!DNL Power BI] aplicación de escritorio tal cual.

>[!IMPORTANT]
>
>Para ver los cambios de datos que se han producido desde la importación inicial, debe actualizar los datos en [!DNL Power BI] importando de nuevo el conjunto de datos completo.

Para importar una tabla, introduzca los detalles del servidor y la base de datos [tal como se describe anteriormente](#connect-power-bi) y seleccione **[!DNL Import]** [!DNL Data Connectivity mode], seguido de **[!DNL OK]**. Aparece un cuadro de diálogo que muestra una lista de todas las tablas disponibles. Seleccione la tabla de la que desea obtener una vista previa, seguida de **[!DNL Load]** para introducir el conjunto de datos en Power BI.

![El cuadro de diálogo Navegador con una tabla y Cargar resaltado.](../images/clients/power-bi/preview-table.png)

La tabla ahora se importa en [!DNL Power BI].

![La variable [!DNL Power BI] tablero con instrucciones sobre la creación de visualizaciones personalizadas resaltadas.](../images/clients/power-bi/import-table.png)

### Importar tablas con SQL personalizado

[!DNL Power BI] y otras herramientas de terceros como Tableau actualmente no permiten a los usuarios importar objetos anidados, como objetos XDM en Platform. Para tener en cuenta esto, [!DNL Power BI] permite utilizar SQL personalizado para acceder a estos campos anidados y crear una vista plana de los datos. [!DNL Power BI] a continuación, carga esta vista plana de los datos anidados anteriormente como una tabla normal.

En el [!DNL PostgreSQL] apertura de la base de datos, seleccione **[!DNL Advanced options]** para introducir una consulta SQL personalizada en el **[!DNL SQL statement]** para obtener más información. Esta consulta personalizada debe utilizarse para acoplar sus pares de nombre-valor JSON a un formato de tabla.

![La variable [!DNL PostgreSQL] cuadro de diálogo de base de datos con las opciones avanzadas del modo de conectividad de datos resaltadas. Permiten crear una instrucción SQL personalizada.](../images/clients/power-bi/custom-sql-statement.png)

Una vez introducida la consulta personalizada, seleccione **[!DNL OK]** para continuar conectando la base de datos. Consulte la [autenticación](#authentication) para obtener instrucciones sobre cómo conectar una base de datos desde esta parte del flujo de trabajo.

Una vez finalizada la autenticación, aparece una vista previa de los datos acoplados en la variable [!DNL Power BI] Panel de escritorio como tabla. El nombre del servidor y de la base de datos se muestran en la parte superior del cuadro de diálogo. Select **[!DNL Load]** para completar el proceso de importación.

![Una visualización de una tabla plana e importada en la variable [!DNL Power BI] tablero.](../images/clients/power-bi/imported-table-preview.png)

Las visualizaciones ya están disponibles para su edición y exportación desde el [!DNL Power BI] Aplicación de escritorio.

## Consultar el conjunto de datos sin importar datos {#direct-query}

La variable **[!DNL DirectQuery]** [!DNL Data Connectivity mode] consulta el origen de datos directamente sin importar ni copiar datos en el [!DNL Power BI] Escritorio. Con este modo de conexión, puede actualizar todas las visualizaciones con datos actuales a través de la interfaz de usuario. Sin embargo, el tiempo necesario para producir o actualizar la visualización variará según el rendimiento de la fuente de datos subyacente.

Para usar esto [!DNL Data Connectivity mode], seleccione **[!DNL DirectQuery]** alternar entonces **[!DNL Advanced options]** para introducir una consulta SQL personalizada en el **[!DNL SQL statement]** para obtener más información. Asegúrese de que **[!DNL Include relationship columns]** está seleccionado. Una vez completada la consulta, seleccione **[!DNL OK]** para continuar.

![La variable [!DNL PostgreSQL] cuadro de diálogo de base de datos con la configuración necesaria para utilizar el modo Conectividad de datos resaltado.](../images/clients/power-bi/direct-query-mode.png)

Aparecerá una vista previa de la consulta. Select **[!DNL Load]** para ver los resultados de la consulta.

![Vista previa de los resultados tabularizados a partir de la consulta de ejemplo.](../images/clients/power-bi/preview-direct-query.png)

## Pasos siguientes

Al leer este documento, ahora debe comprender cómo conectar con la variable [!DNL Power BI] Aplicación de escritorio y los distintos modos de conexión de datos disponibles. Para obtener más información sobre cómo escribir y ejecutar consultas, consulte la [directrices para la ejecución de consultas](../best-practices/writing-queries.md).
