---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Conectar con Aqua Data Studio
topic: connect
description: Este documento recorre los pasos para conectar Aqua Data Studio con el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Conectar con [!DNL Aqua Data Studio]

Este documento recorre los pasos para conectarse [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

Después de la instalación [!DNL Aqua Data Studio], primero debe registrar el servidor. En el menú principal, haga clic en **[!UICONTROL Servidor]** y, a continuación, en **[!UICONTROL Registrar servidor]**.

![](../images/clients/aqua-data-studio/register-server.png)

Aparece el cuadro de diálogo **[!UICONTROL Registrar servidor]** . En la ficha **[!UICONTROL General]** , seleccione **[!UICONTROL PostgreSQL]** en la lista del lado izquierdo. En el cuadro de diálogo que aparece, proporcione los siguientes detalles para la configuración del servidor.

- **[!UICONTROL Nombre]**: Nombre de la conexión.
- **[!UICONTROL Nombre de inicio de sesión y contraseña]**: Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario adopta la forma de `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host y puerto]**: El punto final del host y su puerto para [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse con [!DNL Query Service].
- **[!UICONTROL Base de datos]:** Base de datos que se utilizará.

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar las credenciales de inicio de sesión, el host, el puerto y el nombre de la base de datos, visite la página de [credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para buscar las credenciales, inicie sesión en [!DNL Platform], haga clic en **[!UICONTROL Consultas]** y, a continuación, haga clic en **[!UICONTROL Credenciales]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **[!UICONTROL Driver]** tab. En **[!UICONTROL Parámetros]**, establezca el valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Después de introducir los detalles de la conexión, haga clic en **[!UICONTROL Probar conexión]** para asegurarse de que las credenciales funcionan correctamente. Si la conexión es correcta, haga clic en **[!UICONTROL Guardar]** para registrar el servidor. La conexión aparece en el *Panel* tras registrarse correctamente, lo que confirma que ahora puede conectarse al servidor y realizar la vista de los objetos de esquema.

## Pasos siguientes

Ahora que se ha conectado a [!DNL Query Service], puede utilizar el analizador **[!UICONTROL de]** Consultas en [!DNL Aqua Data Studio] para ejecutar y editar sentencias SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía de consultas [en ejecución](../creating-queries/creating-queries.md).