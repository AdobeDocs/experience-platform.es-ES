---
keywords: Experience Platform;inicio;temas populares;perfil de producto;administrar permisos
solution: Experience Platform
title: Administrar Permisos Para Un Perfil De Producto
topic-legacy: user guide
description: El control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funcionalidades de Platform mediante Adobe Admin Console. Este documento sirve como guía para administrar los permisos de un perfil de producto para Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 099bfc0098ebf5a2325f344215c6b21f1c347473
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Administrar permisos para un perfil de producto

Inmediatamente después de [crear un nuevo perfil de producto](#create-a-new-product-profile), se le pedirá que configure los permisos del perfil. Si está editando permisos para un perfil existente, seleccione el perfil en la pestaña **[!UICONTROL Product Profiles]** para abrir la página de detalles del perfil y, a continuación, seleccione **[!UICONTROL Permissions]**.

![permissions](../images/permissions.png)

Los permisos se dividen en categorías y se enumeran en esta página. La lista muestra el nombre de la categoría, el número de permisos que contiene (y cuántos están activos) y su descripción.

Seleccione cualquier categoría de la lista para abrir la página **[!UICONTROL Editar permisos]**.

![edit-permissions](../images/edit-permissions.png)

La página **[!UICONTROL Editar permisos]** proporciona un espacio de trabajo para agregar y quitar permisos del perfil de producto seleccionado. La parte izquierda de la pantalla muestra una lista de categorías de permisos. Al seleccionar una categoría, se cambian los permisos que se muestran en **[!UICONTROL Elementos de permisos disponibles]**.

Por ejemplo, para actualizar los permisos para Administración de perfiles, seleccione **[!UICONTROL Administración de perfiles]**.

![administración de perfiles](../images/profile-management.png)

Para agregar un permiso, seleccione el icono más **(+)** junto al nombre del permiso. Como alternativa, puede seleccionar **[!UICONTROL Agregar todo]** para agregar todos los permisos de la categoría actual al perfil. Los permisos añadidos aparecen en **[!UICONTROL Elementos de permisos incluidos]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>La lista **[!UICONTROL Elementos de permisos incluidos]** solo muestra los permisos agregados de la categoría seleccionada actualmente.

Para quitar un permiso, seleccione el icono **X** junto al nombre del permiso o seleccione **[!UICONTROL Quitar todo]** para eliminar todos los permisos de la categoría actual. Los permisos eliminados vuelven a aparecer en **[!UICONTROL Elementos de permisos disponibles]**.

Continúe pasando por las categorías disponibles y agregando los permisos que desee. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![remove-permission](../images/remove-permission.png)

La pestaña **[!UICONTROL Permisos]** del perfil del producto vuelve a aparecer y muestra que los permisos seleccionados ya están activos.

![permissions-update](../images/permissions-updated.png)

## Pasos siguientes

Con los permisos establecidos, puede continuar con el siguiente paso para [administrar detalles y servicios para un perfil de producto](details-and-services.md)
