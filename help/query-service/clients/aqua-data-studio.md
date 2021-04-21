---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Aqua Data Studio;estudio de datos Aqua;conexión al servicio de consulta;
solution: Experience Platform
title: Conexión de Aqua Data Studio al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar Aqua Data Studio con el servicio de consulta de Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Conectar [!DNL Aqua Data Studio] al servicio de consulta

Este documento cubre los pasos para conectar [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Aqua Data Studio] y está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Aqua Data Studio] en la [oficial [!DNL Aqua Data Studio] documentación](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Después de instalar [!DNL Aqua Data Studio], primero debe registrar el servidor. En el menú principal, seleccione **[!DNL Server]**, seguido de **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Aparece el cuadro de diálogo **[!DNL Register Server]**. En la pestaña **[!DNL General]**, seleccione **[!DNL PostgreSQL]** en la lista del lado izquierdo. En el cuadro de diálogo que aparece, proporcione los siguientes detalles para la configuración del servidor.

- **[!DNL Name]**: Nombre de la conexión.
- **[!DNL Login Name and Password]**: Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario adopta la forma `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: El punto final del host y su puerto para  [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse con [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar sus credenciales de inicio de sesión, host, puerto y nombre de base de datos, visite la página [credenciales en Platform](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Queries]**, seguido de **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Seleccione la pestaña **[!DNL Driver]** En **[!DNL Parameters]**, establezca el valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Después de introducir los detalles de conexión, seleccione **[!DNL Test Connection]** para asegurarse de que las credenciales funcionan correctamente. Si la conexión se ha realizado correctamente, seleccione **[!DNL Save]** para registrar el servidor. La conexión aparece en el panel tras registrarse correctamente, lo que confirma que ahora puede conectarse al servidor y ver sus objetos de esquema.

## Pasos siguientes

Ahora que se ha conectado a [!DNL Query Service], puede utilizar el **[!DNL Query Analyzer]** dentro de [!DNL Aqua Data Studio] para ejecutar y editar las instrucciones SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
