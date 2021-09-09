---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta;editor de consultas;editor de consultas;editor de consultas;
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de consulta
topic-legacy: guide
description: El servicio de consulta de Adobe Experience Platform proporciona una interfaz de usuario que puede utilizarse para escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de la organización de IMS.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

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

Para crear un conjunto de credenciales que no caducan, seleccione **[!UICONTROL Generar credenciales]**.

>[!NOTE]
>
>Para poder crear credenciales que no caduquen, debe tener los permisos **Sandboxes** y **Administrar integración del servicio de consulta**. Para aprender a asignar estos permisos, lea la documentación sobre [Control de acceso](../../access-control/home.md).

![](../images/ui/credentials/generate-credentials.png)

Aparece el modal de generación de credenciales. Para crear credenciales que no caduquen, debe proporcionar los siguientes detalles:

- **[!UICONTROL Nombre]**: Nombre de las credenciales que está generando.
- **[!UICONTROL Descripción]**: (Opcional) Descripción de las credenciales que está generando.
- **[!UICONTROL Asignado a]**: El usuario al que se asignarán las credenciales. Este valor debe ser la dirección de correo electrónico del usuario que está creando las credenciales.
- **[!UICONTROL Contraseña]**  (opcional) Una contraseña opcional para sus credenciales. Si la contraseña no está establecida, Adobe generará automáticamente una contraseña.

Una vez que haya proporcionado todos los detalles requeridos, seleccione **[!UICONTROL Generate credentials]** para generar sus credenciales.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Una vez seleccionado el botón **[!UICONTROL Generate credentials]** , un archivo de configuración que contiene información como nombre de cuenta técnica, ID de cuenta técnica y credenciales. Dado que el Adobe **not** registra la credencial generada, **debe** almacenar de forma segura el archivo descargado y mantener un registro de la credencial.
>
>Además, si las credenciales no se utilizan durante 90 días, se cancelarán.

Ahora que ha guardado las credenciales generadas, seleccione **[!UICONTROL Cerrar]**. Ahora puede ver una lista de todas sus credenciales que no caducan.

![](../images/ui/credentials/list-credentials.png)

Puede editar o eliminar las credenciales que no caducan. Para editar una credencial que no caduque, seleccione el icono de lápiz (![](../images/ui/credentials/edit-icon.png)). Para eliminar una credencial que no caduque, seleccione el icono de eliminación (![](../images/ui/credentials/delete-icon.png)).

Al editar una credencial que no caduca, aparece un modal. Puede proporcionar los siguientes detalles para actualizar:

- **[!UICONTROL Nombre]**: Nombre de las credenciales que está generando.
- **[!UICONTROL Descripción]**: (Opcional) Descripción de las credenciales que está generando.
- **[!UICONTROL Asignado a]**: El usuario al que se asignarán las credenciales. Este valor debe ser la dirección de correo electrónico del usuario que está creando las credenciales.

![](../images/ui/credentials/update-credentials.png)

Una vez que haya proporcionado todos los detalles requeridos, seleccione **[!UICONTROL Update account]** para completar la actualización de sus credenciales.

## Uso de credenciales para conectarse a clientes externos

Puede utilizar las credenciales que caducan o que no caducan para conectarse con clientes externos, como Aqua Data Studio, Looker o Power BI.

Al conectarse a estos clientes externos, generalmente debe incluir la siguiente información:

- **Servidor/Host**: Nombre del servidor/host al que se está conectando. Este valor adopta la forma de `server.adobe.io` y se puede encontrar en **[!UICONTROL Host]** dentro de la sección de credenciales que caducan.
- **Puerto**: Puerto para el servidor/host al que se está conectando. Este valor se encuentra en **[!UICONTROL Port]** dentro de la sección de credenciales que caducan. Un valor de ejemplo para el puerto sería `80`.
- **Nombre de usuario**: El nombre de usuario del usuario que se está conectando al cliente externo. Esto toma la forma `ID@AdobeOrg` y se puede encontrar en **[!UICONTROL Nombre de usuario]** dentro de la sección de credenciales que caducan.
- **Contraseña**: La contraseña del usuario que se está conectando al cliente externo. Si está utilizando credenciales que caducan, esto se encuentra en **[!UICONTROL Contraseña]** dentro de la sección de credenciales que caducan. Si utiliza credenciales que no caducan, este valor está compuesto por el ID de cuenta técnica y la credencial en el formulario: `technicalAccountId:credential`.
- **Base de datos**: La base de datos a la que se está conectando. Este valor se puede encontrar en **[!UICONTROL Database]** dentro de la sección de credenciales que caducan. Un valor de ejemplo para la base de datos sería `prod:all`.

## Pasos siguientes

Ahora que comprende cómo funcionan las credenciales que caducan y las que no caducan, puede utilizar estas credenciales para conectarse a clientes externos. Para obtener más información detallada sobre los clientes externos, lea la [guía de conexión de clientes a Query Service](../clients/overview.md).