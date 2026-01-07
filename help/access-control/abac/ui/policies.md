---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Administrar directivas de control de acceso
description: Administre las políticas de control de acceso a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 8%

---

# Administrar directivas de control de acceso

Las políticas de control de acceso son instrucciones que unen atributos para establecer acciones permisibles e inadmisibles. Adobe proporciona una directiva predeterminada que se puede activar inmediatamente o cuando su organización está lista para empezar a controlar el acceso a objetos específicos en función de [labels](./labels.md){target="_blank"}. La directiva predeterminada **[!UICONTROL Default-Label-Based-Access-Control-Policy]** aprovecha las etiquetas aplicadas a los recursos para denegar el acceso a menos que los usuarios tengan un rol con una etiqueta coincidente.

>[!IMPORTANT]
>
>Las políticas de control de acceso no deben confundirse con las políticas de uso de datos, que controlan cómo se utilizan los datos en Adobe Experience Platform. Consulte la guía sobre la creación de [políticas de uso de datos](../../../data-governance/policies/create.md){target="_blank"} para obtener más información.

## Configuración de zonas protegidas para una directiva {#configure-policy}

Las políticas se aplican en el nivel de zona protegida para controlar qué zonas protegidas aplican un control de acceso basado en etiquetas. De forma predeterminada, la característica **[!UICONTROL Auto-include]** está activada, lo que significa que todas las zonas protegidas actuales y futuras se agregan automáticamente a la directiva. Cuando **[!UICONTROL Auto-include]** está desactivado, solo las zonas protegidas que agregue manualmente estarán sujetas a las reglas de control de acceso de la directiva.

>[!NOTE]
>
>La directiva **[!UICONTROL Default-Label-Based-Access-Control-Policy]** es la única disponible actualmente para la configuración.

Para comenzar a configurar las zonas protegidas de una directiva, vaya a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleccione **[!UICONTROL Policies]** del panel izquierdo y, a continuación, seleccione **[!UICONTROL Default-Label-Based-Access-Control-Policy]** de la lista.

![Espacio de trabajo de directivas que muestra una lista de directivas existentes.](../../images/ui/policies/policies-home.png){zoomable="yes"}

Aparecerá el espacio de trabajo de detalles de la política. Seleccione la pestaña **[!UICONTROL Sandboxes]** para ver la lista de zonas protegidas asociadas con la directiva y acceder a las opciones de configuración de la zona protegida.

![Espacio de trabajo de la zona protegida de la directiva que muestra una lista de zonas protegidas asociadas.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Administrar la inclusión automática {#manage-auto-include}

>[!IMPORTANT]
>
>De forma predeterminada, **[!UICONTROL Auto-include]** está activado, lo que significa que todas las zonas protegidas actuales y futuras se agregan automáticamente a la directiva.

Para controlar qué zonas protegidas se incluyen en una directiva, puede activar o desactivar la característica **[!UICONTROL Auto-include]**. Al desactivar **[!UICONTROL Auto-include]**, las zonas protegidas futuras no se agregarán automáticamente a la directiva. Sin embargo, si se desactiva la función **, no se** quitará ninguna zona protegida que ya esté incluida en la directiva.

![Pestaña de zona protegida de la directiva con la opción de inclusión automática resaltada y en estado &quot;desactivado&quot;.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Para volver a habilitar **[!UICONTROL Auto-include]**, use la opción para volver a activarlo. Aparecerá el cuadro de diálogo **[!UICONTROL Enable Auto-include]** pidiéndole que confirme su selección. Seleccione **[!UICONTROL Enable]** para completar la configuración.

>[!NOTE]
>
>Al volver a habilitar **[!UICONTROL Auto-include]**, se volverán a agregar las zonas protegidas que quitó anteriormente de la directiva.

![Cuadro de diálogo Habilitar inclusión automática con la opción Habilitar resaltada.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Administrar zonas protegidas manualmente {#manually-manage-sandboxes}

Cuando **[!UICONTROL Auto-include]** está desactivado, puede agregar o quitar manualmente zonas protegidas específicas de la directiva. Esto le proporciona un control preciso sobre los entornos limitados que aplican las reglas de control de acceso de la directiva.

>[!NOTE]
>
>Para agregar o quitar zonas protegidas manualmente, la opción **[!UICONTROL Auto-include]** **debe** estar desactivada.

**Para agregar zonas protegidas:**

Seleccione **[!UICONTROL Add Sandboxes]** del espacio de trabajo de la zona protegida de la directiva.

![Espacio de trabajo de la directiva con la opción Agregar zonas protegidas resaltada.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Aparecerá el cuadro de diálogo **[!UICONTROL Add Sandboxes]**, que mostrará la biblioteca de zonas protegidas disponibles. Seleccione las zonas protegidas que desee agregar a la directiva y luego seleccione **[!UICONTROL Save]**.

![Cuadro de diálogo Agregar zonas protegidas con una zona protegida seleccionada y la opción Guardar resaltada.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Si todas las zonas protegidas disponibles ya están incluidas en la directiva, verá el mensaje &quot;No tiene nada en la biblioteca&quot; dentro del cuadro de diálogo.

**Para quitar zonas protegidas:**

Busque la zona protegida que desee eliminar de la lista y seleccione el icono **X** junto a su nombre.

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
