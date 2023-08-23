---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Administrar directivas de control de acceso
description: Este documento proporciona información sobre la administración de directivas de control de acceso a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 7cafe1f7e9dd6789db4199631cb605be666ce48a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Administrar directivas de control de acceso

Las políticas de control de acceso son instrucciones que unen atributos para establecer acciones permisibles e inadmisibles. Las directivas de acceso pueden ser locales o globales, y pueden invalidar otras directivas. El Adobe proporciona una directiva predeterminada que se puede activar inmediatamente o siempre que su organización esté lista para empezar a controlar el acceso a objetos específicos en función de las etiquetas. La directiva predeterminada aprovecha las etiquetas aplicadas a los recursos para denegar el acceso a menos que los usuarios tengan una función con una etiqueta coincidente.

>[!IMPORTANT]
>
>Las políticas de acceso no se deben confundir con las políticas de uso de datos, que controlan cómo se utilizan los datos en Adobe Experience Platform en lugar de los usuarios de su organización que tienen acceso a ellos. Consulte la guía sobre creación de [políticas de uso de datos](../../../data-governance/policies/create.md) para obtener más información.

<!-- ## Create a new policy

To create a new policy, select the **[!UICONTROL Policies]** tab in the sidebar and select **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** dialog appears, prompting you to enter a name, and an optional description. When finished, select **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Using the dropdown arrow select if you would like to **Permit access to** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png)) a resource or **Deny access to** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) a resource.

Next, select the resource that you would like to include in the policy using the dropdown menu and search access type, read or write.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Next, using the dropdown arrow select the condition you would like to apply to this policy, **The following being true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) or **The following being false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Select the plus icon to **Add matches expression** or **Add expression group** for the resource. 

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Using the dropdown, select the **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Next, using the dropdown select the **Matches**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Next, using the dropdown, select the type of label (**[!UICONTROL Core label]** or **[!UICONTROL Custom label]**) to match the label assigned to the User in roles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finally, select the **Sandbox** that you would like the policy conditions to apply to, using the dropdown menu.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Add resource** to add more resources. Once finished, select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The new policy is successfully created, and you are redirected to the **[!UICONTROL Policies]** tab, where you will see the newly created policy appear in the list. 

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Edit a policy

To edit an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to the policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select edit from the dropdown.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

The policy permissions screen appears. Make the updates then select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The policy is successfully updated, and you are redirected to the **[!UICONTROL Policies]** tab.

## Duplicate a policy

To duplicate an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select duplicate from the dropdown.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** dialog appears, prompting you to confirm the duplication. 

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

The new policy appears in the list as a copy of the original on the **[!UICONTROL Policies]** tab.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Delete a policy

To delete an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to delete.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select delete from the dropdown.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** dialog appears, prompting you to confirm the deletion. 

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

You are returned to the **[!UICONTROL policies]** tab and a confirmation of deletion pop over appears.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png) -->

## Configurar la directiva de una zona protegida

>[!IMPORTANT]
>
>De forma predeterminada, la variable [!UICONTROL Inclusión automática] La función está activada para todos los clientes, lo que significa que todas las zonas protegidas se añaden a la directiva.

>[!NOTE]
>
>El **[!UICONTROL Default-Label-Based-Access-Control-Policy]** La directiva de es la única disponible para la configuración.

Para ver las zonas protegidas asociadas a una directiva, selecciónela en el **[!UICONTROL Políticas]** pestaña.

