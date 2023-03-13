---
title: Administración de permisos para el Privacy Service
description: Obtenga información sobre cómo administrar permisos de usuario para Adobe Experience Platform Privacy Service mediante Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: ebcfdc9f73fc9120cf3819169d72bd828d0b35a6
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# Administración de permisos para el Privacy Service

Acceso a [Adobe Experience Platform Privacy Service](./home.md) se controla mediante permisos granulares basados en funciones en Adobe Admin Console. Al crear perfiles de producto que asignan permisos a grupos de usuarios, puede determinar quién tiene acceso a qué funciones del Privacy Service [IU](./ui/overview.md) y [API](./api/overview.md).

>[!NOTE]
>
>Al crear una integración para la API de Privacy Service, debe seleccionar un perfil de producto existente para determinar para qué funciones o acciones tiene permisos esa integración. Consulte la guía de [introducción a la API de Privacy Service](./api/getting-started.md) para obtener más información.

Esta guía muestra cómo administrar permisos para Privacy Service.

## Primeros pasos

Para configurar el control de acceso de Privacy Service, debe tener privilegios de administrador en una organización que tenga una integración de productos con Adobe Experience Platform Privacy Service. La función mínima que puede conceder o retirar permisos es una **administrador de perfil de producto**. Otras funciones de administrador que pueden administrar permisos son **administradores de productos** (puede administrar todos los perfiles de un producto) y **administradores del sistema** (sin restricciones). Consulte el artículo sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) en la Guía de administración de Adobe Enterprise para obtener más información.

En esta guía se da por hecho que está familiarizado con conceptos básicos de Admin Console, como los perfiles de producto y cómo conceden permisos de producto a usuarios y grupos individuales. Para obtener más información, consulte la [Guía del usuario del Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

## Permisos disponibles

En la tabla siguiente se describen los permisos disponibles para los Privacy Service con descripciones de las funciones específicas a las que conceden acceso:

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de lectura de privacidad] | Determina si el usuario puede ver las solicitudes de acceso y eliminación existentes, junto con sus detalles. |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de escritura de privacidad] | Determina si un usuario puede crear nuevas solicitudes de acceso y eliminación. |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de lectura (acceso) de entrega de contenido] | Cuando el Privacy Service procesa una solicitud de acceso, se envía a ese cliente un archivo ZIP que contiene los datos del cliente. Al buscar los detalles de una solicitud de acceso, este permiso determina si el usuario puede acceder al vínculo de descarga del archivo ZIP de la solicitud. |
| [!UICONTROL Permisos de exclusión de venta] | [!UICONTROL Permiso de lectura: Desactivar la venta] | Determina si el usuario puede ver las solicitudes de exclusión de la venta existentes, junto con sus detalles. |
| [!UICONTROL Permisos de exclusión de venta] | [!UICONTROL Permiso de escritura: exclusión de la venta] | Determina si un usuario puede crear nuevas solicitudes de exclusión de la venta. |

{style="table-layout:auto"}

## Administración de permisos {#manage}

