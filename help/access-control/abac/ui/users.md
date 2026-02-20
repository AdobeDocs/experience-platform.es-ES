---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Control de acceso basado en atributos Administrar usuarios
description: Administre usuarios y grupos de usuarios a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: 16450867-040a-4be1-a6c0-f03d0a1b90ba
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 4%

---

# Administrar usuarios y agregar grupos de usuarios {#manage-users}

>[!CONTEXTUALHELP]
>id="platform_permissions_users_about"
>title="¿Qué son los usuarios?"
>abstract="Los usuarios son las personas que tienen acceso a Experience Platform. El acceso de un usuario individual a los recursos de una organización se administra mediante las funciones."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/roles?lang=es" text="Administrar funciones"

Los usuarios son las personas que tienen acceso a Adobe Experience Platform. El acceso de un usuario individual a los recursos de una organización se administra mediante [roles](./roles.md){target="_blank"}. Una organización también puede crear [grupos de usuarios](#user-groups) para dar acceso sin problemas a varios usuarios al mismo tiempo. Los usuarios se administran en Admin Console y los usuarios asociados a la tarjeta de producto de Adobe Experience Platform aparecen como parte de la lista de usuarios en Experience Platform.

## Administrar usuarios

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform users. To add users to Experience Platform, navigate to Adobe Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add users through the Admin Console, follow the [adding users to Experience Platform](...){#target="_blank"} guide.
-->

Para ver los usuarios de tu organización, ve a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleccione **[!UICONTROL Users]** en el panel izquierdo.

![El área de trabajo de usuarios con permisos.](../../images/ui/users/users-overview.png){zoomable="yes"}

Aparecerá una lista de usuarios. Seleccione el usuario que desee ver en la lista. También puede utilizar la barra de búsqueda para buscar el usuario introduciendo su nombre o dirección de correo electrónico.

La ficha **[!UICONTROL Details]** proporciona información general del usuario. La descripción general muestra los estados **[!UICONTROL Name]**, **[!UICONTROL Preferred languages]**, **[!UICONTROL Account Type]**, **[!UICONTROL Authentication ID]**, **[!UICONTROL Email]**, **[!UICONTROL Email verified]**, **[!UICONTROL Country code]** y **[!UICONTROL Phone number]** del usuario.

![Espacio de trabajo de detalles de un usuario.](../../images/ui/users/user-details.png){zoomable="yes"}

Seleccione la ficha **[!UICONTROL Roles]** para ver los roles a los que está asignado el usuario.

![Espacio de trabajo de funciones de un usuario.](../../images/ui/users/user-roles.png){zoomable="yes"}

### Agregar una función a un usuario {#add-user-role}

Para agregar un rol al usuario, seleccione **[!UICONTROL Add Roles]**.

![Espacio de trabajo del rol del usuario con la opción Agregar roles resaltada.](../../images/ui/users/user-add-roles.png){zoomable="yes"}

Aparecerá el cuadro de diálogo **[!UICONTROL Add Roles]**. Seleccione los roles que desea agregar al usuario y luego seleccione **[!UICONTROL Save]**.

![Cuadro de diálogo Agregar roles con los roles seleccionados y la opción de guardar resaltada.](../../images/ui/users/user-roles-add-roles-confirm.png){zoomable="yes"}

### Quitar una función de un usuario {#remove-user-role}

Para quitar un rol del usuario, seleccione el **X** junto al nombre del rol.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW

>[!NOTE]
>
>Role's that have been added to a user through a user group cannot be removed through the user's role workspace. Role's that have been added through a user group will have an [!Info icon](/help/images/icons/info.png) beside the **X** containing information about the associated user group. To remove the role, the role would need to be [removed from the user group](#remove-user-group-role).
-->

![Área de trabajo de roles de un usuario con la opción de eliminación de un rol resaltada.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Confirm]** para finalizar la eliminación del rol.

![Cuadro de diálogo de confirmación para quitar un rol con la opción Confirmar resaltada.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

## Administrar grupos de usuarios {#user-groups}

Los grupos de usuarios son varios usuarios que se han agrupado y tienen acceso para ejecutar las mismas funciones.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform user groups. To add user groups to Experience Platform, navigate to Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add user groups in the Admin Console, follow the [adding user groups to Experience Platform](...){#target="_blank"} guide.
 -->

Para ver los usuarios de su organización, vaya a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleccione **[!UICONTROL Groups]** en la sección **[!UICONTROL Users]** del panel izquierdo.

![El espacio de trabajo de grupos de usuarios con permisos.](../../images/ui/users/user-groups-overview.png){zoomable="yes"}

Aparecerá una lista de grupos de usuarios. Seleccione el grupo que desee ver en la lista.

La ficha **[!UICONTROL Details]** proporciona información general sobre el grupo de usuarios. La descripción general muestra **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL User Count]** y **[!UICONTROL Admin count]** de los grupos.

![Espacio de trabajo de detalles del grupo de usuarios.](../../images/ui/users/user-group-details.png){zoomable="yes"}

Seleccione la ficha **[!UICONTROL Users]** para ver una lista de los usuarios asignados al grupo.

![Espacio de trabajo de usuarios de un grupo de usuarios.](../../images/ui/users/user-group-users.png){zoomable="yes"}

Seleccione la ficha **[!UICONTROL Roles]** para ver la lista de funciones asignadas actualmente al grupo.

![Espacio de trabajo de funciones de un grupo de usuarios.](../../images/ui/users/user-group-roles.png){zoomable="yes"}

### Agregar funciones a un grupo de usuarios {#add-user-group-role}

Para agregar una función nueva al grupo, seleccione **[!UICONTROL Add Roles]**.

![Espacio de trabajo de roles de un grupo de usuarios con la opción Agregar roles resaltada.](../../images/ui/users/user-group-add-roles.png){zoomable="yes"}

Aparecerá el cuadro de diálogo **[!UICONTROL Add Roles]**. Seleccione los roles que desea agregar y luego seleccione **[!UICONTROL Save]**. Se agregarán las funciones para todos los usuarios que pertenezcan al grupo de usuarios.

![Cuadro de diálogo Agregar roles con un rol seleccionado y la opción Guardar resaltada.](../../images/ui/users/user-group-add-roles-select.png){zoomable="yes"}

### Eliminación de funciones de un grupo de usuarios {#remove-user-group-role}

Para quitar un rol del grupo de usuarios, seleccione el **X** junto al nombre del rol.

![Área de trabajo de funciones de un grupo de usuarios con la opción de quitar un rol resaltada.](../../images/ui/users/user-group-remove-role.png){zoomable="yes"}

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Confirm]** para finalizar la eliminación del rol.

![Cuadro de diálogo de confirmación para quitar un rol con la opción Confirmar resaltada.](../../images/ui/users/user-group-remove-role-confirm.png){zoomable="yes"}

## Credenciales de API

>[!IMPORTANT]
>
>Solo los administradores del sistema tienen la capacidad de ver y administrar credenciales de API en Permisos.

Para utilizar las API de Experience Platform como usuario o desarrollador, un administrador del sistema debe agregar credenciales de API además del conjunto de permisos dado de una función. Los permisos le permiten asignar a las funciones las credenciales de API creadas anteriormente y asignadas al producto de Experience Platform. Para obtener una guía completa sobre cómo crear y asignar credenciales de API, así como los permisos necesarios, consulte el tutorial paso a paso en [autenticar y acceder a las API de Experience Platform](/help/landing/api-authentication.md){target="_blank"}.

Para ver las credenciales de la API de su organización asociadas con Experience Platform, vaya a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleccione **[!UICONTROL API Credentials]** de la sección **[!UICONTROL Users]** en el panel izquierdo.

![El espacio de trabajo de credenciales de API con permisos.](../../images/ui/users/api-credentials-overview.png){zoomable="yes"}

>[!NOTE]
>
> Para ver las credenciales de API de su organización en todos los productos de su organización, o para obtener más información sobre las credenciales, seleccione **[!UICONTROL Edit in admin console]**.

Aparecerá una lista de credenciales de API. Seleccione la credencial de la API que desee ver en la lista.

La ficha **[!UICONTROL Details]** proporciona información general sobre las credenciales de la API. La descripción general muestra **[!UICONTROL Name]**, **[!UICONTROL Modified]** fecha, **[!UICONTROL Modified By]** atributo, **[!UICONTROL Created]** fecha, **[!UICONTROL Created by]** atributo, **[!UICONTROL API key]**, **[!UICONTROL Technical ID]** y **[!UICONTROL Email]** de las credenciales.

![Espacio de trabajo de detalles de una credencial de API.](../../images/ui/users/api-credential-details.png){zoomable="yes"}

Seleccione la pestaña **[!UICONTROL Roles]** Aparecerá una lista de funciones asociadas a la credencial de la API.

![Área de trabajo de funciones de una credencial de API.](../../images/ui/users/api-credential-roles.png){zoomable="yes"}

### Agregar una función a una credencial de API {#add-api-credential-role}

Para agregar un rol a la credencial de la API, seleccione **[!UICONTROL Add Roles]**.

![Espacio de trabajo de la credencial de API con la opción Agregar roles resaltada.](../../images/ui/users/api-credential-add-roles.png){zoomable="yes"}

Aparecerá el cuadro de diálogo **[!UICONTROL Add Roles]**. Seleccione los roles que desea agregar al usuario y luego seleccione **[!UICONTROL Save]**.

![Cuadro de diálogo Agregar roles con los roles seleccionados y la opción de guardar resaltada.](../../images/ui/users/api-credential-add-roles-select.png){zoomable="yes"}

### Quitar una función de una credencial de API {#remove-api-credential-role}

Para quitar un rol de la credencial de API, seleccione el **X** junto al nombre de la credencial de API.

![Área de trabajo de funciones de una credencial de API con la opción de quitar un rol resaltada.](../../images/ui/users/api-credential-remove-role.png){zoomable="yes"}

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Confirm]** para finalizar la eliminación del rol.

![Cuadro de diálogo de confirmación para quitar un rol con la opción Confirmar resaltada.](../../images/ui/users/api-credential-remove-role-confirm.png){zoomable="yes"}

## Próximos pasos

Ahora sabe cómo ver los detalles y las funciones de un usuario, un grupo de usuarios y las credenciales de la API. Para obtener más información sobre el control de acceso basado en atributos, consulte la [descripción general del control de acceso basado en atributos](../overview.md).

<!--
The following video is intended to support your understanding of developer and API credentials.

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)
-->