---
keywords: Experience Platform;inicio;temas populares;servicio de Consulta;servicio de consulta;postico;Postico;conectar con servicio de consulta;
solution: Experience Platform
title: Conectar Postico al servicio de Consulta
topic: connect
description: Este documento contiene el vínculo para instalar el cliente de copia de seguridad Postico para el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Conectar [!DNL Postico] al servicio de Consulta (Mac)

Este documento cubre los pasos para conectar [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se asume que ya tiene acceso a [!DNL Postico] y que está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Postico] en la [documentación oficial [!DNL Postico] ](https://eggerapps.at/postico/docs).
> 
> Además, [!DNL Postico] está **sólo** disponible en dispositivos macOS.

Para conectar [!DNL Postico] al servicio de Consulta, abra [!DNL Postico] y seleccione **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

Ahora puede introducir valores para conectarse con Adobe Experience Platform.

Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la [página de credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Después de insertar las credenciales, seleccione **[!DNL Connect]** para conectarse con el servicio de Consulta.

![](../images/clients/postico/authentication-details.png)

Después de conectarse a Platform, podrá ver una lista de todas las relaciones realizadas anteriormente con el servicio de Consulta.

![](../images/clients/postico/show-queries.png)

## Crear sentencias SQL

Para crear una nueva consulta SQL, seleccione y abra &quot;Consulta SQL&quot;.

![](../images/clients/postico/create-query.png)

Aparece un cuadro y desde aquí puede escribir la consulta que desee ejecutar. Cuando termine, seleccione **[!DNL Execute Statement]** para ejecutar la consulta.

![](../images/clients/postico/run-statement.png)

Aparece una tabla que muestra los resultados de la ejecución de la consulta completada.

![](../images/clients/postico/query-results.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Postico] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).