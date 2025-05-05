---
keywords: Experience Platform;inicio;temas populares;tableau;Tableau;servicio de consultas;servicio de consultas;conectarse al servicio de consultas;
solution: Experience Platform
title: Conexión de Tableau con el servicio de consultas
description: Este documento explica los pasos para conectar Tableau con el servicio de consultas de Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Conectar [!DNL Tableau] al servicio de consultas

Este documento proporciona información para conectar [!DNL Tableau] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL Tableau] y que está familiarizado con la forma de navegar por su interfaz. Encontrará más información sobre [!DNL Tableau] en la [documentación oficial [!DNL Tableau] 3&rbrace;.](https://help.tableau.com/current/pro/desktop/en-us/default.htm)

Las instrucciones sobre cómo [conectarse a un servidor PostgreSQL con Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) están disponibles en el sitio web oficial de Tableau. Una vez que aparezca el cuadro de diálogo para la configuración de conexión, introduzca sus credenciales de Experience Platform en los campos de parámetros para conectarse con Adobe Experience Platform. A continuación, se muestra una lista de los parámetros de conexión necesarios.

| Parámetro de conexión | Descripción |
|---|---|
| **[!DNL Server]** | La dirección de la ubicación de almacenamiento SFTP. Use el valor de su credencial **[!UICONTROL Host]** de Experience Platform. |
| **[!DNL Port]:** | El puerto de [!DNL Query Service]. Debe usar el puerto **80** o **5432** para conectarse con [!DNL Query Service]. |
| **[!DNL Database]** | Las bases de datos a las que desea acceder. Use el valor de su credencial **[!UICONTROL Database]** de Experience Platform: `prod:all`. |
| **[!DNL Authentication]:** | El método elegido para probar la identidad del usuario. Se recomienda seleccionar [!DNL Username and Password] de las opciones disponibles en el menú desplegable. |
| **[!DNL Username]** | Este es su ID de organización de Experience Platform. Use el valor de su credencial de Experience Platform **[!UICONTROL Username]**. El id. tendrá el formato `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Esta cadena alfanumérica es su credencial **[!UICONTROL Password]** de Experience Platform. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados de `technicalAccountID` y `credential` descargados en el archivo JSON de configuración. El valor de contraseña adopta la forma: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante la inicialización de la que Adobe no conserva una copia. |

Para obtener más información sobre cómo encontrar su nombre de usuario, contraseña y credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Experience Platform] y luego seleccione **[!UICONTROL Consultas]**, seguidas de **[!UICONTROL Credenciales]**.

>[!IMPORTANT]
>
>Como usuario de Tableau o Power BI, puede conectar Customer Journey Analytics a sus herramientas de BI desde la pestaña Credenciales del servicio de consulta. Consulte la documentación de credenciales para obtener instrucciones sobre cómo [conectar las herramientas de BI a Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

Asegúrese de marcar la casilla **[!UICONTROL Requerir SSL]** antes de intentar conectarse. Consulte la [documentación sobre los modos SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros al servicio Adobe Experience Platform Query.

>[!IMPORTANT]
>
>Las estructuras de datos anidadas en herramientas de BI de terceros se pueden aplanar para mejorar su facilidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos. Consulte la documentación sobre la característica [`FLATTEN` ](../key-concepts/flatten-nested-data.md) para obtener instrucciones sobre cómo activar esta configuración al conectarse a una base de datos.

Después de rellenar todas las credenciales, confirme la configuración para continuar. Ahora se ha conectado con Adobe Experience Platform.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede usar [!DNL Tableau] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [ejecutar consultas](../best-practices/writing-queries.md).
