---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Administrar directivas de control de acceso
description: Administre las políticas de control de acceso a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: b0094920720c54990953f79de32ab95c2a5c7e1c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# Administrar directivas de control de acceso

Las políticas de control de acceso son instrucciones que unen atributos para establecer acciones permisibles e inadmisibles. Adobe proporciona una directiva predeterminada que se puede activar inmediatamente o cuando su organización está lista para empezar a controlar el acceso a objetos específicos en función de [labels](./labels.md){target="_blank"}. La directiva predeterminada **[!UICONTROL Default-Label-Based-Access-Control-Policy]** aprovecha las etiquetas aplicadas a los recursos para denegar el acceso a menos que los usuarios tengan un rol con una etiqueta coincidente.

>[!IMPORTANT]
>
>Las políticas de control de acceso no deben confundirse con las políticas de uso de datos, que controlan cómo se utilizan los datos en Adobe Experience Platform. Consulte la guía sobre la creación de [políticas de uso de datos](../../../data-governance/policies/create.md){target="_blank"} para obtener más información.

## Configurar la directiva de una zona protegida {#configure-policy}

>[!NOTE]
>
>La directiva **[!UICONTROL Default-Label-Based-Access-Control-Policy]** es la única disponible actualmente para la configuración.

Para comenzar a configurar una directiva, vaya a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleccione **[!UICONTROL Policies]** del panel izquierdo. Seleccione **[!UICONTROL Default-Label-Based-Access-Control-Policy]** de la lista.

![Espacio de trabajo de directivas que muestra una lista de directivas existentes.](../../images/ui/policies/policies-home.png){zoomable="yes"}

Aparecerá el espacio de trabajo de detalles de la directiva. Seleccione el **[!UICONTROL Sandboxes]**. Se muestra una lista de los entornos limitados asociados a la directiva.

