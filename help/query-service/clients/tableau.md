---
keywords: Experience Platform;inicio;temas populares;tableau;Tableau;servicio de consulta;servicio de consulta;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de Tableau con el servicio de consultas
topic-legacy: connect
description: Este documento recorre los pasos para conectar Tableau con el servicio de consulta de Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 0c20b19c4c34b29c46964d5d87a8646c61055b06
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# Connect [!DNL Tableau] al servicio de consultas

Este documento cubre los pasos para conectar Tableau con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Tableau] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Tableau] se encuentra en la variable [oficial [!DNL Tableau] documentación](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Para conectar [!DNL Tableau] a [!DNL Query Service], abra [!DNL Tableau]y en la **[!DNL To a Server]** sección seleccionar **[!DNL More]** seguido de **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Ahora puede introducir valores para conectarse con Adobe Experience Platform. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform]y, a continuación, seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Asegúrese de haber marcado la variable **[!UICONTROL SSL requerido]** antes de intentar conectarse.

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectarse mediante `verify-full` Modo SSL.

![](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>Las estructuras de datos anidadas en herramientas de BI de terceros se pueden aplanar para mejorar su capacidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos. Consulte la documentación de[`FLATTEN` función](../best-practices/flatten-nested-data.md) para obtener instrucciones sobre cómo activar esta configuración al conectarse a una base de datos.

Después de rellenar todas las credenciales, seleccione **[!DNL Sign In]** para continuar.

Ahora se ha conectado con Adobe Experience Platform, con una lista de las tablas mostradas en el lateral.

![](../images/clients/tableau/connected.png)

## Pasos siguientes

Ahora que está conectado con [!DNL Query Service], puede usar [!DNL Tableau] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía de [ejecución de consultas](../best-practices/writing-queries.md).
