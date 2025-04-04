---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;Aqua Data Studio;Aqua data studio;conectarse al servicio de consultas;
solution: Experience Platform
title: Conexión de Aqua Data Studio al servicio de consultas
description: Este documento explica los pasos para conectar Aqua Data Studio con el servicio de consultas de Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Conectar [!DNL Aqua Data Studio] al servicio de consultas

Este documento describe los pasos para conectar [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

## Introducción

Esta guía requiere que ya tenga acceso a [!DNL Aqua Data Studio] y que esté familiarizado con cómo navegar por su interfaz. Encontrará más información sobre [!DNL Aqua Data Studio] en la [documentación oficial [!DNL Aqua Data Studio] 3}.](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)

>[!NOTE]
>
>Hay [!DNL Windows] y [!DNL macOS] versiones de [!DNL Aqua Data Studio]. Las capturas de pantalla de esta guía se tomaron mediante la aplicación de escritorio [!DNL macOS]. Puede haber discrepancias menores en la interfaz de usuario entre las versiones.

Para adquirir las credenciales necesarias para conectar [!DNL Aqua Data Studio] a Experience Platform, debe tener acceso al área de trabajo [!UICONTROL Consultas] en la interfaz de usuario de Experience Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo [!UICONTROL Consultas].

## Registrar el servidor {#register-server}

Después de instalar [!DNL Aqua Data Studio], primero debe registrar el servidor. Consulte la documentación oficial de Aqua Data Studio para obtener instrucciones sobre cómo [iniciar el [!DNL Register Server] diálogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) y [registrar el servidor](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Una vez que aparezca el cuadro de diálogo **[!DNL Register Server]** para un servidor PostgresSQL, proporcione los siguientes detalles para la configuración del servidor.

- **[!DNL Name]**: nombre de su conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión.
- **[!DNL Login Name]**: el nombre de inicio de sesión es su ID de organización de Experience Platform. Adopta la forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: se trata de una cadena alfanumérica que se encuentra en el panel de credenciales de [!DNL Query Service].
- **[!DNL Host and Port]**: el extremo de host y su puerto para [!DNL Query Service]. Debe usar el puerto 80 para conectarse con [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará. Use el valor de la credencial `dbname` de la interfaz de usuario de Experience Platform: `prod:all`.

### Credenciales de [!DNL Query Service]

Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de [!DNL Experience Platform] y seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas para encontrar sus credenciales de inicio de sesión, host, puerto y nombre de base de datos, lea la [guía de credenciales](../ui/credentials.md).

[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para obtener [instrucciones completas sobre cómo generar y utilizar credenciales que no caducan](../ui/credentials.md#non-expiring-credentials).

### Estableciendo modo SSL

A continuación, debe establecer el valor del modo SSL como `?sslmode=require`. Esto se hace desde la ficha [!DNL Driver] del cuadro de diálogo [!DNL Edit Server Properties]. Consulte la documentación oficial de Aqua Data Studio para obtener instrucciones sobre cómo [editar las propiedades del controlador](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) y [configurar SSL para [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilice la barra de búsqueda para encontrar la propiedad `sslmode`.

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros con el servicio Adobe Experience Platform Query y cómo conectarse mediante el modo SSL `verify-full`.

Después de escribir los detalles de conexión, en la misma ficha, seleccione **[!DNL Test Connection]** para asegurarse de que las credenciales funcionan correctamente. Si la prueba de conexión se realizó correctamente, seleccione **[!DNL Save]** para registrar el servidor. Aparecerá un cuadro de diálogo de confirmación que confirma la conexión y el icono de conexión aparecerá en el panel. Ahora puede conectarse al servidor y ver sus objetos de esquema.

## Pasos siguientes

Ahora que se ha conectado a [!DNL Query Service], puede usar **[!DNL Query Analyzer]** en [!DNL Aqua Data Studio] para ejecutar y editar instrucciones SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
