---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;postal;pórtico;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar Postico al servicio de consultas
description: Este documento contiene el vínculo para instalar el cliente de copia de seguridad Postico para Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Conectar [!DNL Postico] al servicio de consultas (Mac)

Este documento describe los pasos para conectar [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL Postico] y que está familiarizado con la forma de navegar por su interfaz. Encontrará más información sobre [!DNL Postico] en la [documentación oficial [!DNL Postico] 3}.](https://eggerapps.at/postico/docs)
> 
> Además, [!DNL Postico] es **solamente** disponible en dispositivos macOS.

Para conectar a [!DNL Postico] al servicio de consultas, abra [!DNL Postico] y seleccione **[!DNL New Favorite]**. Aparecerá el cuadro de diálogo para la configuración de conexión. Desde aquí puede introducir valores de parámetro para conectarse con Adobe Experience Platform. Introduzca la configuración de conexión que se indica a continuación. Las instrucciones sobre cómo [conectarse a un servidor PostgreSQL con Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) también están disponibles en el sitio web oficial de Postico.

| Parámetro de conexión | Descripción |
|---|---|
| **[!DNL Host]:** | Nombre de host del servidor PostgreSQL. |
| **[!DNL Port]:** | El puerto de [!DNL Query Service]. Debe usar el puerto **80** o **5432** para conectarse con [!DNL Query Service]. |
| **[!DNL User]** | Cree un nombre para la conexión específica. Deje el campo en blanco para utilizar el nombre de inicio de sesión de Mac. |
| **[!DNL Password]** | Esta cadena alfanumérica es su credencial **[!UICONTROL Password]** de Experience Platform. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados de `technicalAccountID` y `credential` descargados en el archivo JSON de configuración. El valor de contraseña adopta la forma: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante la inicialización de la que Adobe no conserva una copia. |
| **[!DNL Database]** | Use su valor de credencial **[!UICONTROL Database]** de Experience Platform: `prod:all`. |

Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Experience Platform] y luego seleccione **[!UICONTROL Consultas]**, seguidas de **[!UICONTROL Credenciales]**.

Después de insertar las credenciales, seleccione **[!DNL Connect]** para conectarse al servicio de consultas.

Después de conectarse a Experience Platform, podrá ver una lista de todas las relaciones realizadas anteriormente con Query Service.

## Crear instrucciones SQL

Para crear una nueva consulta SQL, seleccione **[!DNL SQL Query]** en la barra lateral. También puede utilizar el método abreviado de teclado (⇧⌘T) para desplazarse a la vista de consulta e introducir la consulta que desea ejecutar. Cuando termine, seleccione **[!DNL Execute Statement]** para ejecutar la consulta. Aparecerá una tabla con los resultados de la ejecución de la consulta completada.

Consulte la documentación oficial de Postico para obtener más información sobre [cómo usar la vista de consulta](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede usar [!DNL Postico] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
