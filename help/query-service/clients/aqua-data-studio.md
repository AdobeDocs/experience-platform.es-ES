---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Aqua Data Studio;estudio de datos Aqua;conexión al servicio de consulta;
solution: Experience Platform
title: Conexión de Aqua Data Studio al servicio de consulta
description: Este documento recorre los pasos para conectar Aqua Data Studio con el servicio de consulta de Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '487'
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

Después de instalar [!DNL Aqua Data Studio], primero debe registrar el servidor. En el menú principal, seleccione **[!DNL Server]**, seguido de **[!DNL Register Server]**.

![Menú desplegable Servidor con Registro del servidor resaltado.](../images/clients/aqua-data-studio/register-server.png)

La variable **[!DNL Register Server]** se abre. En el **[!DNL General]** , seleccione **[!DNL PostgreSQL]** de la lista en el lado izquierdo. En el cuadro de diálogo que aparece, proporcione los siguientes detalles para la configuración del servidor.

- **[!DNL Name]**: Nombre de la conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión.
- **[!DNL Login Name]**: El nombre de inicio de sesión es su ID de organización de Platform. Toma la forma de `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Esta es una cadena alfanumérica que se encuentra en la variable [!DNL Query Service] tablero de credenciales.
- **[!DNL Host and Port]**: El punto final del host y su puerto para [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse con [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará. Utilizar el valor de las credenciales de la interfaz de usuario de Platform `dbname`: `prod:all`.

![La variable [!DNL Aqua Data Studio] Ficha General con los campos de entrada necesarios resaltados.](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] credenciales

Para encontrar sus credenciales, inicie sesión en la [!DNL Platform] IU y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas para encontrar sus credenciales de inicio de sesión, host, puerto y nombre de la base de datos, lea la [guía de credenciales](../ui/credentials.md).

[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para [instrucciones completas sobre cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials).

### Configuración del modo SSL

A continuación, seleccione la **[!DNL Driver]** pestaña . En **[!DNL Parameters]**, establezca el valor como `?sslmode=require`

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectarse mediante `verify-full` Modo SSL.

![La variable [!DNL Aqua Data Studio] Pestaña Controlador con el campo Parámetros resaltado.](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Después de introducir los detalles de conexión, seleccione **[!DNL Test Connection]** para garantizar que sus credenciales funcionen correctamente. Si la prueba de conexión se ha realizado correctamente, seleccione **[!DNL Save]** para registrar su servidor. Aparece un cuadro de diálogo de confirmación que confirma la conexión y esta aparece en el panel. Ahora puede conectarse al servidor y ver sus objetos de esquema.

## Pasos siguientes

Ahora se ha conectado a [!DNL Query Service], puede usar la variable **[!DNL Query Analyzer]** en [!DNL Aqua Data Studio] para ejecutar y editar instrucciones SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
