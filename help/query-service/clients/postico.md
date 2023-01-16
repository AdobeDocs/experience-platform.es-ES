---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;postico;Postico;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de Postico al servicio de consulta
description: Este documento contiene el enlace para instalar el cliente de copia de seguridad Postico para el servicio de consulta de Adobe Experience Platform.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connect [!DNL Postico] a servicio de consulta (Mac)

Este documento cubre los pasos para la conexión [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Postico] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Postico] se encuentra en la variable [oficial [!DNL Postico] documentación](https://eggerapps.at/postico/docs).
> 
> Además, [!DNL Postico] es **only** disponible en dispositivos macOS.

Para conectar [!DNL Postico] a Query Service, abra [!DNL Postico] y seleccione **[!DNL New Favorite]**. Aparecerá el cuadro de diálogo para la configuración de conexión. Desde aquí puede introducir valores de parámetro para conectarse con Adobe Experience Platform. Introduzca la configuración de conexión que aparece a continuación. Instrucciones sobre cómo [conexión a un servidor PostgreSQL con Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) también están disponibles en el sitio web oficial de Postico.

| Parámetro de conexión | Descripción |
|---|---|
| **[!DNL Host]:** | El nombre de host del servidor PostgreSQL. |
| **[!DNL Port]:** | El puerto de [!DNL Query Service]. Debe utilizar el puerto **80** o **5432** para conectarse con [!DNL Query Service]. |
| **[!DNL User]** | Cree un nombre para la conexión específica. Deje el campo en blanco para utilizar su nombre de inicio de sesión de Mac. |
| **[!DNL Password]** | Esta cadena alfanumérica es su Experience Platform **[!UICONTROL Contraseña]** credencial. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados del `technicalAccountID` y `credential` descargado en el archivo JSON de configuración. El valor de la contraseña adopta la forma: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante su inicialización de que el Adobe no conserva una copia de . |
| **[!DNL Database]** | Uso de su Experience Platform **[!UICONTROL Base de datos]** valor de credencial: `prod:all`. |

Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform]y, a continuación, seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Después de insertar las credenciales, seleccione **[!DNL Connect]** para conectarse con el servicio de consulta.

Después de conectarse a Platform, podrá ver una lista de todas las relaciones realizadas anteriormente con el servicio de consulta.

## Crear instrucciones SQL

Para crear una nueva consulta SQL, seleccione **[!DNL SQL Query]** de la barra lateral. También puede utilizar el método abreviado de teclado ( ⇧ ⌘ T) para ir a la vista de consulta e introducir la consulta que desea ejecutar. Cuando termine, seleccione **[!DNL Execute Statement]** para ejecutar la consulta. Aparece una tabla con los resultados de la ejecución de la consulta completada.

Consulte la documentación oficial de Postico para obtener más información sobre [uso de la vista de consulta](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Pasos siguientes

Ahora que está conectado con [!DNL Query Service], puede usar [!DNL Postico] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
