---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Buscador;buscador;conectarse al servicio de consulta;
solution: Experience Platform
title: Conectar el buscador al servicio de consulta
description: Este documento recorre los pasos para conectar Looker con el servicio de consulta de Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] al servicio de consultas

Este documento cubre los pasos para la conexión [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Looker] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Looker] se encuentra en la variable [oficial [!DNL Looker] documentación](https://docs.looker.com/).

## Crear una nueva conexión de base de datos {#create-connection}

Tras iniciar sesión [!DNL Looker], seleccione **[!DNL Admin]**, seguido de **[!DNL Connections]**. La variable [!DNL Connections] se abre. En el [!DNL Connections] página, seleccione **[!DNL Add Connection]**.

Desde aquí, introduzca los detalles de la configuración de conexión que se indican a continuación. Consulte la documentación oficial del buscador para [instrucciones para crear una nueva conexión de base de datos y descripciones de las propiedades disponibles](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nombre de la conexión.
- **[!DNL Dialect]:** El dialecto utilizado para la base de datos SQL. [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** El punto final del host y su puerto para [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.
- **[!DNL Username and Password]:** Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario se muestra en forma de `ORG_ID@AdobeOrg`.
- **SSL**: Habilite SSL para garantizar una conexión segura a través de la red.

Para encontrar las credenciales necesarias para conectar el buscador con el servicio de consulta, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener más información, consulte **host**, **puerto**, **base de datos**, **username** y **password** credenciales, lea la [guía de credenciales](../ui/credentials.md).

![La página Credenciales del espacio de trabajo Consultas de Experience Platform con Credenciales y las Credenciales de Vencimiento resaltadas.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para [instrucciones completas sobre cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials). Es necesario completar este proceso si desea conectar Looker como configuración única. La variable `credential` y `technicalAccountId` los valores adquiridos comprenden el valor del buscador `password` parámetro.

Para obtener más información sobre la compatibilidad con SSL para conexiones de terceros en Adobe Experience Platform, consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md). Este documento proporciona instrucciones sobre cómo conectar usando `verify-full` Modo SSL.

Una vez especificados los detalles de conexión, seleccione **[!DNL Test These Settings]** para garantizar que sus credenciales funcionen correctamente. Más información sobre [probar la configuración de conexión](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) se proporcionan en la documentación oficial del Looker. Cuando la conexión se ha realizado correctamente, aparece un mensaje en la pantalla para indicar que puede conectarse. Una vez que la conexión se haya realizado correctamente, seleccione **[!DNL Add Connection]** para crear la conexión.

## Pasos siguientes

Ahora que está conectado con [!DNL Query Service], puede usar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
