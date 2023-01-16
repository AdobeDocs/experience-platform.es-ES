---
keywords: Experience Platform;inicio;temas populares;tableau;Tableau;servicio de consulta;servicio de consulta;conectar con servicio de consulta;
solution: Experience Platform
title: Conexión de Tableau con el servicio de consultas
description: Este documento recorre los pasos para conectar Tableau con el servicio de consulta de Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 1d71cc4336747eb258ec2d8dcdc545cb2233692d
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connect [!DNL Tableau] al servicio de consultas

Este documento proporciona información para la conexión [!DNL Tableau] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Tableau] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Tableau] se encuentra en la variable [oficial [!DNL Tableau] documentación](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instrucciones sobre cómo [conexión a un servidor PostgreSQL con Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) puede consultarse en el sitio oficial de Tableau. Una vez que aparezca el cuadro de diálogo para la configuración de conexión, introduzca las credenciales de Platform en los campos de parámetros para conectarse con Adobe Experience Platform. A continuación se muestra una lista de los parámetros de conexión necesarios.

| Parámetro de conexión | Descripción |
|---|---|
| **[!DNL Server]** | La dirección de la ubicación de almacenamiento SFTP. Utilice el valor de su Experience Platform **[!UICONTROL Host]** credencial. |
| **[!DNL Port]:** | El puerto de [!DNL Query Service]. Debe utilizar el puerto **80** o **5432** para conectarse con [!DNL Query Service]. |
| **[!DNL Database]** | Las bases de datos a las que desee acceder. Utilice el valor de su Experience Platform **[!UICONTROL Base de datos]** credencial: `prod:all`. |
| **[!DNL Authentication]:** | Método que ha elegido para probar la identidad del usuario. Se recomienda seleccionar [!DNL Username and Password] en las opciones disponibles del menú desplegable. |
| **[!DNL Username]** | Este es su ID de organización de Platform. Utilice el valor de su Experience Platform **[!UICONTROL Nombre de usuario]** credencial. El ID tendrá el formato de `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Esta cadena alfanumérica es su Experience Platform **[!UICONTROL Contraseña]** credencial. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados del `technicalAccountID` y `credential` descargado en el archivo JSON de configuración. El valor de la contraseña adopta la forma: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante su inicialización de que el Adobe no conserva una copia de . |

Para obtener más información sobre cómo encontrar su nombre de usuario, contraseña y credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform]y, a continuación, seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Asegúrese de haber marcado la variable **[!UICONTROL Requerir SSL]** antes de intentar conectarse. Consulte la [Documentación de modos SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform.

>[!IMPORTANT]
>
>Las estructuras de datos anidadas en herramientas de BI de terceros se pueden aplanar para mejorar su capacidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos. Consulte la documentación de[`FLATTEN` función](../best-practices/flatten-nested-data.md) para obtener instrucciones sobre cómo activar esta configuración al conectarse a una base de datos.

Después de completar todas las credenciales, confirme la configuración para continuar. Ahora está conectado con Adobe Experience Platform.

## Pasos siguientes

Ahora que está conectado con [!DNL Query Service], puede usar [!DNL Tableau] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía de [ejecución de consultas](../best-practices/writing-queries.md).
