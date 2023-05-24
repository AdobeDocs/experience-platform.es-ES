---
keywords: Experience Platform;inicio;temas populares;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Autenticar el conector de origen de Marketo
description: Este documento proporciona información sobre cómo generar las credenciales de autenticación de Marketo.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Autentique su [!DNL Marketo Engage] conector de origen

Antes de crear un [!DNL Marketo Engage] (en lo sucesivo, &quot;[!DNL Marketo]&quot;), primero debe configurar un servicio personalizado a través del [!DNL Marketo] , así como recuperar valores para su ID de Munchkin, ID de cliente y secreto de cliente.

La siguiente documentación proporciona pasos sobre cómo adquirir credenciales de autenticación para crear una [!DNL Marketo] conector de origen.

## Configurar una función nueva

El primer paso para adquirir sus credenciales de autenticación es configurar una nueva función a través de [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) interfaz.

Iniciar sesión en [!DNL Marketo] y seleccione **[!DNL Admin]** en la barra de navegación superior.

![Administrador para un nuevo rol](../images/marketo/home.png)

El *[!DNL Users & Role]s* contiene información sobre usuarios, funciones e historiales de inicio de sesión. Para crear una función nueva, seleccione **[!DNL Roles]** en el encabezado superior y, a continuación, seleccione **[!DNL New Role]**.

![new-role](../images/marketo/new-role.png)

Aparece el cuadro de diálogo **[!DNL Create New Role]**. Proporcione un nombre y una descripción y, a continuación, seleccione los permisos que desee conceder para esta función. Los permisos están restringidos a espacios de trabajo específicos y los usuarios solo pueden realizar acciones en espacios de trabajo en los que tienen permisos.

Una vez seleccionados los permisos que desea conceder, seleccione **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

Puede administrar permisos restringidos en la API al crear funciones con [!DNL Marketo]. En lugar de seleccionar &quot;API de acceso&quot;, puede proporcionar a un rol el nivel mínimo de acceso seleccionando los siguientes permisos:

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## Configuración de un nuevo usuario

De forma similar a las funciones, puede configurar un nuevo usuario desde el **[!DNL Users & Roles]** página. El **[!DNL Users]** Esta página proporciona una lista de los usuarios activos que están aprovisionados actualmente en Marketo. Seleccionar **[!DNL Invite New User]** para aprovisionar un nuevo usuario.

![invite-new-user](../images/marketo/invite-new-user.png)

Aparecerá un menú de diálogo emergente. Proporcione la información adecuada para su correo electrónico, nombre, apellidos y motivo. Durante este paso, también puede establecer una fecha de caducidad para el acceso de la nueva cuenta de usuario que está invitando. Cuando termine, seleccione **[!DNL Next]**.

>[!IMPORTANT]
>
>Al configurar un usuario nuevo, debe asignar acceso a un usuario que esté dedicado estrictamente al servicio personalizado que está creando.

![user-info](../images/marketo/new-user-info.png)

Seleccione los campos adecuados en la **[!DNL Permissions]** y, a continuación, seleccione la **[!DNL API Only]** para proporcionar una función de API al nuevo usuario. Seleccionar **[!DNL Next]** para continuar.

![permissions](../images/marketo/permissions.png)

Para completar el proceso, seleccione **[!DNL Send]**.

![message](../images/marketo/message.png)

## Configurar un servicio personalizado

Una vez que haya establecido un nuevo usuario, puede configurar un servicio personalizado para recuperar las nuevas credenciales. En la página de administración, seleccione **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

El **[!DNL Installed services]** página contiene una lista de servicios existentes. Para crear un nuevo servicio personalizado, seleccione **[!DNL New]** y luego seleccione **[!DNL New Service]**.

![new-service](../images/marketo/new-service.png)

Proporcione un nombre descriptivo al nuevo servicio y seleccione **[!DNL Custom]** desde el **[!DNL Service]** menú desplegable. Proporcione una descripción adecuada y, a continuación, seleccione el usuario que desee aprovisionar en la **[!DNL API Only User]** menú desplegable. Una vez que haya rellenado los detalles necesarios, seleccione **[!DNL Create]** para crear su nuevo servicio personalizado.

![create](../images/marketo/create.png)

## Obtenga su ID de cliente y secreto de cliente

Con un nuevo servicio personalizado creado, ahora puede recuperar valores para el ID de cliente y el secreto de cliente. Desde el **[!DNL Installed Services]** , busque el servicio personalizado al que desee acceder y, a continuación, seleccione **[!DNL View Details]**.

![view-details](../images/marketo/view-details.png)

Aparece un cuadro de diálogo que contiene su ID de cliente y secreto de cliente.

![credenciales](../images/marketo/credentials.png)

## Obtén tu Munchkin ID

El paso final debe completarse para autenticar su [!DNL Marketo] El conector de origen es para recuperar su ID de Munchkin. En la página de administración, seleccione **[!DNL Munchkin]** en el **[!DNL Integration]** panel.

![admin-munchkin](../images/marketo/admin-munchkin.png)

El *[!DNL Munchkin]* Aparecerá la página con su ID de Munchkin único en la parte superior del panel.

![munchkin-Id](../images/marketo/munchkin-id.png)

Combinado con su ID de cliente y secreto de cliente, puede usar su ID de Munchkin para configurar una nueva cuenta y [crear un nuevo [!DNL Marketo] conexión de origen](../../../tutorials/ui/create/adobe-applications/marketo.md) en el Experience Platform.