Para administrar permisos de Privacy Service, inicie sesión en [Admin Console](https://adminconsole.adobe.com/) y seleccione **[!UICONTROL Productos]** desde la barra de navegación superior. Desde aquí, seleccione **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Imagen que muestra la tarjeta de producto de Privacy Service en Admin Console](./images/permissions/privacy-service-card.png)

### Seleccione o cree un perfil de producto

La siguiente pantalla muestra una lista de perfiles de producto disponibles para los Privacy Service de su organización. Si no existen perfiles de producto, seleccione **[!UICONTROL Nuevo perfil]** para crear uno. Si tiene varias funciones o grupos de usuarios en su organización que requieren diferentes niveles de acceso, debe crear un perfil de producto independiente para cada uno de ellos.

![Imagen que muestra los perfiles de producto del Privacy Service en Admin Console](./images/permissions/select-or-create-profile.png)

Después de seleccionar un perfil de producto, puede usar el **[!UICONTROL Permisos]** pestaña para iniciar [editar permisos](#edit-permissions) para el perfil o seleccione la opción **[!UICONTROL Usuarios]** pestaña para iniciar [asignación de usuarios](#assign-users) al perfil.

![Imagen que muestra la pestaña de permisos de un Admin Console de perfil de producto](./images/permissions/users-permissions-tabs.png)

### Edición de permisos para el perfil {#edit-permissions}

En el **[!UICONTROL Permisos]** , seleccione cualquiera de las categorías de permisos mostradas para acceder a la vista de edición de permisos.

Al editar permisos para un perfil, los permisos disponibles se enumeran en la columna izquierda, mientras que los que se incluyen en el perfil se enumeran en la columna derecha. Seleccione los permisos de la lista para moverlos entre cualquiera de las columnas.

![Imagen que muestra las columnas de permisos disponibles e incluidas](./images/permissions/edit-permissions.png)

Los permisos se organizan en categorías. Para cambiar entre categorías, seleccione la categoría que desee en el panel de navegación izquierdo.

![Imagen que muestra el [!UICONTROL Desactivar la venta] sección en permisos](./images/permissions/switch-category.png)

Seleccionar **[!UICONTROL Guardar]** una vez que haya terminado de configurar los permisos.

![Imagen que muestra la configuración de permisos que se está guardando para el perfil del producto](./images/permissions/save-permissions.png)

La vista de perfil de producto vuelve a aparecer con los permisos añadidos reflejados.

![Imagen que muestra los permisos añadidos para el perfil del producto](./images/permissions/permissions-added.png)

### Asignación de usuarios al perfil {#assign-users}

Para asignar usuarios al perfil de producto (y concederles los permisos configurados del perfil), seleccione **[!UICONTROL Usuarios]** pestaña, seguido de **[!UICONTROL Agregar usuario]**.

![Imagen que muestra la pestaña de usuarios de un perfil de producto en Admin Console](./images/permissions/manage-users.png)

Para obtener más información sobre la administración de usuarios para un perfil de producto, consulte la [Documentación del Admin Console](https://helpx.adobe.com/es/enterprise/using/manage-product-profiles.html).

### Migración de credenciales de API heredadas al perfil {#migrate-tech-accounts}

>[!NOTE]
>
>Esta sección solo se aplica a las credenciales de API existentes que se crearon antes de que los permisos de Privacy Service se integraran en Adobe Admin Console. Para las nuevas credenciales, los perfiles de producto (y sus permisos) se asignan mediante [Proyectos de la consola Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/projects/) en su lugar.<br><br>Consulte la sección sobre [asignación de perfiles de producto a un proyecto](./api/getting-started.md#product-profiles) en la Guía de introducción a la API de Privacy Service para obtener más información.

Para migrar credenciales de API heredadas al perfil de producto, seleccione **[!UICONTROL Credenciales de API]**, seguido de **[!UICONTROL Añadir credenciales de API]**.

![[!UICONTROL Añadir credenciales de API] que se está seleccionando en Admin Console, en [!UICONTROL Credenciales de API] para un perfil de producto](./images/permissions/api-credentials.png)

Elija los proyectos de Developer Console que desee en la lista y, a continuación, seleccione **[!UICONTROL Guardar]** para añadirlos al perfil de producto. Todas las llamadas a la API que utilicen las credenciales de estos proyectos heredarán los permisos granulares otorgados por el perfil del producto.

## Pasos siguientes

Esta guía abarcaba los permisos disponibles para Privacy Service y cómo administrarlos mediante Admin Console.

Para ver los pasos sobre cómo crear una nueva integración de API después de configurar perfiles de producto, consulte la [guía de introducción para la API de Privacy Service](./api/getting-started.md). Para obtener más información sobre la administración de permisos para otras funcionalidades de Adobe Experience Platform, consulte la [documentación de control de acceso](../access-control/home.md).
