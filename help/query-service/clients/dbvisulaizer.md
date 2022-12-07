---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Db Visualizer;DbVisualizer;visor de db;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de DbVisualizer al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar DbVisualizer con el servicio de consulta de Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 7d38488c204e28c9cfd8ea50c06f1ce781d76c59
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# Connect [!DNL DbVisualizer] a [!DNL Query Service] {#connect-dbvisualizer}

Este documento cubre los pasos para conectar el [!DNL DbVisualizer] herramienta de base de datos con Adobe Experience Platform [!DNL Query Service].

## Primeros pasos

Esta guía requiere que ya tenga acceso al [!DNL DbVisualizer] aplicación de escritorio y están familiarizados con cómo navegar por su interfaz. Para descargar el [!DNL DbVisualizer] aplicación de escritorio o para obtener más información, consulte la [oficial [!DNL DbVisualizer] documentación](https://www.dbvis.com/download/).

>[!NOTE]
>
>Hay [!DNL Windows], [!DNL macOS]y [!DNL Linux] versiones de [!DNL DbVisualizer]. Las capturas de pantalla de esta guía se tomaron usando la variable [!DNL macOS] aplicación de escritorio. Puede haber pequeñas discrepancias en la interfaz de usuario entre las versiones.

Para adquirir las credenciales necesarias para la conexión [!DNL  DbVisualizer] para Experience Platform, debe tener acceso al espacio de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de la organización IMS si actualmente no tiene acceso al espacio de trabajo Consultas .

## Creación de una conexión de base de datos {#connect-database}

Una vez que haya instalado la aplicación de escritorio en el equipo local, inicie la aplicación y seleccione **[!DNL Create a Database Connection]** desde la [!DNL DbVisualizer] para abrir el Navegador. A continuación, seleccione **[!DNL Create a Connection]** en el panel de la derecha.

![La variable [!DNL DbVisualizer] menú principal con &quot;Crear una conexión de base de datos&quot; resaltado.](../images/clients/dbvisualizer/create-db-connection.png)

Utilice la barra de búsqueda o seleccione [!DNL PostgreSQL] en la lista desplegable nombre del controlador . Aparecerá el espacio de trabajo Conexión a la base de datos.

![El menú desplegable de nombre del controlador con [!DNL PostgreSQL] resaltado.](../images/clients/dbvisualizer/driver-name.png)

### Establecer propiedades para la conexión {#properties}

En el espacio de trabajo de Conexión a la base de datos, seleccione la opción **[!DNL Properties]** , seguido de la pestaña **[!DNL Driver Properties]** desde la barra lateral de navegación.

![El espacio de trabajo Conexión a la base de datos con Propiedades y Propiedades del controlador resaltadas.](../images/clients/dbvisualizer/driver-properties.png)

A continuación, introduzca las propiedades del controlador que se describen en la tabla siguiente.

>[!IMPORTANT]
>
>Para conectar DBVisualizer con Adobe Experience Platform, debe habilitar el uso de SSL. Consulte la [Documentación de modos SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectarse mediante `verify-full` Modo SSL.

| Propiedad | Descripción |
| ------ | ------ |
| `PGHOST` | El nombre de host de la variable [!DNL PostgreSQL] servidor. Este valor es su Experience Platform **[!UICONTROL Host] credencial**. |
| `ssl` | Definir el valor SSL `1` para habilitar el uso de SSL. |
| `sslmode` | Esto controla el nivel de protección SSL. Se recomienda usar la variable `require` Modo SSL al conectar clientes de terceros a Adobe Experience Platform. La variable `require` garantiza que se requiere cifrado en todas las comunicaciones y que se confía en que la red se conecte al servidor correcto. No es necesario validar el certificado SSL del servidor. |
| `user` | El nombre de usuario conectado a la base de datos es su ID de organización. Es una cadena alfanumérica que termina en `@Adobe.Org`. Este valor es su Experience Platform **[!UICONTROL Nombre de usuario] credencial**. |

Utilice la barra de búsqueda para encontrar cada propiedad y luego seleccione la celda correspondiente para el valor del parámetro. La celda se resalta en azul. Introduzca las credenciales de Platform en el campo de valor y seleccione **[!DNL Apply]** para añadir la propiedad driver.

![La ficha Propiedades del controlador DBVisulaizer con un valor introducido y Aplicar resaltado.](../images/clients/dbvisualizer/apply-parameter-value.png)

>[!NOTE]
>
>Para agregar un segundo `user` perfil, seleccione `user` en la columna parámetro , seleccione el icono azul + (más) para agregar credenciales para cada usuario. Select **[!DNL Apply]** para añadir la propiedad driver.

La variable [!DNL Edited] muestra una marca de verificación para indicar que se ha actualizado el valor del parámetro.

### Entrada[!DNL Query Service] credenciales

Para encontrar las credenciales necesarias para conectar BBVisualizer con Query Service, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener más información, consulte **host**, **puerto**, **base de datos**, **username** y **password** credenciales, lea la [guía de credenciales](../ui/credentials.md).

![La página Credenciales del espacio de trabajo Consultas de Experience Platform con Credenciales y las Credenciales de Vencimiento resaltadas.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para [instrucciones completas sobre cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials). Es necesario completar este proceso si desea conectar BDVisualizer como configuración única. La variable `credential` y `technicalAccountId` los valores adquiridos comprenden el valor del depurador DBVisualizer `password` parámetro.

## Autenticación

Para requerir un ID de usuario y autenticación basada en contraseña cada vez que se establece una conexión, seleccione **[!DNL Authentication]** desde la barra lateral de navegación debajo de [!DNL PostgreSQL].

En el panel Autenticación de conexión, marque las dos **[!DNL Require Userid]** y **[!DNL Require Password]** casillas de verificación y seleccione **[!DNL Apply]**.

![El panel Autenticación para [!DNL PostgreSQL] Conexión de base de datos con las casillas de verificación Requerir Userid y Contraseña resaltadas.](../images/clients/dbvisualizer/connection-authentication.png)

## Conectarse a Platform

Puede realizar una conexión con credenciales que caduquen o no caduquen. Para establecer una conexión, seleccione la opción **[!DNL Connection]** en el espacio de trabajo de Conexión a la base de datos e introduzca las credenciales del Experience Platform para las siguientes configuraciones.

>[!NOTE]
>
>Todas las credenciales requeridas por BDVisualizer en la tabla siguiente son las mismas para las credenciales que caducan y no caducan a menos que se indique en la descripción del parámetro.

| Parámetro de conexión | Descripción |
|---|---|
| **[!UICONTROL Nombre]** | Cree un nombre para la conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión. |
| **[!UICONTROL Servidor de bases de datos]** | Este es su Experience Platform **[!UICONTROL Host]** credencial. |
| **[!UICONTROL Puerto de base de datos]** | El puerto de [!DNL Query Service]. Debe utilizar el puerto **80** para conectarse con [!DNL Query Service]. |
| **[!UICONTROL Database]** | Uso de su Experience Platform **[!UICONTROL Base de datos]** valor de credencial: `prod:all`. |
| **[!UICONTROL Base de Datos Userid]** | Este es su ID de organización de Platform. Uso de su Experience Platform **[!UICONTROL Nombre de usuario]** valor de credencial. El ID tendrá el formato de `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Contraseña de base de datos]** | Esta cadena alfanumérica es su Experience Platform **[!UICONTROL Contraseña]** credencial.Si desea utilizar credenciales que no caduquen, este valor es el argumento concatenado del `technicalAccountID` y `credential` descargado en el archivo JSON de configuración. El valor de la contraseña adopta la forma: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante su inicialización de que el Adobe no conserva una copia de . |

Después de haber introducido todas las credenciales relevantes, seleccione **[!DNL Connect]**.

![La variable [!DNL PostgreSQL] Espacio de trabajo de conexión a base de datos con la ficha Conexión y el botón de conexión resaltado.](../images/clients/dbvisualizer/connect.png)

La variable [!DNL Connect] aparece en la primera ocasión del período de sesiones.

![La conexión: [!DNL PostgreSQL] con los campos de texto Userid de base de datos y Contraseña de base de datos resaltados.](../images/clients/dbvisualizer/connect-dialog.png)

Introduzca su Userid y su Contraseña y seleccione **[!DNL Connect]**. Aparece un mensaje en el registro para confirmar que la conexión se ha realizado correctamente.

## Pasos siguientes

Ahora que se ha conectado [!DNL DbVisualizer] con [!DNL Query Service], puede usar [!DNL DbVisualizer] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía sobre la ejecución de consultas](../best-practices/writing-queries.md).
