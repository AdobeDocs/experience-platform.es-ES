---
keywords: Experience Platform;inicio;temas populares;tableau;Tableau;servicio de consultas;servicio de consultas;conectarse al servicio de consultas;
solution: Experience Platform
title: Conexión de Tableau con el servicio de consultas
description: Este documento explica los pasos para conectar Tableau con el servicio de consultas de Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connect [!DNL Tableau] al servicio de consultas

Este documento proporciona información para la conexión [!DNL Tableau] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL Tableau] y están familiarizados con cómo navegar por su interfaz. Más información sobre [!DNL Tableau] se puede encontrar en la [funcionario [!DNL Tableau] documentación](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instrucciones sobre cómo [conectarse a un servidor PostgreSQL con Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) están disponibles en el sitio web oficial de Tableau. Una vez que aparezca el cuadro de diálogo de la configuración de conexión, introduzca sus credenciales de Platform en los campos de parámetros para conectarse con Adobe Experience Platform. A continuación, se muestra una lista de los parámetros de conexión necesarios.

| Parámetro de conexión | Descripción |
|---|---|
| **[!DNL Server]** | La dirección de la ubicación de almacenamiento SFTP. Utilice el valor de su Experience Platform **[!UICONTROL Host]** credencial. |
| **[!DNL Port]:** | El puerto para [!DNL Query Service]. Debe utilizar el puerto **80** o **5432** para conectar con [!DNL Query Service]. |
| **[!DNL Database]** | Las bases de datos a las que desea acceder. Utilice el valor de su Experience Platform **[!UICONTROL Base de datos]** credencial: `prod:all`. |
| **[!DNL Authentication]:** | El método elegido para probar la identidad del usuario. Se recomienda seleccionar [!DNL Username and Password] en las opciones disponibles del menú desplegable. |
| **[!DNL Username]** | Este es su ID de organización de Platform. Utilice el valor de su Experience Platform **[!UICONTROL Nombre de usuario]** credencial. El ID tendrá el formato de `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Esta cadena alfanumérica es su Experience Platform **[!UICONTROL Contraseña]** credencial. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados del `technicalAccountID` y el `credential` descargado en el archivo JSON de configuración. El valor de la contraseña adopta la forma siguiente: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante su inicialización de la que la Adobe no conserva una copia. |

Para obtener más información sobre cómo encontrar su nombre de usuario, contraseña y credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform], luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Asegúrese de haber comprobado las **[!UICONTROL Requerir SSL]** antes de intentar conectarse. Consulte la [Documentación de modos SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros con Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Las estructuras de datos anidadas en herramientas de BI de terceros se pueden aplanar para mejorar su facilidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos. Consulte la documentación de la[`FLATTEN` característica](../essential-concepts/flatten-nested-data.md) para obtener instrucciones sobre cómo activar esta configuración al conectarse a una base de datos.

Después de rellenar todas las credenciales, confirme la configuración para continuar. Ahora se ha conectado con Adobe Experience Platform.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Tableau] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [ejecución de consultas](../best-practices/writing-queries.md).
