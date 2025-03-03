---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Control de acceso basado en atributos Crear una función
description: Este documento proporciona información sobre la administración de funciones a través de la interfaz Permisos en Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 74980c6108a32ec6736ab5892d89590e04e8a500
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 23%

---

# Administrar funciones

Las funciones definen el acceso que un administrador, un especialista o un usuario final tiene a los recursos de su organización. En un entorno de control de acceso basado en funciones, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y a los miembros de su organización se les puede asignar una o más funciones, según el ámbito de vista o acceso de escritura que necesiten.

## Crear una nueva función {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Crear nueva función"
>abstract="Cree nuevas funciones para clasificar mejor a los usuarios que interactúan con la instancia de Platform. Por ejemplo, puede crear una función para un equipo interno de marketing y aplicar la etiqueta RHD (datos de salud regulados) a esa función, lo que permite que su equipo interno de marketing acceda a la información de salud protegida (PHI). Como alternativa, también puede crear una función para una agencia externa y denegar el acceso de esa función a los datos de PHI al no aplicar la etiqueta RHD a esa función."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=es" text="Administrar una función"
>additional-url="https://experienceleague.adobe.com/es/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Aplicar etiquetas a una función"

Para crear una función nueva, seleccione la ficha **[!UICONTROL Funciones]** en la barra lateral y seleccione **[!UICONTROL Crear función]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Crear un nuevo rol]**, en el que se le pedirá que escriba un nombre y una descripción opcional.

Cuando termine, seleccione **[!UICONTROL Confirmar]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

A continuación, seleccione los permisos de recurso que desea incluir en la función mediante el menú desplegable.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Para agregar recursos adicionales, selecciona **[!UICONTROL Adobe Experience Platform]** en el panel de navegación izquierdo, que muestra una lista de recursos. También puede introducir el nombre del recurso en la barra de búsqueda del panel de navegación izquierdo.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Haga clic en el recurso correspondiente, arrástrelo y suéltelo en el panel principal.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Seleccione los permisos de recurso que desee incluir en la función mediante el menú desplegable. Repita este proceso para todos los recursos que desee incluir en el rol. Cuando termine, seleccione **[!UICONTROL Guardar y salir]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

La nueva función se ha creado correctamente y se le redirigirá a la página **[!UICONTROL Funciones]**, donde verá aparecer la función recién creada en la lista.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Consulte las secciones sobre [administración de permisos para una función](#manage-permissions-for-a-role) para obtener más información sobre cómo administrar permisos de funciones una vez creados.

El siguiente vídeo tiene como objetivo ayudarle a comprender la creación de una función nueva y a administrar usuarios para esa función.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Duplicación de un rol

Para duplicar un rol existente, seleccione el rol en la ficha **[!UICONTROL Roles]**. También puede utilizar la opción de filtro para filtrar los resultados y encontrar la función que desea duplicar.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

A continuación, seleccione **[!UICONTROL Duplicate]** en la parte superior derecha de la pantalla.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

Aparece el cuadro de diálogo **[!UICONTROL Duplicar rol]**, que le solicita que confirme la duplicación.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

A continuación, se le redirigirá a la página de detalles de la función, donde podrá cambiar el nombre y los permisos de la función. Los detalles, las etiquetas y las zonas protegidas se duplican con respecto a la función anterior. Los usuarios deberán añadirse a través de la pestaña usuarios. Puede ver el documento [administrar permisos para una función](permissions.md) para obtener más información sobre cómo agregar detalles, etiquetas, zonas protegidas y usuarios a una función.

Haga clic en la flecha izquierda para volver a la ficha **[!UICONTROL Roles]**.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

El nuevo rol aparecerá en la lista de la página **[!UICONTROL Roles]**.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Eliminar un rol

Seleccione los puntos suspensivos (`…`) junto al nombre de un rol y aparecerá una lista desplegable con controles para editar, eliminar o duplicar el rol. Seleccione eliminar de la lista desplegable.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Eliminar función de usuario]**, que le pedirá que confirme la eliminación.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Volverá a la ficha **[!UICONTROL Roles]**.

## Pasos siguientes

Con una función nueva creada, puede continuar con el siguiente paso para [administrar permisos para una función](permissions.md).