![Espacio de trabajo de la zona protegida de la directiva que muestra una lista de zonas protegidas asociadas.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Agregar directiva a todas las zonas protegidas {#add-policy-to-all}

>[!IMPORTANT]
>
>De forma predeterminada, **[!UICONTROL Auto-include]** está activado, lo que significa que todas las zonas protegidas actuales y futuras se agregan automáticamente a la directiva.

Desactive la característica **[!UICONTROL Auto-include]** para evitar que las zonas protegidas futuras se agreguen automáticamente a la directiva. Al desactivar la característica **, no se** quitará ninguna zona protegida de la directiva.

![Pestaña de zona protegida de la directiva con la opción de inclusión automática resaltada y en estado &quot;desactivado&quot;.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Si **[!UICONTROL Auto-include]** no está activo en una directiva, puede usar la opción para volver a activarlo. Aparecerá el cuadro de diálogo **[!UICONTROL Enable Auto-include]** pidiéndole que confirme su selección. Seleccione **[!UICONTROL Enable]** para completar la configuración.

>[!NOTE]
>
>Se volverán a agregar todas las zonas protegidas que quitó de la directiva mientras se desactivó **[!UICONTROL Auto-include]**.

![Cuadro de diálogo Habilitar inclusión automática con la opción Habilitar resaltada.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Seleccionar manualmente zonas protegidas para una directiva {#manually-select-sandboxes}

Para agregar o quitar manualmente zonas protegidas a una directiva, la opción **[!UICONTROL Auto-include]** **debe** estar desactivada.

#### Agregar zonas protegidas

Para agregar zonas protegidas a una directiva, seleccione **[!UICONTROL Add Sandboxes]**.

![Espacio de trabajo de la directiva con la opción Agregar zonas protegidas resaltada.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Aparecerá el cuadro de diálogo **[!UICONTROL Add Sandboxes]**. Seleccione las zonas protegidas que desee agregar a la directiva y luego seleccione **[!UICONTROL Save]**.

![Cuadro de diálogo Agregar zonas protegidas con una zona protegida seleccionada y la opción Guardar resaltada.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Si ya se han añadido a la directiva todas las zonas protegidas disponibles, verá el mensaje &quot;No tiene nada en la biblioteca&quot; en el cuadro de diálogo.

#### Eliminar zonas protegidas

Para quitar las zonas protegidas de una directiva, búsquelas de la lista y, a continuación, seleccione el icono **X**.

![Lista de zonas protegidas de la directiva con una &quot;x&quot; resaltada para quitar una zona protegida.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Confirm]** para finalizar la eliminación de la zona protegida de la directiva.

![Cuadro de diálogo de confirmación de una zona protegida con la opción Confirmar resaltada.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Activar una política {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="¿Qué son las directivas?"
>abstract="Las directivas son declaraciones que reúnen atributos para establecer acciones permitidas y no permitidas. Cada organización viene con una directiva predeterminada que debe activar para comenzar a controlar el acceso a objetos específicos en función de las etiquetas. Las etiquetas aplicadas a los recursos deniegan el acceso a menos que se asigne a los usuarios una función con una etiqueta coincidente. Las directivas no se pueden editar ni eliminar, pero se pueden activar o desactivar."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/labels?lang=es" text="Administrar etiquetas"

Para activar una directiva existente, selecciónela en la ficha **[!UICONTROL Policies]** de **[!UICONTROL Permissions]**. El estado de activación de la directiva es visible en la sección **[!UICONTROL Status]**.

![Espacio de trabajo de directivas con el estado de una directiva resaltado.](../../images/ui/policies/policy-status.png){zoomable="yes"}

Se mostrará el espacio de trabajo de detalles de la política. Seleccione **[!UICONTROL Activate]**.

![Espacio de trabajo de detalles de la directiva con la opción Activar resaltada.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

Aparecerá el cuadro de diálogo **[!UICONTROL Activate Policy]**. Seleccione **[!UICONTROL Confirm]** para finalizar la activación de la directiva.

![Cuadro de diálogo Activar directiva con la opción Confirmar resaltada.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Próximos pasos

Con una directiva activada, puede continuar con el siguiente paso para [administrar permisos para un rol](permissions.md).

<!--Policies are applied at the sandbox level to control which sandboxes enforce label-based access control. By default, the **[!UICONTROL Auto-include]** feature is turned on, which means all current and future sandboxes are automatically added to the policy. When **[!UICONTROL Auto-include]** is turned off, only the sandboxes you manually add will be subject to the policy's access control rules.

To begin configuring a policy's sandboxes, navigate to **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Select **[!UICONTROL Policies]** from the left panel, then select the **[!UICONTROL Default-Label-Based-Access-Control-Policy]** from the list.

The policy's details workspace appears. Select the **[!UICONTROL Sandboxes]** tab to view the list of sandboxes associated with the policy and access the sandbox configuration options.

### Manage Auto-include {#manage-auto-include}

To control which sandboxes are included in a policy, you can toggle the **[!UICONTROL Auto-include]** feature on or off. When you toggle off **[!UICONTROL Auto-include]**, future sandboxes will not be automatically added to the policy. However, toggling off the feature **will not** remove any sandboxes that are already included in the policy.

To re-enable **[!UICONTROL Auto-include]**, use the toggle to turn it back on. The **[!UICONTROL Enable Auto-include]** dialog appears prompting you to confirm your selection. Select **[!UICONTROL Enable]** to complete the configuration setting.

>[!NOTE]
>
>When you re-enable **[!UICONTROL Auto-include]**, any sandboxes you previously removed from the policy will be re-added.

### Manually manage sandboxes {#manually-manage-sandboxes}

When **[!UICONTROL Auto-include]**is turned off, you can manually add or remove specific sandboxes from the policy. This gives you precise control over which sandboxes enforce the policy's access control rules.

>[!NOTE]
>
>To manually add or remove sandboxes, the **[!UICONTROL Auto-include]** toggle **must** be off.

**To add sandboxes:**

Select **[!UICONTROL Add Sandboxes]** from the policy's sandbox workspace.

The **[!UICONTROL Add Sandboxes]** dialog appears, displaying your library of available sandboxes. Select the sandbox(es) you wish to add to the policy and then select **[!UICONTROL Save]**.

>[!NOTE]
>
>If all available sandboxes are already included in the policy, you will see a "You have nothing in your library" message within the dialog.

**To remove sandboxes:**

Find the sandbox you wish to remove from the list and select the **X** icon next to its name.

A confirmation dialog will appear. Select **[!UICONTROL Confirm]** to finish removing the sandbox from the policy.

-->