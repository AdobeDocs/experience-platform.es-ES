---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;buscador;buscador;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar el buscador al servicio de consultas
description: Este documento explica los pasos para conectar Looker con el servicio de consultas de Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] al servicio de consultas

Este documento describe los pasos para la conexión [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL Looker] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Looker] se puede encontrar en la [funcionario [!DNL Looker] documentación](https://docs.looker.com/).

## Crear una nueva conexión de base de datos {#create-connection}

Después de iniciar sesión en [!DNL Looker], seleccione **[!DNL Admin]**, seguido de **[!DNL Connections]**. El [!DNL Connections] se abre la página. En el [!DNL Connections] página, seleccione **[!DNL Add Connection]**.

Desde aquí, introduzca los detalles de la configuración de conexión que se indica a continuación. Consulte la documentación oficial de Looker para [instrucciones para crear una nueva conexión de base de datos y descripciones de las propiedades disponibles](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nombre de la conexión.
- **[!DNL Dialect]:** El dialecto utilizado para la base de datos SQL. [!DNL Query Service] utiliza **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** El extremo de host y su puerto para [!DNL Query Service].
- **[!DNL Database]:** La base de datos que se utilizará.
- **[!DNL Username and Password]:** Credenciales de inicio de sesión que se utilizarán. El nombre de usuario debe ser `ORG_ID@AdobeOrg`.
- **SSL**: habilite SSL para garantizar una conexión segura a través de la red.

Para encontrar las credenciales necesarias para conectar el buscador con el servicio de consultas, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar su **host**, **puerto**, **database**, **nombre de usuario**, y **contraseña** credenciales, lea la [guía de credenciales](../ui/credentials.md).

![La página Credenciales del espacio de trabajo Consultas del Experience Platform con las credenciales y las credenciales caducadas resaltadas.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación de [instrucciones completas sobre cómo generar y utilizar credenciales que no caducan](../ui/credentials.md#non-expiring-credentials). Es necesario completar este proceso si desea conectar Looker como una configuración única. El `credential` y `technicalAccountId` Los valores adquiridos comprenden el valor del elemento buscador `password` parámetro.

Para obtener más información sobre la compatibilidad SSL con conexiones de terceros en Adobe Experience Platform, consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md). Este documento proporciona instrucciones sobre cómo conectarse mediante `verify-full` Modo SSL.

Una vez introducidos los detalles de conexión, seleccione **[!DNL Test These Settings]** para asegurarse de que sus credenciales funcionan correctamente. Más información sobre [prueba de la configuración de conexión](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) se proporcionan en la documentación oficial de Looker. Una vez que la conexión se haya realizado correctamente, aparecerá un mensaje en pantalla para indicar que puede conectarse. Una vez realizada la conexión correctamente, seleccione **[!DNL Add Connection]** para crear la conexión.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Looker] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
