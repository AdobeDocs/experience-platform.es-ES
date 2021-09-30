---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta;editor de consultas;editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de consulta
topic-legacy: guide
description: El servicio de consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de la organización de IMS.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 696db8081ab8225d79cd468b7435770d407d3e3d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 1%

---

# Guía de credenciales

El servicio de consulta de Adobe Experience Platform le permite conectarse con clientes externos. Puede conectarse a estos clientes externos utilizando credenciales que caducan o credenciales que no caducan.

## Credenciales de caducidad

Puede utilizar las credenciales caducadas para configurar rápidamente una conexión con un cliente externo.

![](../images/ui/credentials/expiring-credentials.png)

La sección **[!UICONTROL Credenciales de caducidad]** proporciona la siguiente información:

- **[!UICONTROL Host]**: Nombre del host al que se conectará. Para conectarse al servicio de consulta, esto incluirá el nombre de la organización de IMS que está utilizando actualmente.
- **[!UICONTROL Puerto]**: Número de puerto del host al que se conectará.
- **[!UICONTROL Base de datos]**: Nombre de la base de datos a la que se conectará.
- **[!UICONTROL Nombre de usuario]**: El nombre de usuario que utilizará para conectarse al servicio de consulta.
- **[!UICONTROL Contraseña]**: La contraseña que utilizará para conectarse al servicio de consulta.
- **[!UICONTROL Comando]** PSQL: Un comando que ha insertado automáticamente toda la información relevante para que se conecte al servicio de consulta mediante PSQL en la línea de comandos.
- **[!UICONTROL Caduca]**: La fecha de caducidad de las credenciales que caducan. Las credenciales caducan 24 horas después de generarse.

## Credenciales que no caducan

Puede utilizar credenciales que no caduquen para configurar una conexión más permanente con un cliente externo.

### Requisitos previos

Para poder generar credenciales que no caduquen, debe completar los siguientes pasos en Adobe Admin Console:

1. Inicie sesión en [Adobe Admin Console](https://adminconsole.adobe.com/) y seleccione la organización correspondiente en la barra de navegación superior.
2. [Seleccione un perfil de producto.](../../access-control/ui/browse.md)
3. [Configure los permisos de  **** Sandboxesy  **Administrar** ](../../access-control/ui/permissions.md) integración del servicio de consultas para el perfil del producto.
4. [Agregue un nuevo usuario a un ](../../access-control/ui/users.md) perfil de producto para que se les concedan los permisos configurados.
5. [Agregue al usuario como ](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) administrador de perfiles de producto para permitir la creación de cuentas para cualquier perfil de producto activo.
6. [Añada el usuario como ](https://helpx.adobe.com/es/enterprise/using/manage-developers.html) desarrollador de perfiles de producto para crear una integración.

Para obtener más información sobre cómo asignar permisos, lea la documentación sobre [control de acceso](../../access-control/home.md).

Todos los permisos necesarios ahora están configurados en Adobe Developer Console para que el usuario utilice la función de credenciales caducadas.

### Generar credenciales

Para crear un conjunto de credenciales que no caducan, vuelva a la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Consultas]. A continuación, seleccione la pestaña **[!UICONTROL Credentials]** seguida de **[!UICONTROL Generate credentials]**.

![](../images/ui/credentials/generate-credentials.png)

Aparece un cuadro de diálogo que le permite generar credenciales. Para crear credenciales que no caduquen, debe proporcionar los siguientes detalles:

- **[!UICONTROL Nombre]**: Nombre de las credenciales que está generando.
- **[!UICONTROL Descripción]**: (Opcional) Descripción de las credenciales que está generando.
- **[!UICONTROL Asignado a]**: Usuario al que se asignarán las credenciales. Este valor debe ser la dirección de correo electrónico del usuario que está creando las credenciales.
- **[!UICONTROL Contraseña]**  (opcional) Una contraseña opcional para sus credenciales. Si la contraseña no está establecida, Adobe generará automáticamente una contraseña.

Una vez que haya proporcionado todos los detalles requeridos, seleccione **[!UICONTROL Generate credentials]** para generar sus credenciales.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Una vez seleccionado el botón **[!UICONTROL Generate credentials]** , se descarga un archivo JSON de configuración en el equipo local. Dado que el Adobe **not** registra las credenciales generadas, debe almacenar de forma segura el archivo descargado y mantener un registro de las credenciales.
>
>Además, si las credenciales no se utilizan durante 90 días, se eliminarán.

El archivo JSON de configuración contiene información como el nombre de cuenta técnica, el ID de cuenta técnica y las credenciales. Se proporciona en el siguiente formato.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Una vez guardadas las credenciales generadas, seleccione **[!UICONTROL Cerrar]**. Ahora puede ver una lista de todas sus credenciales que no caducan.

![](../images/ui/credentials/list-credentials.png)

Puede editar o eliminar las credenciales que no caducan. Para editar una credencial que no caduque, seleccione el icono de lápiz (![](../images/ui/credentials/edit-icon.png)). Para eliminar una credencial que no caduque, seleccione el icono de eliminación (![](../images/ui/credentials/delete-icon.png)).

Al editar una credencial que no caduca, aparece un modal. Puede proporcionar los siguientes detalles para actualizar:

- **[!UICONTROL Nombre]**: Nombre de las credenciales que está generando.
- **[!UICONTROL Descripción]**: (Opcional) Descripción de las credenciales que está generando.
- **[!UICONTROL Asignado a]**: Usuario al que se asignarán las credenciales. Este valor debe ser la dirección de correo electrónico del usuario que está creando las credenciales.

![](../images/ui/credentials/update-credentials.png)

Una vez que haya proporcionado todos los detalles requeridos, seleccione **[!UICONTROL Update account]** para completar la actualización de sus credenciales.

## Uso de credenciales para conectarse a clientes externos

Puede utilizar las credenciales que caducan o que no caducan para conectarse con clientes externos, como Aqua Data Studio, Looker o Power BI. El método de entrada para estas credenciales variará según el cliente externo. Consulte la documentación del cliente externo para obtener instrucciones específicas sobre el uso de estas credenciales.

La imagen indica la ubicación de cada parámetro que se encuentra en la interfaz de usuario, excepto la contraseña de las credenciales que no caducan. Aunque sus archivos de configuración JSON proporcionan credenciales que no caducan, puede ver sus credenciales que caducan en la pestaña **Credentials** de la interfaz de usuario.

![](../images/ui/credentials/expiring-credentials.png)

En la tabla siguiente se describen los parámetros que suelen ser necesarios para conectarse a clientes externos.

>[!NOTE]
>
>Cuando se conecta a un host con credenciales que no caducan, sigue siendo necesario utilizar todos los parámetros enumerados en la sección [!UICONTROL EXPIRING CREDENTIALS] excepto la contraseña y el nombre de usuario.

| Parámetro | Descripción |
|---|---|
| Servidor/Host | Nombre del servidor/host al que se está conectando. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan y adopta la forma `server.adobe.io`. El valor se encuentra en **[!UICONTROL Host]** en la sección [!UICONTROL CREDENCIALES DE CADUCIDAD].</ul></li> |
| Puerto | Puerto para el servidor/host al que se está conectando. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan, y se encuentra en **[!UICONTROL Puerto]** en la sección [!UICONTROL CREDENCIALES QUE CADUCAN]. Un valor de ejemplo para el puerto sería `80`.</ul></li> |
| Database | La base de datos a la que se está conectando. <ul><li>Este valor se utiliza tanto para credenciales que caducan como para credenciales que no caducan, y se encuentra en **[!UICONTROL Database]** en la sección [!UICONTROL EXPIRING CREDENTIALS]. Un valor de ejemplo para la base de datos sería `prod:all`.</ul></li> |
| Nombre de usuario | El nombre de usuario del usuario que se está conectando al cliente externo. <ul><li>Si está utilizando credenciales que caducan, esto toma la forma de una cadena alfanumérica antes de `@AdobeOrg`. Este valor se encuentra en **[!UICONTROL Nombre de usuario]**.</li><li>Si utiliza credenciales que no caducan, es una cadena de su elección, aunque **no puede** ser la misma que el valor `technicalAccountID` encontrado en el archivo JSON de configuración.</li></ul> |
| Contraseña | La contraseña del usuario que se está conectando al cliente externo. <ul><li>Si está utilizando credenciales que caducan, esto se encuentra en **[!UICONTROL Password]** en la sección [!UICONTROL EXPIRING CREDENTIALS].</li><li>Si utiliza credenciales que no caducan, este valor son los argumentos concatenados de technicalAccountID y las credenciales tomadas del archivo JSON de configuración. El valor de la contraseña adopta la forma: `{technicalAccountId}:{credential}`.</li></ul> |

## Pasos siguientes

Ahora que comprende cómo funcionan las credenciales que caducan y las que no caducan, puede utilizar estas credenciales para conectarse a clientes externos. Para obtener más información detallada sobre los clientes externos, lea la [guía de conexión de clientes a Query Service](../clients/overview.md).
