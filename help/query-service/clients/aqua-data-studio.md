---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Aqua Data Studio;estudio de datos Aqua;conexión al servicio de consulta;
solution: Experience Platform
title: Conexión de Aqua Data Studio al servicio de consulta
description: Este documento recorre los pasos para conectar Aqua Data Studio con el servicio de consulta de Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 3ffb535e9a6648f037678acebba0de5f2088e79e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] al servicio de consultas

Este documento cubre los pasos para la conexión [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

## Primeros pasos

Esta guía requiere que ya tenga acceso a [!DNL Aqua Data Studio] y familiarizarse con cómo navegar por su interfaz. Más información sobre [!DNL Aqua Data Studio] se encuentra en la variable [oficial [!DNL Aqua Data Studio] documentación](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Hay [!DNL Windows] y [!DNL macOS] versiones de [!DNL Aqua Data Studio]. Las capturas de pantalla de esta guía se tomaron usando la variable [!DNL macOS] aplicación de escritorio. Puede haber pequeñas discrepancias en la interfaz de usuario entre las versiones.

Para adquirir las credenciales necesarias para la conexión [!DNL Aqua Data Studio] al Experience Platform, debe tener acceso al [!UICONTROL Consultas] en la interfaz de usuario de Platform. Póngase en contacto con el administrador de la organización IMS si actualmente no tiene acceso al [!UICONTROL Consultas] espacio de trabajo.

## Registrar el servidor {#register-server}

Después de instalar [!DNL Aqua Data Studio], primero debe registrar el servidor. Consulte la documentación oficial de Aqua Data Studio para obtener instrucciones sobre cómo [inicie el [!DNL Register Server] cuadro de diálogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) y [registrar el servidor](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Una vez que la variable **[!DNL Register Server]** para un servidor PostgresSQL, proporcione los siguientes detalles para la configuración del servidor.

- **[!DNL Name]**: Nombre de la conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión.
- **[!DNL Login Name]**: El nombre de inicio de sesión es su ID de organización de Platform. Toma la forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Esta es una cadena alfanumérica que se encuentra en la variable [!DNL Query Service] tablero de credenciales.
- **[!DNL Host and Port]**: El punto final del host y su puerto para [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse con [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará. Utilizar el valor de las credenciales de la interfaz de usuario de Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenciales

Para encontrar sus credenciales, inicie sesión en la [!DNL Platform] IU y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas para encontrar sus credenciales de inicio de sesión, host, puerto y nombre de la base de datos, lea la [guía de credenciales](../ui/credentials.md).

[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para [instrucciones completas sobre cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials).

### Configuración del modo SSL

A continuación, debe establecer el valor del modo SSL como `?sslmode=require`. Esto se realiza desde la variable [!DNL Driver] de la pestaña [!DNL Edit Server Properties] diálogo. Consulte la documentación oficial de Aqua Data Studio para obtener instrucciones sobre cómo [editar propiedades del controlador](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) y [configurar SSL para [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilice la barra de búsqueda para encontrar la variable `sslmode` propiedad.

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectarse mediante `verify-full` Modo SSL.

Después de introducir los detalles de conexión, en la misma pestaña, seleccione **[!DNL Test Connection]** para garantizar que sus credenciales funcionen correctamente. Si la prueba de conexión se ha realizado correctamente, seleccione **[!DNL Save]** para registrar su servidor. Aparece un cuadro de diálogo de confirmación que confirma la conexión y el icono de conexión aparece en el panel. Ahora puede conectarse al servidor y ver sus objetos de esquema.

## Pasos siguientes

Ahora se ha conectado a [!DNL Query Service], puede usar la variable **[!DNL Query Analyzer]** en [!DNL Aqua Data Studio] para ejecutar y editar instrucciones SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
