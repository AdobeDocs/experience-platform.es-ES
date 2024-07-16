---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;buscador;buscador;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar el buscador al servicio de consultas
description: Este documento explica los pasos para conectar Looker con el servicio de consultas de Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Conectar [!DNL Looker] al servicio de consultas

Este documento describe los pasos para conectar [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL Looker] y que está familiarizado con la forma de navegar por su interfaz. Encontrará más información sobre [!DNL Looker] en la [documentación oficial [!DNL Looker] 3}.](https://docs.looker.com/)

## Crear una nueva conexión de base de datos {#create-connection}

Después de iniciar sesión en [!DNL Looker], seleccione **[!DNL Admin]**, seguido de **[!DNL Connections]**. Se abre la página [!DNL Connections]. En la página [!DNL Connections], seleccione **[!DNL Add Connection]**.

Desde aquí, introduzca los detalles de la configuración de conexión que se indica a continuación. Consulte la documentación oficial del buscador para obtener [instrucciones para crear una nueva conexión de base de datos y descripciones de las propiedades disponibles](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** El nombre de su conexión.
- **[!DNL Dialect]:** El dialecto usado para la base de datos SQL. [!DNL Query Service] usa **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** El extremo de host y su puerto para [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.
- **[!DNL Username and Password]:** Credenciales de inicio de sesión que se utilizarán. El nombre de usuario será `ORG_ID@AdobeOrg`.
- **SSL**: habilite SSL para garantizar una conexión segura a través de la red.

Para encontrar las credenciales necesarias para conectar el buscador con el servicio de consultas, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar las credenciales de **host**, **puerto**, **base de datos**, **nombre de usuario** y **contraseña**, lea la [guía de credenciales](../ui/credentials.md).

![Se resaltaron la página Credenciales del área de trabajo Consultas de Experience Platform con las credenciales y las credenciales que caducan.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para obtener [instrucciones completas sobre cómo generar y utilizar credenciales que no caducan](../ui/credentials.md#non-expiring-credentials). Es necesario completar este proceso si desea conectar Looker como una configuración única. Los valores `credential` y `technicalAccountId` adquiridos comprenden el valor del parámetro Looker `password`.

Para obtener más información acerca de la compatibilidad de SSL con conexiones de terceros en Adobe Experience Platform, consulte la [[!DNL Query Service] documentación de SSL](./ssl-modes.md). Este documento proporciona instrucciones sobre cómo conectarse utilizando el modo SSL `verify-full`.

Una vez que haya ingresado los detalles de la conexión, seleccione **[!DNL Test These Settings]** para asegurarse de que sus credenciales funcionen correctamente. Encontrará más información sobre [probar la configuración de conexión](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) en la documentación oficial de Looker. Una vez que la conexión se haya realizado correctamente, aparecerá un mensaje en pantalla para indicar que puede conectarse. Una vez que la conexión se haya realizado correctamente, seleccione **[!DNL Add Connection]** para crear la conexión.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede usar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
