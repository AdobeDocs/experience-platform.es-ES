---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar con el buscador
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Conectar con [!DNL Looker]

Para conectarse [!DNL Looker] con [!DNL Query Service] Adobe Experience Platform, siga los pasos a continuación:

Después de iniciar sesión [!DNL Looker], haga clic en **[!UICONTROL Administrador]**, seguido de **[!UICONTROL Conexiones]**.

![](../images/clients/looker/click-admin-connections.png)

En esta página, haga clic en **Nueva conexión**.

![](../images/clients/looker/click-new-connection.png)

Desde aquí puede completar los detalles de la Configuración de conexión.

![](../images/clients/looker/new-connection.png)

- **Nombre:** Nombre de la conexión.
- **Dialect:** El dialecto utilizado para la base de datos SQL. [!DNL Query Service] usa **[!DNL PostgreSQL]**.
- **Host y puerto:** El punto final del host y su puerto para [!DNL Query Service].
- **Base de datos:** Base de datos que se utilizará.
- **Nombre de usuario y contraseña:** Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario tendrá la forma de `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar el host y el puerto, el nombre de la base de datos y las credenciales de inicio de sesión, visite la página de [credenciales en Platform](https://platform.adobe.com/query/configuration). Para buscar las credenciales, inicie sesión en [!DNL Platform], haga clic en **[!UICONTROL Consultas]** y, a continuación, haga clic en **[!UICONTROL Credenciales]**.

Después de introducir los detalles de la conexión, haga clic en **[!UICONTROL Probar esta configuración]** para asegurarse de que las credenciales funcionan correctamente. Si lo hacen, a continuación aparecerá un mensaje que indica que puede conectarse. Si la conexión es correcta, haga clic en **[!UICONTROL Añadir conexión]** para crear la conexión.

![](../images/clients/looker/click-test-connection.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede usar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía de consultas [en ejecución](../creating-queries/creating-queries.md).