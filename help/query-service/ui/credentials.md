---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta;editor de consultas;editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de credenciales del servicio de consulta
topic-legacy: guide
description: El servicio de consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de la organización de IMS.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 344602a0e828d140ea386daf30a25b8f595f8d04
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 1%

---

# Guía de credenciales

El servicio de consulta de Adobe Experience Platform le permite conectarse con clientes externos. Puede conectarse a estos clientes externos utilizando credenciales que caducan o credenciales que no caducan.

## Credenciales de caducidad {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Modo SSL del cliente"
>abstract="SSL debe estar habilitado en los clientes conectados al servicio de consulta. Asegúrese de que el modo SSL esté configurado en &quot;Requisito&quot;."

Puede utilizar las credenciales caducadas para configurar rápidamente una conexión con un cliente externo.

![La ficha Credenciales del panel Consultas con la sección Credenciales de caducidad resaltada.](../images/ui/credentials/expiring-credentials.png)

La variable **[!UICONTROL Credenciales de caducidad]** proporciona la siguiente información:

- **[!UICONTROL Host]**: Nombre del host al que se conectará. Para conectarse al servicio de consulta, esto incluirá el nombre de la organización de IMS que está utilizando actualmente.
- **[!UICONTROL Puerto]**: Número de puerto del host al que se conectará.
- **[!UICONTROL Base de datos]**: Nombre de la base de datos a la que se conectará.
- **[!UICONTROL Nombre de usuario]**: El nombre de usuario que utilizará para conectarse al servicio de consulta.
- **[!UICONTROL Contraseña]**: La contraseña que utilizará para conectarse al servicio de consulta.
- **[!UICONTROL PSQL, comando]**: Un comando que ha insertado automáticamente toda la información relevante para que se conecte al servicio de consulta mediante PSQL en la línea de comandos.
- **[!UICONTROL Caduca]**: La fecha de caducidad de las credenciales que caducan. Las credenciales caducan 24 horas después de generarse.

## Credenciales que no caducan {#non-expiring-credentials}

Puede utilizar credenciales que no caduquen para configurar una conexión más permanente con un cliente externo.

### Requisitos previos

Para poder generar credenciales que no caduquen, debe completar los siguientes pasos en Adobe Admin Console:

1. Iniciar sesión [Adobe Admin Console](https://adminconsole.adobe.com/) y seleccione la organización correspondiente en la barra de navegación superior.
2. [Seleccione un perfil de producto.](../../access-control/ui/browse.md)
3. [Configure ambas variables **Sandboxes** y **Administrar integración del servicio de consultas** permissions](../../access-control/ui/permissions.md) para el perfil de producto.
4. [Agregar un nuevo usuario a un perfil de producto](../../access-control/ui/users.md) por lo tanto, se les conceden los permisos configurados.
5. [Agregar el usuario como administrador de perfil de producto](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) para permitir la creación de cuentas para cualquier perfil de producto activo.
6. [Agregar el usuario como desarrollador de perfiles de producto](https://helpx.adobe.com/es/enterprise/using/manage-developers.html) para crear una integración.

Para obtener más información sobre cómo asignar permisos, lea la documentación de [control de acceso](../../access-control/home.md).

Todos los permisos necesarios ahora están configurados en la consola de Adobe Developer para que el usuario utilice la función de credenciales caducadas.

### Generar credenciales

Para crear un conjunto de credenciales que no caduquen, vuelva a la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Consultas] espacio de trabajo. A continuación, seleccione la **[!UICONTROL Credenciales]** pestaña seguida de **[!UICONTROL Generar credenciales]**.

![El panel Consultas con la pestaña Credenciales y las credenciales de Generación resaltadas.](../images/ui/credentials/generate-credentials.png)

Aparece un cuadro de diálogo que le permite generar credenciales. Para crear credenciales que no caduquen, debe proporcionar los siguientes detalles:

- **[!UICONTROL Nombre]**: Nombre de las credenciales que está generando.
- **[!UICONTROL Descripción]**: (Opcional) Descripción de las credenciales que está generando.
- **[!UICONTROL Asignado a]**: Usuario al que se asignarán las credenciales. Este valor debe ser la dirección de correo electrónico del usuario que está creando las credenciales.
- **[!UICONTROL Contraseña]** (Opcional) Una contraseña opcional para sus credenciales. Si la contraseña no está establecida, Adobe generará automáticamente una contraseña.

Una vez que haya proporcionado todos los detalles requeridos, seleccione **[!UICONTROL Generar credenciales]** para generar sus credenciales.

![Se resalta el cuadro de diálogo Generar credenciales.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>When **[!UICONTROL Generar credenciales]** está seleccionado, se descarga un archivo JSON de configuración en el equipo local. Dado que el Adobe sí **not** registre las credenciales generadas, debe almacenar de forma segura el archivo descargado y guardar un registro de las credenciales.
>
>Además, si las credenciales no se utilizan durante 90 días, se eliminarán.

El archivo JSON de configuración contiene información como el nombre de cuenta técnica, el ID de cuenta técnica y las credenciales. Se proporciona en el siguiente formato.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Después de guardar las credenciales generadas, seleccione **[!UICONTROL Cerrar]**. Ahora puede ver una lista de todas sus credenciales que no caducan.

![La ficha Credenciales del panel Consultas con la sección Credenciales que no caducan resaltada.](../images/ui/credentials/list-credentials.png)

Puede editar o eliminar las credenciales que no caducan. Para editar una credencial que no caduque, seleccione el icono de lápiz (![Un icono de lápiz.](../images/ui/credentials/edit-icon.png)). Para eliminar una credencial que no caduque, seleccione el icono Eliminar (![Un icono de la papelera.](../images/ui/credentials/delete-icon.png)).

Al editar una credencial que no caduca, aparece un modal. Puede proporcionar los siguientes detalles para actualizar:

- **[!UICONTROL Nombre]**: Nombre de las credenciales que está generando.
- **[!UICONTROL Descripción]**: (Opcional) Descripción de las credenciales que está generando.
- **[!UICONTROL Asignado a]**: Usuario al que se asignarán las credenciales. Este valor debe ser la dirección de correo electrónico del usuario que está creando las credenciales.

![El cuadro de diálogo Actualizar cuenta .](../images/ui/credentials/update-credentials.png)

Una vez que haya proporcionado todos los detalles requeridos, seleccione **[!UICONTROL Actualizar cuenta]** para completar la actualización de sus credenciales.

## Usar credenciales para conectarse a clientes externos {#use-credential-to-connect}

Puede utilizar las credenciales que caducan o que no caducan para conectarse con clientes externos, como Aqua Data Studio, Looker o Power BI. El método de entrada para estas credenciales variará según el cliente externo. Consulte la documentación del cliente externo para obtener instrucciones específicas sobre el uso de estas credenciales.

La imagen indica la ubicación de cada parámetro que se encuentra en la interfaz de usuario, excepto la contraseña de las credenciales que no caducan. Aunque sus archivos de configuración JSON proporcionan credenciales que no caducan, puede ver sus credenciales que caducan en la sección **Credenciales** en la interfaz de usuario.

![La ficha Credenciales del espacio de trabajo Consultas con las credenciales caducadas resaltadas.](../images/ui/credentials/expiring-credentials.png)

En la tabla siguiente se describen los parámetros que suelen ser necesarios para conectarse a clientes externos.

>[!NOTE]
>
>Cuando se conecta a un host con credenciales que no caducan, sigue siendo necesario utilizar todos los parámetros enumerados en la variable [!UICONTROL CREDENCIALES DE CADUCIDAD] excepto la contraseña y el nombre de usuario.
>El formato para introducir el nombre de usuario y la contraseña utiliza valores separados por dos puntos, como se muestra en este ejemplo `username:{your_username}` y `password:{password_string}`.

| Parámetro | Descripción |
|---|---|
| **Servidor/Host** | Nombre del servidor/host al que se está conectando. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan, y adopta la forma de `server.adobe.io`. El valor se encuentra en **[!UICONTROL Host]** en el [!UICONTROL CREDENCIALES DE CADUCIDAD] para obtener más información.</ul></li> |
| **Puerto** | Puerto para el servidor/host al que se está conectando. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan, y se encuentra en **[!UICONTROL Puerto]** en el [!UICONTROL CREDENCIALES DE CADUCIDAD] para obtener más información. Un valor de ejemplo para el puerto sería `80`.</ul></li> |
| **Database** | La base de datos a la que se está conectando. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan, y se encuentra en **[!UICONTROL Base de datos]** en el [!UICONTROL CREDENCIALES DE CADUCIDAD] para obtener más información. Un valor de ejemplo para la base de datos sería `prod:all`.</ul></li> |
| **Nombre de usuario** | El nombre de usuario del usuario que se está conectando al cliente externo. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan. Toma la forma de una cadena alfanumérica antes de `@AdobeOrg`. Este valor se encuentra en **[!UICONTROL Nombre de usuario]**.</li></ul> |
| **Contraseña** | La contraseña del usuario que se está conectando al cliente externo. <ul><li>Si está utilizando credenciales que caducan, esto se encuentra en **[!UICONTROL Contraseña]** dentro de la variable [!UICONTROL CREDENCIALES DE CADUCIDAD] para obtener más información.</li><li>Si utiliza credenciales que no caducan, este valor son los argumentos concatenados de technicalAccountID y las credenciales tomadas del archivo JSON de configuración. El valor de la contraseña adopta la forma: `{technicalAccountId}:{credential}`.</li></ul> |

## Pasos siguientes

Ahora que comprende cómo funcionan las credenciales que caducan y las que no caducan, puede utilizar estas credenciales para conectarse a clientes externos. Para obtener más información detallada sobre los clientes externos, lea la [conectar clientes a la guía del servicio de consulta](../clients/overview.md).
