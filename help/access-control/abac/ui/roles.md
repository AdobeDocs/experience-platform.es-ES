---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Control de acceso basado en atributos Crear una función
description: Administre funciones a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 13%

---

# Administrar funciones

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

Para empezar a administrar los roles, vaya a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} y seleccione **[!UICONTROL Roles]** en el panel izquierdo.

![Área de trabajo de roles con permisos.](../../images/ui/roles/roles-overview.png)

## Crear una nueva función {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Crear nueva función"
>abstract="Cree nuevas funciones para clasificar mejor a los usuarios que interactúan con la instancia de Experience Platform. Por ejemplo, puede crear una función para un equipo interno de marketing y aplicar la etiqueta RHD (datos de salud regulados) a esa función, lo que permite que su equipo interno de marketing acceda a la información de salud protegida (PHI). Como alternativa, también puede crear una función para una agencia externa y denegar el acceso de esa función a los datos de PHI al no aplicar la etiqueta RHD a esa función."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=es" text="Administrar una función"
>additional-url="https://experienceleague.adobe.com/es/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Aplicar etiquetas a una función"

Para crear un nuevo rol, seleccione **[!UICONTROL Create role]**.

>[!TIP]
>
>Las funciones de solo lectura están disponibles de forma predeterminada. Una función de solo lectura es una función que concede al usuario la capacidad de ver los datos, la configuración y las características de la interfaz de usuario sin tener la capacidad de cambiar el estado del sistema. Los administradores no pueden editar estas funciones, pero pueden asociar usuarios a las funciones.

![Espacio de trabajo del rol con la opción Crear rol resaltada.](../../images/ui/roles/roles-create-role.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Create new role]**. Escriba un(a) **[!UICONTROL Name]** para el rol y, opcionalmente, un(a) **[!UICONTROL Description]**, y después seleccione **[!UICONTROL Confirm]**.

![Cuadro de diálogo Crear nuevos roles con el nombre y la descripción rellenados y la opción Confirmar resaltada.](../../images/ui/roles/roles-create-new-role.png)

Aparece el área de trabajo **[!UICONTROL Resources]**. Busque el recurso que necesita desplazándose o introduciendo el nombre del recurso en la barra de búsqueda del panel izquierdo. Agregue recursos seleccionando el ![icono de Más](/help/images/icons/plus.png) junto al nombre del recurso.

![Espacio de trabajo de recursos con la opción Agregar de un recurso individual resaltada.](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

El recurso se agrega al espacio de trabajo principal. Seleccione el menú desplegable situado junto al nombre del recurso y seleccione los permisos que desee añadir a la función. Puede elegirlos individualmente, seleccionar **[!UICONTROL Add all]** o buscar permisos específicos introduciendo el nombre del permiso en la barra de búsqueda.

![Se expandió y resaltó el área de trabajo de recursos con el menú desplegable de un recurso individual.](../../images/ui/roles/roles-resources-permissions.png)

Continúe seleccionando todos los recursos y los permisos que desee agregar a la función. Cuando haya terminado, seleccione **[!UICONTROL Save]**.

![Espacio de trabajo de recursos con la opción Guardar resaltada.](../../images/ui/roles/roles-resources-permissions-save.png)

Recibirá una alerta que indica que la función se ha guardado correctamente. Seleccione **[!UICONTROL Close]** para volver al área de trabajo **[!UICONTROL Roles]**.

![Área de trabajo de recursos con la alerta de éxito y la opción Cerrar resaltada.](../../images/ui/roles/roles-resources-permissions-close.png)

La nueva función se ha creado correctamente y se le redirigirá a la página **[!UICONTROL Roles]**, donde verá aparecer la función recién creada en la lista.

<!-- The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on) -->

## Duplicación de un rol

Si se duplica una función, se copiarán los detalles, los permisos, las etiquetas y los entornos limitados. Los usuarios, los grupos de usuarios y las credenciales de API **no se copian** y deberán agregarse manualmente al rol.

Para duplicar un rol existente, busque el rol que desea duplicar en la ficha **[!UICONTROL Roles]**. Seleccione el ![icono Más](/help/images/icons/more.png) junto al nombre del rol y, a continuación, seleccione **[!UICONTROL Duplicate]** en el menú desplegable.

![Se expandió el área de trabajo de roles con el menú desplegable de un rol y se resaltó la opción Duplicar.](../../images/ui/roles/role-duplicate.png)

Aparecerá el cuadro de diálogo de confirmación duplicado. Seleccione **[!UICONTROL Confirm]** para terminar de duplicar el rol. La nueva función se guardará con el mismo nombre y se agregará `_Copy` como sufijo.

![Cuadro de diálogo de confirmación duplicado con la opción Confirmar resaltada.](../../images/ui/roles/role-duplicate-confirm.png)

También puede duplicar un rol desde el espacio de trabajo de un rol individual. Seleccione el rol que desea duplicar del área de trabajo **[!UICONTROL Roles]** y, a continuación, seleccione **[!UICONTROL Duplicate]**.

![Espacio de trabajo de un rol individual con la opción Duplicar resaltada.](../../images/ui/roles/role-duplicate-alt.png)

Aparecerá el cuadro de diálogo de confirmación duplicado. Seleccione **[!UICONTROL Confirm]** para terminar de duplicar el rol. Se le redirigirá a la nueva función.

![Cuadro de diálogo de confirmación duplicado con la opción Confirmar resaltada.](../../images/ui/roles/role-duplicate-alt-confirm.png)

## Eliminar un rol

Para eliminar un rol, busque el rol que desea eliminar en la ficha **[!UICONTROL Roles]**. Seleccione el ![icono Más](/help/images/icons/more.png) junto al nombre del rol y, a continuación, seleccione **[!UICONTROL Delete]** en el menú desplegable.

![Se expandió el área de trabajo de roles con el menú desplegable de un rol y se resaltó la opción Duplicar.](../../images/ui/roles/role-delete.png)

Aparecerá el cuadro de diálogo de confirmación de eliminación. Seleccione **[!UICONTROL Confirm]** para finalizar la eliminación del rol.

![Cuadro de diálogo de confirmación duplicado con la opción Confirmar resaltada.](../../images/ui/roles/role-duplicate-confirm.png)

También puede eliminar un rol desde el espacio de trabajo de un rol individual. Seleccione la función que desea eliminar del área de trabajo **[!UICONTROL Roles]** y, a continuación, seleccione **[!UICONTROL Delete]**.

![Espacio de trabajo de un rol individual con la opción Eliminar resaltada.](../../images/ui/roles/role-delete-alt.png)

Aparecerá el cuadro de diálogo de confirmación de eliminación. Seleccione **[!UICONTROL Confirm]** para finalizar la eliminación del rol.

![Cuadro de diálogo de confirmación de eliminación con la opción Confirmar resaltada.](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## Próximos pasos

Con una función nueva creada, puede continuar con el siguiente paso para [administrar permisos para una función](permissions.md).
