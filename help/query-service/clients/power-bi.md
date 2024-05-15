---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;Power BI;power bi;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar la Power BI al servicio de consultas
description: Este documento explica los pasos para conectar Power BI con el servicio de consultas de Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# Connect [!DNL Power BI] al servicio de consultas

Este documento describe los pasos para la conexión [!DNL Power BI] Escritorio con servicio de consultas de Adobe Experience Platform.

## Introducción

Esta guía requiere que ya tenga acceso a [!DNL Power BI] y están familiarizados con cómo navegar por su interfaz. Para descargar [!DNL Power BI] Escritorio o para obtener más información, consulte la [funcionario [!DNL Power BI] documentación](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> El [!DNL Power BI] la aplicación de escritorio es **solamente** disponible en dispositivos Windows.

Para adquirir las credenciales necesarias para la conexión [!DNL Power BI] Para acceder al Experience Platform, debe tener acceso al espacio de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo de consultas.

Después de la instalación [!DNL Power BI], tendrá que instalar `Npgsql`, un paquete de controladores .NET para PostgreSQL. Puede encontrar más información sobre Npgsql en el [Documentación de Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Debe descargar la versión 4.0.10 o inferior, ya que las versiones más recientes generan errores.

En &quot;[!DNL Npgsql GAC Installation]&quot; en la pantalla de configuración personalizada, seleccione **[!DNL Will be installed on local hard drive]**.

Para asegurarse de que Npgsql se ha instalado correctamente, reinicie el equipo antes de continuar con los siguientes pasos.

## Connect [!DNL Power BI] al servicio de consultas {#connect-power-bi}

Para conectar [!DNL Power BI] al servicio de consultas, abra [!DNL Power BI] y seleccione **[!DNL Get Data]** en la cinta del menú superior. A continuación, introduzca &quot;[!DNL PostgreSQL]&quot; en la barra de búsqueda para reducir la lista de fuentes de datos. De los resultados que aparecen, seleccione **[!DNL PostgreSQL database]**, seguido de **[!DNL Connect]**.

El [!DNL PostgreSQL] aparece el cuadro de diálogo base de datos, solicitando valores para el servidor y la base de datos. Instrucciones adicionales sobre cómo [conectarse a una base de datos PostgreSQL desde Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) se puede encontrar en el [!DNL PowerBI] documentación.

Estos valores necesarios se toman de las credenciales de Adobe Experience Platform. Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md).

>[!IMPORTANT]
>
>Como usuario de Power BI o Tableau, puede conectarse con Customer Journey Analytics a sus herramientas de BI desde la pestaña de credenciales del servicio de consulta. Consulte la documentación de credenciales para obtener instrucciones sobre cómo [conectar las herramientas de BI al Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![El espacio de trabajo Consultas del Experience Platform con la pestaña Credenciales y Credenciales de caducidad resaltadas.](../images/clients/power-bi/query-service-credentials-page.png)

En el **[!DNL Server]** del campo [!DNL PostgreSQL database] , introduzca el valor del host encontrado en el servicio de consultas [!UICONTROL Credenciales] sección. Para la producción, añada el puerto `:80` al final de la cadena de host. Por ejemplo, `made-up.platform-query.adobe.io:80`.

El **[!DNL Database]** el campo puede ser &quot;todo&quot; o un nombre de tabla de conjunto de datos. Por ejemplo, `prod:all`.

>[!IMPORTANT]
>
>Las estructuras de datos anidadas en herramientas de BI de terceros se pueden aplanar para mejorar su facilidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos. Consulte la documentación de la[`FLATTEN` característica](../key-concepts/flatten-nested-data.md) para obtener instrucciones sobre cómo activar esta configuración al conectarse a una base de datos.

### Modo de conectividad de datos {#data-connectivity-mode}

A continuación, puede seleccionar su **[!DNL Data Connectivity mode]**. En el [!DNL PostgreSQL database] diálogo, seleccione **[!DNL Import]** seguido de **[!DNL OK]** para mostrar una lista de todas las tablas disponibles, o seleccione **[!DNL DirectQuery]** para consultar el origen de datos directamente sin importar ni copiar datos directamente en [!DNL Power BI].

Para obtener más información sobre **[!DNL Import]** modo, lea la sección sobre [importación de una tabla](#import). Para obtener más información acerca de **[!DNL DirectQuery]** modo, lea la sección sobre [consultar un conjunto de datos sin importar datos](#direct-query).

Seleccionar **[!DNL OK]** después de confirmar los detalles de la base de datos.

### Autenticación {#authentication}

Después de confirmar el modo de conectividad de datos, aparece un mensaje en el que se solicita la configuración del nombre de usuario, la contraseña y la aplicación. En este caso, el nombre de usuario es su ID de organización y la contraseña es su token de autenticación. Ambos se encuentran en la página de credenciales del servicio de consulta.

Rellene estos detalles y seleccione **[!DNL Connect]** para continuar con el paso siguiente.

## Importar una tabla {#import}

Al seleccionar la variable **[!DNL Import]** [!DNL Data Connectivity mode], se importa el conjunto de datos completo, que le permite utilizar las tablas y columnas seleccionadas dentro de la variable [!DNL Power BI] aplicación de escritorio tal cual.

>[!IMPORTANT]
>
>Para ver los cambios de datos que se han producido desde la importación inicial, debe actualizar los datos en [!DNL Power BI] importando de nuevo el conjunto de datos completo.

Para importar una tabla, introduzca los detalles del servidor y la base de datos [como se ha descrito anteriormente](#connect-power-bi) y seleccione la **[!DNL Import]** [!DNL Data Connectivity mode], seguido de **[!DNL OK]**. El [!DNL Navigator] aparece un cuadro de diálogo que muestra una lista de todas las tablas disponibles. Seleccione la tabla que desee previsualizar, seguida de **[!DNL Load]** para introducir el conjunto de datos en Power BI. La tabla ahora se importa a [!DNL Power BI].

[Información general sobre la conexión a datos en el escritorio de PowerBi](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) La aplicación se encuentra en la documentación oficial.

### Importar tablas mediante SQL personalizado

[!DNL Power BI] y otras herramientas de terceros como [!DNL Tableau] actualmente no permiten a los usuarios importar objetos anidados, como objetos XDM en Platform. Para tener en cuenta esto, [!DNL Power BI] permite utilizar SQL personalizado para acceder a estos campos anidados y crear una vista plana de los datos. [!DNL Power BI] a continuación, carga esta vista aplanada de los datos anidados anteriormente como una tabla normal.

Desde el [!DNL PostgreSQL database] diálogo, seleccione **[!DNL Advanced options]** para introducir una consulta SQL personalizada en **[!DNL SQL statement]** sección. Esta consulta personalizada debe utilizarse para acoplar los pares de nombre-valor de JSON a un formato de tabla. La documentación oficial también proporciona información sobre cómo [conectar Power BI con una instrucción SQL en las opciones avanzadas](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Después de introducir la consulta personalizada, seleccione **[!DNL OK]** para continuar conectando la base de datos. Consulte la [authentication](#authentication) para obtener instrucciones sobre cómo conectar una base de datos desde esta parte del flujo de trabajo.

Una vez finalizada la autenticación, aparece una vista previa de los datos aplanados en la [!DNL Power BI] Tablero de escritorio como tabla. El nombre del servidor y la base de datos se muestran en la parte superior del cuadro de diálogo. Seleccionar **[!DNL Load]** para completar el proceso de importación.

Las visualizaciones ya están disponibles para la edición y exportación desde [!DNL Power BI] Aplicación de escritorio.

## Consultar el conjunto de datos sin importar datos {#direct-query}

El **[!DNL DirectQuery]** [!DNL Data Connectivity mode] consulta el origen de datos directamente sin importar ni copiar datos en [!DNL Power BI] Escritorio. Con este modo de conexión, puede actualizar todas las visualizaciones con datos actuales a través de la interfaz de usuario. Sin embargo, el tiempo necesario para producir o actualizar la visualización variará según el rendimiento del origen de datos subyacente.

Más información sobre [el uso de [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) así como una discusión exhaustiva sobre sus [opciones de conectividad, casos de uso y limitaciones](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) se puede encontrar en el [!DNL PowerBI] documentación.

Para usar esto [!DNL Data Connectivity mode], seleccione la **[!DNL DirectQuery]** alternar entonces **[!DNL Advanced options]** para introducir una consulta SQL personalizada en **[!DNL SQL statement]** sección. Asegúrese de que **[!DNL Include relationship columns]** está seleccionado. Una vez completada la consulta, seleccione **[!DNL OK]** para continuar.

Aparecerá una vista previa de la consulta. Seleccionar **[!DNL Load]** para ver los resultados de la consulta.

## Pasos siguientes

Al leer este documento, debería saber cómo conectarse a la [!DNL Power BI] Aplicación de escritorio y los diferentes modos de conexión de datos disponibles. Para obtener más información sobre cómo escribir y ejecutar consultas, consulte la [instrucciones para la ejecución de consultas](../best-practices/writing-queries.md).
