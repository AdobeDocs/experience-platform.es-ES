---
keywords: Experience Platform;inicio;temas populares;tableau;Tableau;servicio de consulta;servicio de consulta;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de Tableau al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar Tableau con el servicio de consulta de Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Conectar [!DNL Tableau] al servicio de consulta

Este documento cubre los pasos para conectar Tableau con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Tableau] y está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Tableau] en la [oficial [!DNL Tableau] documentación](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Para conectar [!DNL Tableau] a [!DNL Query Service], abra [!DNL Tableau] y, en la sección **[!DNL To a Server]**, seleccione **[!DNL More]** seguido de **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Ahora puede introducir valores para conectarse con Adobe Experience Platform. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la página [credenciales de Platform](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Queries]**, seguido de **[!UICONTROL Credentials]**.

Asegúrese de haber marcado la casilla **[!UICONTROL SSL Required]** antes de intentar conectarse.

Después de completar todas las credenciales, seleccione **[!DNL Sign In]** para continuar.

![](../images/clients/tableau/sign-in.png)

Ahora se ha conectado con Adobe Experience Platform, con una lista de las tablas mostradas en el lateral.

![](../images/clients/tableau/connected.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Tableau] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).
