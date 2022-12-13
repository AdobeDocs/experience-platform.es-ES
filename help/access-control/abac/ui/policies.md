---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Administrar directivas de control de acceso
description: Este documento proporciona información sobre la administración de políticas de control de acceso a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Administrar las políticas de control de acceso

Las políticas de control de acceso son instrucciones que unen atributos para establecer acciones permisibles e inadmisibles. Las políticas de acceso pueden ser locales o globales y pueden anular otras directivas.

>[!IMPORTANT]
>
>Las políticas de acceso no deben confundirse con las políticas de uso de datos, que controlan cómo se utilizan los datos en Adobe Experience Platform en lugar de qué usuarios de la organización tienen acceso a ellos. Consulte la guía sobre la creación [políticas de uso de datos](../../../data-governance/policies/create.md) para obtener más información.

## Crear una directiva nueva

Para crear una directiva nueva, seleccione la opción **[!UICONTROL Políticas]** en la barra lateral y seleccione **[!UICONTROL Crear directiva]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

La variable **[!UICONTROL Crear una directiva nueva]** , solicitándole que escriba un nombre y una descripción opcional. Cuando termine, seleccione **[!UICONTROL Confirmar]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Con la flecha desplegable, seleccione si desea **Permita el acceso a** (![flac-allow-access-to](../../images/flac-ui/flac-permit-access-to.png)) un recurso o **Denegar acceso a** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) un recurso.

A continuación, seleccione el recurso que desee incluir en la directiva mediante el menú desplegable y busque el tipo de acceso, lea o escriba.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

A continuación, con la flecha desplegable, seleccione la condición que desee aplicar a esta directiva, **Lo siguiente es verdadero** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) o **siendo false lo siguiente** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Seleccione el icono de signo más para **Añadir expresión de coincidencias** o **Agregar grupo de expresiones** para el recurso.

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

En el menú desplegable, seleccione la opción **Recurso**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

A continuación, en la lista desplegable , seleccione la opción **Coincide**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

A continuación, en el menú desplegable, seleccione el tipo de etiqueta (**[!UICONTROL Etiqueta principal]** o **[!UICONTROL Etiqueta personalizada]**) para que coincida con la etiqueta asignada al usuario en las funciones.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finalmente, seleccione la **Sandbox** que desea que se apliquen las condiciones de directiva mediante el menú desplegable.

![flac-policy-sandboxes-desplegable](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Agregar recurso** para agregar más recursos. Una vez finalizado, seleccione **[!UICONTROL Guardar y salir]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

La nueva directiva se ha creado correctamente y se le redirige al **[!UICONTROL Políticas]** , donde verá que la política recién creada aparece en la lista.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Editar una directiva

Para editar una política existente, seleccione la política en la **[!UICONTROL Políticas]** pestaña . Como alternativa, utilice la opción de filtro para filtrar los resultados y encontrar la directiva que desea editar.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

A continuación, seleccione los puntos suspensivos (`…`) junto al nombre de las directivas y un menú desplegable muestra los controles para editar, desactivar, eliminar o duplicar la función. Seleccione Editar en la lista desplegable.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

Aparecerá la pantalla de permisos de directivas. Realice las actualizaciones y seleccione **[!UICONTROL Guardar y salir]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

La directiva se actualiza correctamente y se le redirige al **[!UICONTROL Políticas]** pestaña .

## Duplicar una directiva

Para duplicar una directiva existente, seleccione la directiva en la **[!UICONTROL Políticas]** pestaña . Como alternativa, utilice la opción de filtro para filtrar los resultados y encontrar la directiva que desea editar.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

A continuación, seleccione los puntos suspensivos (`…`) junto al nombre de una política y un menú desplegable muestra los controles para editar, desactivar, eliminar o duplicar la función. Seleccione duplicar en la lista desplegable.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

La variable **[!UICONTROL Duplicar directiva]** , pidiéndole que confirme la duplicación.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

La nueva directiva aparece en la lista como una copia del original en la **[!UICONTROL Políticas]** pestaña .

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Eliminar una directiva

Para eliminar una directiva existente, seleccione la directiva en la sección **[!UICONTROL Políticas]** pestaña . Como alternativa, utilice la opción de filtro para filtrar los resultados y encontrar la política que desea eliminar.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

A continuación, seleccione los puntos suspensivos (`…`) junto al nombre de una política y un menú desplegable muestra los controles para editar, desactivar, eliminar o duplicar la función. Seleccione eliminar en la lista desplegable.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

La variable **[!UICONTROL Eliminar directiva de usuario]** , pidiéndole que confirme la eliminación.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Volverá a la **[!UICONTROL políticas]** y aparece una confirmación de eliminación emergente.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Activar una directiva

Para activar una directiva existente, selecciónela en el **[!UICONTROL Políticas]** pestaña . Como alternativa, utilice la opción de filtro para filtrar los resultados y encontrar la política que desea eliminar.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

A continuación, seleccione los puntos suspensivos (`…`) junto al nombre de una política y un menú desplegable muestra los controles para editar, activar, eliminar o duplicar la función. Seleccione activar en la lista desplegable.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

La variable **[!UICONTROL Activar la directiva de usuario]** , pidiéndole que confirme la activación.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Volverá a la **[!UICONTROL políticas]** y aparece una ventana emergente de confirmación de activación. El estado de la directiva se muestra como activo.

![flac-policy-enabled](../../images/flac-ui/flac-policy-activated.png)

## Pasos siguientes

Con una nueva directiva creada, puede continuar con el paso siguiente a [administrar permisos para una función](permissions.md).
