---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;Aqua Data Studio;Aqua data studio;conectarse al servicio de consultas;
solution: Experience Platform
title: Conexión de Aqua Data Studio al servicio de consultas
description: Este documento explica los pasos para conectar Aqua Data Studio con el servicio de consultas de Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] al servicio de consultas

Este documento describe los pasos para la conexión [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

## Primeros pasos

Esta guía requiere que ya tenga acceso a [!DNL Aqua Data Studio] y estar familiarizado con cómo navegar por su interfaz. Más información sobre [!DNL Aqua Data Studio] se puede encontrar en la [funcionario [!DNL Aqua Data Studio] documentación](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>No hay [!DNL Windows] y [!DNL macOS] versiones de [!DNL Aqua Data Studio]. Las capturas de pantalla de esta guía se tomaron utilizando el [!DNL macOS] aplicación de escritorio. Puede haber discrepancias menores en la interfaz de usuario entre las versiones.

Para adquirir las credenciales necesarias para la conexión [!DNL Aqua Data Studio] para acceder a Experience Platform, debe tener acceso a [!UICONTROL Consultas] Workspace en la IU de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso a [!UICONTROL Consultas] workspace.

## Registrar el servidor {#register-server}

Después de la instalación [!DNL Aqua Data Studio], primero debe registrar el servidor. Consulte la documentación oficial de Aqua Data Studio para obtener instrucciones sobre cómo [inicie el [!DNL Register Server] diálogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) y [registrar el servidor](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Una vez que **[!DNL Register Server]** aparece para un servidor PostgresSQL, proporcione los siguientes detalles para la configuración del servidor.

- **[!DNL Name]**: Nombre de la conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión.
- **[!DNL Login Name]**: el nombre de inicio de sesión es su ID de organización de Platform. Adopta la forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Se trata de una cadena alfanumérica que se encuentra en la variable [!DNL Query Service] tablero de credenciales.
- **[!DNL Host and Port]**: el extremo del host y su puerto para [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse a [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará. Utilice el valor de las credenciales de la IU de Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenciales

Para encontrar sus credenciales, inicie sesión en [!DNL Platform] IU y seleccione **[!UICONTROL Consultas]** desde el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas para encontrar sus credenciales de inicio de sesión, host, puerto y nombre de base de datos, lea la [guía de credenciales](../ui/credentials.md).

[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación de [instrucciones completas sobre cómo generar y utilizar credenciales que no caducan](../ui/credentials.md#non-expiring-credentials).

### Estableciendo modo SSL

A continuación, debe establecer el valor del modo SSL como `?sslmode=require`. Esto se hace desde el [!DNL Driver] de la pestaña [!DNL Edit Server Properties] diálogo. Consulte la documentación oficial de Aqua Data Studio para obtener instrucciones sobre cómo [editar propiedades del controlador](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) y [configurar SSL para [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilice la barra de búsqueda para buscar `sslmode` propiedad.

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros con Adobe Experience Platform Query Service y cómo conectarse mediante `verify-full` Modo SSL.

Después de introducir los detalles de conexión, en la misma pestaña, seleccione **[!DNL Test Connection]** para asegurarse de que sus credenciales funcionan correctamente. Si la prueba de conexión se realiza correctamente, seleccione **[!DNL Save]** para registrar su servidor. Aparecerá un cuadro de diálogo de confirmación que confirma la conexión y el icono de conexión aparecerá en el panel. Ahora puede conectarse al servidor y ver sus objetos de esquema.

## Pasos siguientes

Ahora que se ha conectado a [!DNL Query Service], puede utilizar el **[!DNL Query Analyzer]** dentro [!DNL Aqua Data Studio] para ejecutar y editar sentencias SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
