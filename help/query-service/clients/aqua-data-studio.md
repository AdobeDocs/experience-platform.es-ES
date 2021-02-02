---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;Aqua Data Studio;Estudio de datos Aqua;conexión al servicio de consulta;
solution: Experience Platform
title: Conectar con Aqua Data Studio
topic: connect
description: Este documento recorre los pasos para conectar Aqua Data Studio con el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---


# [!DNL Aqua Data Studio]

Este documento cubre los pasos para conectar [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se asume que ya tiene acceso a [!DNL Aqua Data Studio] y que está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Aqua Data Studio] en la [documentación oficial [!DNL Aqua Data Studio] ](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

## Conectar [!DNL Aqua Data Studio] con plataforma

Después de instalar [!DNL Aqua Data Studio], primero debe registrar el servidor. En el menú principal, seleccione **[!DNL Server]**, seguido de **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Aparece el cuadro de diálogo **[!DNL Register Server]**. En la ficha **[!DNL General]**, seleccione **[!DNL PostgreSQL]** en la lista del lado izquierdo. En el cuadro de diálogo que aparece, proporcione los siguientes detalles para la configuración del servidor.

- **[!DNL Name]**:: Nombre de la conexión.
- **[!DNL Login Name and Password]**:: Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario toma la forma `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**:: El punto final del host y su puerto para  [!DNL Query Service]. Debe utilizar el puerto 80 para conectarse con [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar sus credenciales de inicio de sesión, host, puerto y nombre de base de datos, visite la página [credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Seleccione la pestaña **[!DNL Driver]** En **[!DNL Parameters]**, establezca el valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Después de introducir los detalles de conexión, seleccione **[!DNL Test Connection]** para asegurarse de que las credenciales funcionan correctamente. Si la conexión es correcta, seleccione **[!DNL Save]** para registrar el servidor. La conexión aparece en el panel tras el registro correcto, lo que confirma que ahora puede conectarse al servidor y realizar la vista de los objetos de esquema.

## Pasos siguientes

Ahora que se ha conectado a [!DNL Query Service], puede utilizar **[!DNL Query Analyzer]** dentro de [!DNL Aqua Data Studio] para ejecutar y editar sentencias SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).