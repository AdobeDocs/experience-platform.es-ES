---
title: Administrar permisos para Privacy Service
description: Obtenga información sobre cómo administrar los permisos de usuario para Adobe Experience Platform Privacy Service mediante Adobe Admin Console.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Administrar permisos para Privacy Service

Acceso a [Adobe Experience Platform Privacy Service](./home.md) se controla mediante permisos granulares basados en funciones en Adobe Admin Console. Al crear perfiles de producto que asignen permisos a grupos de usuarios, puede determinar quién tiene acceso a qué funciones del Privacy Service [IU](./ui/overview.md) y [API](./api/overview.md).

>[!NOTE]
>
>Al crear una integración para la API de Privacy Service, debe seleccionar un perfil de producto existente para determinar para qué características o acciones tiene permisos la integración. Consulte la guía de [introducción a la API de Privacy Service](./api/getting-started.md) para obtener más información.

Esta guía le muestra cómo administrar los permisos para Privacy Service.

## Primeros pasos

Para configurar el control de acceso para Privacy Service, debe tener privilegios de administrador para una organización que tenga una integración de producto con Adobe Experience Platform Privacy Service. La función mínima que puede conceder o retirar permisos es una **administrador de perfiles de producto**. Otras funciones de administrador que pueden administrar permisos son **administradores de productos** (puede administrar todos los perfiles de un producto) y **administradores del sistema** (sin restricciones). Consulte el artículo sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) en la guía de administración de Adobe Enterprise para obtener más información.

En esta guía se da por hecho que está familiarizado con conceptos básicos de Admin Console como perfiles de producto y cómo conceden permisos de producto a usuarios y grupos individuales. Para obtener más información, consulte la [Guía del usuario del Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

## Permisos disponibles

La siguiente tabla describe los permisos disponibles para el Privacy Service con descripciones de las funciones específicas a las que concede acceso:

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de lectura de privacidad] | Determina si el usuario puede ver solicitudes de acceso y eliminación existentes, junto con sus detalles. |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de escritura de privacidad] | Determina si un usuario puede crear nuevas solicitudes de acceso y eliminación. |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de lectura (acceso) de la entrega de contenido] | Cuando el Privacy Service procesa una solicitud de acceso, se envía a ese cliente un archivo ZIP que contiene los datos del cliente. Al buscar los detalles de una solicitud de acceso, este permiso determina si el usuario puede acceder al vínculo de descarga del archivo ZIP de la solicitud. |
| [!UICONTROL Permisos de exclusión de venta] | [!UICONTROL Permiso de lectura: exclusión de la venta] | Determina si el usuario puede ver solicitudes de exclusión de venta existentes, junto con sus detalles. |
| [!UICONTROL Permisos de exclusión de venta] | [!UICONTROL Permiso de escritura - Exclusión de venta] | Determina si un usuario puede crear nuevas solicitudes de exclusión de la venta. |

{style=&quot;table-layout:auto&quot;}

## Administración de permisos {#manage}

Para administrar los permisos de Privacy Service, inicie sesión en [Admin Console](https://adminconsole.adobe.com/) y seleccione **[!UICONTROL Productos]** desde la barra de navegación superior. Desde aquí, seleccione **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Imagen que muestra la tarjeta de producto del Privacy Service en el Admin Console](./images/permissions/privacy-service-card.png)

### Seleccionar o crear un perfil de producto

La siguiente pantalla muestra una lista de perfiles de producto disponibles para el Privacy Service de su organización. Si no existen perfiles de producto, seleccione **[!UICONTROL Nuevo perfil]** para crear uno. Si tiene varias funciones o grupos de usuarios en su organización que requieren diferentes niveles de acceso, debe crear un perfil de producto independiente para cada uno de ellos.

![Imagen que muestra los perfiles de producto para el Privacy Service en el Admin Console](./images/permissions/select-or-create-profile.png)

Después de seleccionar un perfil de producto, puede usar la variable **[!UICONTROL Permisos]** pestaña para empezar [editar permisos](#edit-permissions) para el perfil o seleccione la **[!UICONTROL Usuarios]** pestaña para empezar [asignación de usuarios](#assign-users) al perfil.

![Imagen que muestra la ficha permisos de un Admin Console de perfiles de producto](./images/permissions/users-permissions-tabs.png)

### Editar permisos para el perfil {#edit-permissions}

En el **[!UICONTROL Permisos]** , seleccione cualquiera de las categorías de permisos mostradas para acceder a la vista de edición de permisos.

Al editar permisos para un perfil, los permisos disponibles se enumeran en la columna izquierda, mientras que los que se incluyen en el perfil se enumeran en la columna derecha. Seleccione los permisos enumerados para moverlos entre cualquiera de las columnas.

![Imagen que muestra las columnas de permisos disponibles e incluidas](./images/permissions/edit-permissions.png)

Los permisos se organizan en categorías. Para cambiar entre categorías, seleccione la categoría que desee en el panel de navegación izquierdo.

![Imagen que muestra la variable [!UICONTROL Exclusión de la venta] sección en permisos](./images/permissions/switch-category.png)

Select **[!UICONTROL Guardar]** una vez que haya terminado de configurar los permisos.

![Imagen que muestra la configuración de permisos que se está guardando para el perfil del producto](./images/permissions/save-permissions.png)

La vista de perfil del producto vuelve a aparecer con los permisos añadidos reflejados.

![Imagen que muestra los permisos añadidos para el perfil del producto](./images/permissions/permissions-added.png)

### Asignar usuarios al perfil {#assign-users}

Para asignar usuarios al perfil de producto (y otorgarles los permisos configurados del perfil), seleccione la opción **[!UICONTROL Usuarios]** , seguido de **[!UICONTROL Agregar usuario]**.

![Imagen que muestra la pestaña de usuarios para un perfil de producto en Admin Console](./images/permissions/manage-users.png)

Para obtener más información sobre la administración de usuarios para un perfil de producto, consulte la [documentación del Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### Migración de credenciales de API heredadas al perfil {#migrate-tech-accounts}

>[!NOTE]
>
>Esta sección solo se aplica a las credenciales de API existentes creadas antes de que los permisos de Privacy Service se integraran en Adobe Admin Console. Para nuevas credenciales, los perfiles de producto (y sus permisos) se asignan mediante [Proyectos de la consola de Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/projects/) en su lugar.<br><br>Consulte la sección sobre [asignación de perfiles de producto a un proyecto](./api/getting-started.md#product-profiles) en la guía de introducción a la API de Privacy Service para obtener más información.

Para migrar credenciales de API heredadas al perfil de producto, seleccione **[!UICONTROL Credenciales de API]**, seguido de **[!UICONTROL Agregar credenciales de API]**.

![[!UICONTROL Agregar credenciales de API] seleccionado en Admin Console, en la sección [!UICONTROL Credenciales de API] pestaña para un perfil de producto](./images/permissions/api-credentials.png)

Elija los proyectos de Developer Console que desee en la lista y, a continuación, seleccione **[!UICONTROL Guardar]** para agregarlos al perfil de producto. Todas las llamadas de API que utilicen las credenciales de estos proyectos heredarán los permisos granulares otorgados por el perfil del producto.

## Pasos siguientes

Esta guía abarcaba los permisos disponibles para Privacy Service y cómo administrarlos a través de Admin Console.

Para ver los pasos sobre cómo crear una nueva integración de API después de configurar perfiles de producto, consulte la [guía de introducción a la API de Privacy Service](./api/getting-started.md). Para obtener más información sobre la administración de permisos para otras funciones de Adobe Experience Platform, consulte la [documentación de control de acceso](../access-control/home.md).
