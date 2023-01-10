---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Buscador;buscador;conectarse al servicio de consulta;
solution: Experience Platform
title: Conectar el buscador al servicio de consulta
description: Este documento recorre los pasos para conectar Looker con el servicio de consulta de Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Connect [!DNL Looker] al servicio de consultas

Este documento cubre los pasos para la conexión [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Looker] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Looker] se encuentra en la variable [oficial [!DNL Looker] documentación](https://docs.looker.com/).

Tras iniciar sesión [!DNL Looker], seleccione **[!DNL Admin]**, seguido de **[!DNL Connections]**.

![La variable [!DNL Looker] tablero con Conexiones resaltadas en el menú desplegable Administrador .](../images/clients/looker/click-admin-connections.png)

En esta página, seleccione **[!DNL New Connection]**.

![El espacio de trabajo Conexiones con Nueva conexión resaltado.](../images/clients/looker/click-new-connection.png)

Desde aquí puede rellenar los detalles de la configuración de conexión.

![La página Configuración de conexiones para una nueva conexión.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Nombre de la conexión.
- **[!DNL Dialect]:** El dialecto utilizado para la base de datos SQL. [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** El punto final del host y su puerto para [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.
- **[!DNL Username and Password]:** Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario se muestra en forma de `ORG_ID@AdobeOrg`.
- **SSL**: Habilite SSL para garantizar una conexión segura a través de la red.

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectarse mediante `verify-full` Modo SSL.

Para obtener más información sobre cómo encontrar el host y el puerto, el nombre de la base de datos y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform]y, a continuación, seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Después de introducir los detalles de conexión, seleccione **[!DNL Test These Settings]** para garantizar que sus credenciales funcionen correctamente. Si lo hacen, a continuación aparecerá un mensaje que indica que puede conectarse. Si la conexión se ha realizado correctamente, seleccione **[!DNL Add Connection]** para crear la conexión.

![La página Configuración de conexiones para una nueva conexión con Probar esta configuración está resaltada.](../images/clients/looker/click-test-connection.png)

## Pasos siguientes

Ahora que está conectado con [!DNL Query Service], puede usar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