![La página de directivas muestra una lista de las directivas disponibles.](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

A continuación, seleccione la directiva y, a continuación, seleccione **[!UICONTROL Zonas protegidas]** pestaña. Se muestra una lista de los entornos limitados asociados a la directiva.

![La página de directivas muestra una lista de las directivas disponibles.](../../images/flac-ui/abac-policies-sandboxes-tab.png)

### Agregar directiva a todas las zonas protegidas

Utilice el **[!UICONTROL Inclusión automática]** active la opción **[!UICONTROL Zonas protegidas]** para activar la directiva en todas las zonas protegidas.

![El [!UICONTROL Zonas protegidas] que muestra la pestaña [!UICONTROL Inclusión automática] alternar.](../../images/flac-ui/abac-policies-auto-include.png)

El **[!UICONTROL Habilitar inclusión automática]** aparece un cuadro de diálogo que le solicita que confirme su selección. Seleccionar **[!UICONTROL Activar]** para completar la configuración.

![El [!UICONTROL Habilitar inclusión automática] resaltado de diálogo [!UICONTROL Activar].](../../images/flac-ui/abac-policies-auto-include-enable.png)

>[!SUCCESS]
>
>La directiva se activa para todas las zonas protegidas existentes y se agregará automáticamente a cualquier zona protegida nueva cuando esté disponible.

### Agregar directiva para seleccionar zonas protegidas

>[!IMPORTANT]
>
>Las zonas protegidas futuras no se incluirán en la directiva de forma predeterminada si [!UICONTROL Inclusión automática] la opción está desactivada. Deberá administrar y agregar entornos limitados manualmente a la directiva.

Utilice el **[!UICONTROL Inclusión automática]** active la opción **[!UICONTROL Zonas protegidas]** para deshabilitar la directiva en todas las zonas protegidas.

![El [!UICONTROL Zonas protegidas] que muestra la pestaña [!UICONTROL Inclusión automática] alternar.](../../images/flac-ui/abac-policies-auto-include.png)

Desde el **[!UICONTROL Zonas protegidas]** pestaña, seleccione **[!UICONTROL Agregar zonas protegidas]** para seleccionar las zonas protegidas a las que se aplicará esta directiva.

![El [!UICONTROL Zonas protegidas] pestaña que muestra una lista de zonas protegidas agregadas a la directiva.](../../images/flac-ui/abac-policies-sandboxes-tab-add.png)

Aparecerá una lista de zonas protegidas. Seleccione la zona protegida que desee añadir en la lista. También puede utilizar la barra de búsqueda para buscar la zona protegida. Seleccione **[!UICONTROL Guardar]**.

![El [!UICONTROL Agregar zonas protegidas] página que muestra una lista de las zonas protegidas existentes disponibles para agregar a la directiva.](../../images/flac-ui/abac-policies-sandboxes-list.png)

>[!SUCCESS]
>
>Las zonas protegidas seleccionadas se han agregado correctamente a la directiva.

### Eliminación de zonas protegidas de una directiva

Para quitar una zona protegida, seleccione la **X** junto al nombre de la zona protegida.

![El [!UICONTROL Zonas protegidas] pestaña que muestra una lista de zonas protegidas, resaltando la [!UICONTROL X] para eliminar.](../../images/flac-ui/abac-policies-remove-sandbox-x.png)

El **[!UICONTROL Eliminar]** aparece un cuadro de diálogo que le solicita que confirme su selección. Seleccionar **[!UICONTROL Confirmar]** para completar la eliminación.

![El [!UICONTROL Eliminar] resaltado de diálogo [!UICONTROL Confirmar].](../../images/flac-ui/abac-policies-remove-sandbox.png)

>[!SUCCESS]
>
>La zona protegida seleccionada se ha eliminado correctamente de la directiva.

## Activar una directiva

Para activar una directiva existente, selecciónela en el **[!UICONTROL Políticas]** pestaña.

![flac-policy-select](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

A continuación, seleccione los puntos suspensivos (`…`) junto al nombre de una directiva y un menú desplegable muestra controles para editar, activar, eliminar o duplicar la función. Seleccione activar en el menú desplegable.

![flac-policy-activate](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

El **[!UICONTROL Activar directiva]** aparece un cuadro de diálogo que le solicita que confirme la activación.

![flac-policy-activate-confirm](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


Se le devolverá a la **[!UICONTROL directivas]** y aparece una ventana emergente de confirmación de activación. El estado de la política se muestra como activa.

![flac-policy-activated](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## Pasos siguientes

Con una directiva activada, puede continuar con el siguiente paso para [administrar permisos para una función](permissions.md).
