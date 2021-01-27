---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Conectar con el buscador
topic: connect
description: Este documento recorre los pasos para conectar el buscador con el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Conectar con [!DNL Looker]

Para conectar [!DNL Looker] con [!DNL Query Service] en Adobe Experience Platform, siga los pasos a continuación:

Después de iniciar sesión en [!DNL Looker], haga clic en **[!UICONTROL Administración]**, seguido de **[!UICONTROL Conexiones]**.

![](../images/clients/looker/click-admin-connections.png)

En esta página, haga clic en **Nueva conexión**.

![](../images/clients/looker/click-new-connection.png)

Desde aquí puede completar los detalles de la Configuración de conexión.

![](../images/clients/looker/new-connection.png)

- **Nombre:** el nombre de la conexión.
- **Dialect:** dialecto utilizado para la base de datos SQL. [!DNL Query Service] usa  **[!DNL PostgreSQL]**.
- **Host y puerto:** el punto final del host y su puerto para  [!DNL Query Service].
- **Base de datos:** la base de datos que se utilizará.
- **Nombre de usuario y contraseña:** las credenciales de inicio de sesión que se utilizarán. El nombre de usuario tendrá la forma `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar el host y el puerto, el nombre de la base de datos y las credenciales de inicio de sesión, visite la [página de credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform], haga clic en **[!UICONTROL Consultas]** y luego haga clic en **[!UICONTROL Credenciales]**.

Después de introducir los detalles de la conexión, haga clic en **[!UICONTROL Probar esta configuración]** para asegurarse de que las credenciales funcionan correctamente. Si lo hacen, a continuación aparecerá un mensaje que indica que puede conectarse. Si la conexión es correcta, haga clic en **[!UICONTROL Añadir conexión]** para crear la conexión.

![](../images/clients/looker/click-test-connection.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).