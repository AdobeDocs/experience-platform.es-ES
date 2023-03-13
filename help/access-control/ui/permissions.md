---
keywords: Experience Platform;inicio;temas populares;perfil de producto;administrar permisos
solution: Experience Platform
title: Administración De Permisos Para Un Perfil De Producto
description: El control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para varias funcionalidades de Platform mediante Adobe Admin Console. Este documento sirve como guía para administrar permisos para un perfil de producto para Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Administración de permisos para un perfil de producto

Justo después de [creación de un nuevo perfil de producto](#create-a-new-product-profile), se le pedirá que configure los permisos del perfil. Si está editando permisos para un perfil existente, seleccione el perfil en la **[!UICONTROL Perfiles de producto]** para abrir la página de detalles del perfil y, a continuación, seleccione **[!UICONTROL Permisos]**.

![permissions](../images/permissions.png)

Los permisos se dividen en categorías y se enumeran en esta página. La lista muestra el nombre de la categoría, el número de permisos que contiene (y cuántos están activos) y su descripción.

Seleccione cualquier categoría de la lista para abrir **[!UICONTROL Editar permisos]** página.

![edit-permissions](../images/edit-permissions.png)

El **[!UICONTROL Editar permisos]** Esta página proporciona un espacio de trabajo para agregar y quitar permisos del perfil de producto seleccionado. La parte izquierda de la pantalla muestra una lista de categorías de permisos. Al seleccionar una categoría, cambian los permisos que se muestran en **[!UICONTROL Elementos de permisos disponibles]**.

Por ejemplo, para actualizar permisos para el modelado de datos, seleccione **[!UICONTROL Modelado de datos]**.

![administración de perfiles](../images/profile-management.png)

Para añadir un permiso, seleccione el signo más **(+)** junto al nombre del permiso. Como alternativa, puede seleccionar **[!UICONTROL Añadir todo]** para agregar todos los permisos de la categoría actual al perfil. Los permisos añadidos aparecen en **[!UICONTROL Elementos de permisos incluidos]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>El **[!UICONTROL Elementos de permisos incluidos]** La lista solo muestra los permisos añadidos de la categoría seleccionada actualmente.

Para quitar un permiso, seleccione la **X** junto al nombre del permiso o seleccione. **[!UICONTROL Eliminar todo]** para eliminar todos los permisos de la categoría actual. Los permisos eliminados vuelven a aparecer en **[!UICONTROL Elementos de permisos disponibles]**.

Continúe recorriendo las categorías disponibles y añadiendo los permisos que desee. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![remove-permission](../images/remove-permission.png)

El **[!UICONTROL Permisos]** vuelve a aparecer la pestaña del perfil del producto y muestra que los permisos seleccionados están activos.

![permissions-updated](../images/permissions-updated.png)

## Pasos siguientes

Con los permisos establecidos, puede continuar con el siguiente paso para [administrar detalles y servicios para un perfil de producto](details-and-services.md)
