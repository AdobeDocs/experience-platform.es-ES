---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Db Visualizer;DbVisualizer;visor de db;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de DbVisualizer al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar DbVisualizer con el servicio de consulta de Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 9c272cc5b879e38f6b6113542ec7bdfd4f11fa8a
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

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

En el espacio de trabajo de Conexión a la base de datos, seleccione la opción **[!DNL Properties]** , seguido de la pestaña **[!DNL Driver Properties]** desde la barra lateral de navegación.

![El espacio de trabajo Conexión a la base de datos con la ficha Propiedades resaltada.](../images/clients/dbvisualizer/driver-properties.png)

Las tres propiedades de controlador requeridas se muestran en la siguiente tabla.

| Propiedad | Descripción |
| ------ | ------ |
| `PGHOST` | El nombre de host de la variable [!DNL PostgreSQL] servidor. Este valor es su Experience Platform [!UICONTROL Host] credencial. |
| `SSL` | Esto controla el uso de los requisitos SSL. You **must** utilice el valor `require` para habilitar este requisito. |
| `user` | El nombre de usuario conectado a la base de datos es su ID de organización. Es una cadena alfanumérica que termina en `@adobe.org` |

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectarse mediante `verify-full` Modo SSL.

### [!DNL Query Service] credenciales

La variable `PGHOST` y `user` se toman de sus credenciales de Adobe Experience Platform. Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md).

![Tablero de credenciales de consultas de Experience Platform con credenciales resaltadas.](../images/clients/dbvisualizer/query-service-credentials-page.png)

[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para [instrucciones completas sobre cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials).

Utilice la barra de búsqueda para encontrar cada propiedad y luego seleccione la celda correspondiente para el valor del parámetro. La celda se resalta en azul. Introduzca las credenciales de Platform en el campo de valor y seleccione **[!DNL Apply]** para añadir la propiedad driver.

>[!NOTE]
>
>Para agregar un segundo `user` perfil, seleccione `user` en la columna parámetro , seleccione el icono azul + (más) para agregar credenciales para cada usuario. Select **[!DNL Apply]** para añadir la propiedad driver.

La variable [!DNL Edited] muestra una marca de verificación para indicar que se ha actualizado el valor del parámetro.

## Autenticación

Para requerir un ID de usuario y autenticación basada en contraseña cada vez que se establece una conexión, seleccione **[!DNL Authentication]** desde la barra lateral de navegación debajo de [!DNL PostgreSQL].

En el panel Autenticación de conexión, marque las dos **[!DNL Require Userid]** y **[!DNL Require Password]** casillas de verificación y seleccione **[!DNL Apply]**.

![El panel Autenticación de conexión con las casillas de verificación Userid y Password resaltadas.](../images/clients/dbvisualizer/connection-authentication.png)

## Conectarse a Platform

Para establecer una conexión, seleccione la opción **[!DNL Connection]** en el espacio de trabajo de Conexión a la base de datos e introduzca las credenciales del Experience Platform para las siguientes configuraciones.

- **Nombre**: Se recomienda proporcionar un nombre descriptivo para reconocer la conexión.
- **Servidor de bases de datos**: Este es su Experience Platform [!UICONTROL Host] credencial.
- **Puerto de base de datos**: El puerto de [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse con [!DNL Query Service].
- **Base de datos**: Usar las credenciales `dbname` value `prod:all`.
- **Base de Datos Userid**: Este es su ID de organización de Platform. El Userid tendrá el formato de `ORG_ID@AdobeOrg`.
- **Contraseña de base de datos**: Esta es una cadena alfanumérica que se encuentra en la variable [!DNL Query Service] tablero de credenciales.

Después de haber introducido todas las credenciales relevantes, seleccione **[!DNL Connect]**.

![El espacio de trabajo Conexión a la base de datos con la ficha Conexión y el botón de conexión resaltado.](../images/clients/dbvisualizer/connect.png)

La variable [!DNL Connect] aparece en la primera ocasión del período de sesiones.

![Se resaltan el cuadro de diálogo Conectar con los campos de texto userid de base de datos y contraseña de base de datos.](../images/clients/dbvisualizer/connect-dialog.png)

Introduzca su Userid y su Contraseña y seleccione **[!DNL Connect]**. Aparece un mensaje en el registro para confirmar que la conexión se ha realizado correctamente.

## Pasos siguientes

Ahora que se ha conectado [!DNL DbVisualizer] con [!DNL Query Service], puede usar [!DNL DbVisualizer] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía sobre la ejecución de consultas](../best-practices/writing-queries.md).
