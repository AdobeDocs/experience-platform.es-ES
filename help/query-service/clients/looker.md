---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Buscador;buscador;conectarse al servicio de consulta;
solution: Experience Platform
title: Conectar el buscador al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar Looker con el servicio de consulta de Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Conectar [!DNL Looker] al servicio de consulta

Este documento cubre los pasos para conectar [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Looker] y está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Looker] en la [oficial [!DNL Looker] documentación](https://docs.looker.com/).

Después de iniciar sesión en [!DNL Looker], seleccione **[!DNL Admin]**, seguido de **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

En esta página, seleccione **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

Desde aquí puede rellenar los detalles de la configuración de conexión.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** El nombre de la conexión.
- **[!DNL Dialect]:** El dialecto utilizado para la base de datos SQL. [!DNL Query Service] usa  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** El punto final del host y su puerto para  [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.
- **[!DNL Username and Password]:** Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario tiene la forma `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar el host y el puerto, el nombre de la base de datos y las credenciales de inicio de sesión, visite la página [credenciales de Platform](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Queries]**, seguido de **[!UICONTROL Credentials]**.

Después de introducir los detalles de conexión, seleccione **[!DNL Test These Settings]** para asegurarse de que las credenciales funcionan correctamente. Si lo hacen, a continuación aparecerá un mensaje que indica que puede conectarse. Si la conexión es correcta, seleccione **[!DNL Add Connection]** para crear la conexión.

![](../images/clients/looker/click-test-connection.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
