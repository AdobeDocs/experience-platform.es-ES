---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;postico;Postico;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de Postico al servicio de consulta
description: Este documento contiene el enlace para instalar el cliente de copia de seguridad Postico para el servicio de consulta de Adobe Experience Platform.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Connect [!DNL Postico] a servicio de consulta (Mac)

Este documento cubre los pasos para la conexión [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Postico] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Postico] se encuentra en la variable [oficial [!DNL Postico] documentación](https://eggerapps.at/postico/docs).
> 
> Además, [!DNL Postico] es **only** disponible en dispositivos macOS.

Para conectar [!DNL Postico] a Query Service, abra [!DNL Postico] y seleccione **[!DNL New Favorite]**.

![La variable [!DNL Postico] IU con el nuevo favorito resaltado.](../images/clients/postico/open-postico.png)

Ahora puede introducir valores para conectarse con Adobe Experience Platform.

Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform]y, a continuación, seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Después de insertar las credenciales, seleccione **[!DNL Connect]** para conectarse con el servicio de consulta.

![El cuadro de diálogo Nuevo favorito con conexión resaltado.](../images/clients/postico/authentication-details.png)

Después de conectarse a Platform, podrá ver una lista de todas las relaciones realizadas anteriormente con el servicio de consulta.

![Una lista de conexiones en la [!DNL Postico] IU.](../images/clients/postico/show-queries.png)

## Crear instrucciones SQL

Para crear una nueva consulta SQL, seleccione y abra &quot;Consulta SQL&quot;.

![La variable [!DNL Postico] IU con el acceso directo de consulta SQL resaltado.](../images/clients/postico/create-query.png)

Aparece un cuadro y desde aquí puede escribir la consulta que desee ejecutar. Cuando termine, seleccione **[!DNL Execute Statement]** para ejecutar la consulta.

![El editor SQL con la instrucción Execute resaltada.](../images/clients/postico/run-statement.png)

Aparece una tabla que muestra los resultados de la ejecución de la consulta completada.

![Una tabla de resultados de la consulta de ejemplo.](../images/clients/postico/query-results.png)

## Pasos siguientes

Ahora que está conectado con [!DNL Query Service], puede usar [!DNL Postico] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
