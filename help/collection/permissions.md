---
title: Administración de permisos para la recopilación de datos en Experience Platform
description: Una descripción general de alto nivel de cómo administrar permisos y controlar el acceso a las funciones de recopilación de datos en Adobe Experience Platform.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 28%

---

# Administración de permisos para la recopilación de datos en Experience Platform {#permission-management}

>[!CONTEXTUALHELP]
>id="platform_tags_permissions"
>title="Permisos"
>abstract="Comprenda los permisos clave necesarios para trabajar con flujos de datos, esquemas, identidades y zonas protegidas en Adobe Experience Platform."

[La recopilación de datos en Adobe Experience Platform](./home.md) se compone de diferentes tecnologías que trabajan juntas para recopilar y transferir los datos. El acceso a estas tecnologías se controla mediante permisos granulares basados en funciones en Adobe Admin Console.

Esta guía muestra cómo administrar permisos para funciones de recopilación de datos.

## Introducción

Para configurar el control de acceso para la recopilación de datos, debe tener privilegios de administrador para una organización que tenga una integración de productos con la recopilación de datos de Adobe Experience Platform. La función mínima que puede conceder o retirar permisos es la de **administrador de perfil de producto**. Otras funciones de administrador que pueden administrar permisos son **administradores de productos** (puede administrar todos los perfiles de un producto) y **administradores del sistema** (sin restricciones). Consulte el artículo sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) en la Guía de administración de Adobe Enterprise para obtener más información.

En esta guía se asume que está familiarizado con los conceptos básicos de Admin Console, como los perfiles de producto y la forma en que se conceden los permisos de producto a los usuarios y grupos individuales. Para obtener más información, consulte la [Guía del usuario de Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

## Permisos disponibles

Los permisos relevantes para la recopilación de datos se proporcionan mediante dos designaciones de productos en Admin Console: **Adobe Experience Platform** y **Recopilación de datos de Adobe Experience Platform**. Las secciones siguientes describen los permisos proporcionados en relación con cada producto, así como las descripciones de las capacidades específicas a las que otorgan acceso.

### Permisos de Adobe Experience Platform

Los permisos de Adobe Experience Platform incluyen el acceso a flujos de datos, identidades, esquemas y zonas protegidas. Para ver los pasos sobre cómo configurar los permisos de Adobe Experience Platform, consulte la [guía del usuario de control de acceso](../access-control/ui/overview.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| Zonas protegidas | (N/D) | Según las [zonas protegidas](../sandboxes/home.md) que se hayan creado en su organización, puede controlar el acceso a cada una de ellas mediante esta categoría de permisos en Admin Console. |
| Modelado de datos | Administrar esquemas | Concede la capacidad de ver, crear y editar [esquemas XDM (Experience Data Model)](../xdm/home.md). |
| Modelado de datos | Esquemas de vista | Otorga acceso de solo lectura a los esquemas. |
| Identity Management | Administrar áreas de nombres de identidad | Concede la capacidad de ver, crear y editar [áreas de nombres de identidad](../identity-service/features/namespaces.md). |
| Identity Management | Ver áreas de nombres de identidad | Otorga acceso de solo lectura a las áreas de nombres de identidad. |
| Recopilación de datos | Administrar flujos de datos | Concede la capacidad de ver, crear y editar [flujos de datos](../datastreams/overview.md). |
| Recopilación de datos | Ver flujos de datos | Otorga acceso de solo lectura a las secuencias de datos. |

{style="table-layout:auto"}

### Permisos de recopilación de datos Adobe Experience Platform

Los permisos en Recopilación de datos de Adobe Experience Platform controlan el acceso a las etiquetas y las funciones de reenvío de eventos, incluidas las propiedades, extensiones y entornos. Para ver los pasos sobre cómo configurar los permisos de recopilación de datos de Adobe Experience Platform, consulte la [sección siguiente](#manage).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| Plataformas | Web | Otorga acceso a [propiedades web](../tags/ui/administration/companies-and-properties.md) cuando se combinan con otros derechos de propiedad. |
| Plataformas | Dispositivo móvil | Otorga acceso a [propiedades móviles](../tags/ui/administration/companies-and-properties.md) cuando se combinan con otros derechos de propiedad. |
| Plataformas | Edge | Otorga acceso a [propiedades Edge del reenvío de eventos](../tags/ui/event-forwarding/getting-started.md) cuando se combina con otros derechos de propiedad. |
| Propiedades | (N/D) | Según las propiedades que se hayan creado en su organización, puede controlar el acceso a cada una de ellas a través de esta categoría de permisos en Admin Console.<br><br>Los derechos de propiedad asignados a un usuario sólo se aplican a las propiedades a las que se les ha concedido acceso a través de esta categoría de permisos. |
| Derechos de propiedad | Aprobar | Concede la capacidad de aprobar una compilación de biblioteca como parte del [flujo de publicación](../tags/ui/publishing/publishing-flow.md). |
| Derechos de propiedad | Desarrollo | Concede la capacidad de desarrollar una compilación de biblioteca como parte del [flujo de publicación](../tags/ui/publishing/publishing-flow.md). |
| Derechos de propiedad | Editar propiedad | Concede la capacidad de editar la configuración básica de las propiedades a las que un usuario tiene acceso. |
| Derechos de propiedad | Administrar entornos | Concede la capacidad de administrar los [entornos](../tags/ui/publishing/environments.md) para las propiedades a las que un usuario tiene acceso. |
| Derechos de propiedad | Administración de extensiones | Concede la capacidad de administrar las [extensiones](../tags/ui/managing-resources/extensions/overview.md) para las propiedades a las que un usuario tiene acceso. |
| Derechos de propiedad | Publicación | Concede la capacidad de publicar una compilación de biblioteca como parte del [flujo de publicación](../tags/ui/publishing/publishing-flow.md). |
| Derechos de compañía | Desarrollo de extensiones | Concede la capacidad de crear y modificar paquetes de extensión que sean propiedad de su organización, incluidas versiones privadas y solicitudes de lanzamiento público. |
| Derechos de compañía | Administrar configuraciones de aplicación | Este permiso solo es aplicable si tiene una licencia para Adobe Journey Optimizer u otra solución que conceda acceso a la mensajería móvil en la aplicación y a la mensajería push. Esto le permite administrar las aplicaciones que Adobe Experience Cloud conoce, así como las credenciales push necesarias para comunicarse con el servicio Firebase Cloud Messaging y el servicio de notificaciones push de Apple. |
| Derechos de compañía | Administrar propiedades | Concede la capacidad de crear y administrar etiquetas (propiedad web), reenvío de eventos (propiedad edge) y propiedades móviles. |

{style="table-layout:auto"}

>[!NOTE]
>
>Para obtener más información sobre cómo estos permisos afectan a las capacidades de las etiquetas, incluidas las estrategias de administración para escenarios comunes, consulte la documentación de etiquetas sobre [permisos de usuario](../tags/ui/administration/user-permissions.md).

## Administración de permisos {#manage}

Los permisos para la recopilación de datos se administran mediante dos designaciones de productos: **Adobe Experience Platform** y **Recopilación de datos de Adobe Experience Platform**.

Consulte las subsecciones siguientes para ver los pasos sobre cómo administrar los permisos relevantes en cada producto en Admin Console:

* [Permisos de Adobe Experience Platform](#manage-platform)
* [Permisos de recopilación de datos Adobe Experience Platform](#manage-collection)

### Administración de permisos en Adobe Experience Platform {#manage-platform}

>[!NOTE]
>
>Para administrar permisos para una función, necesitará derechos de administrador. Si no tiene privilegios de administrador, póngase en contacto con el administrador del sistema.

La sección **[!UICONTROL Permisos]** de Experience Cloud le permite definir roles de usuario y directivas para administrar el acceso a características y objetos dentro de una aplicación de producto.

Mediante [!UICONTROL Permisos], puede crear y administrar roles y asignar los permisos de recursos deseados para estos roles.

![Adobe Experience Cloud resalta el producto Permisos.](./images/permissions/permissions-product.png)

Para tener acceso a las características de recopilación de datos, debe habilitar todos los permisos en las categorías **[!UICONTROL zonas protegidas]**, **[!UICONTROL Modelado de datos]**, **[!UICONTROL Identity Management]** y **[!UICONTROL Recopilación de datos]**.

![Imagen que muestra la tarjeta de producto de recopilación de datos en Admin Console](./images/permissions/platform-permission-card.png)

Consulte la [guía de la interfaz de usuario de control de acceso](../access-control/ui/overview.md) para obtener instrucciones detalladas sobre la administración de permisos de Experience Platform.

>[!NOTE]
>
>Según los SKU de producto a los que tenga acceso su organización, es posible que no tenga todos los permisos de Experience Platform disponibles para usted.

### Administración de permisos en Recopilación de datos de Adobe Experience Platform {#manage-collection}

Para administrar estos permisos, inicia sesión en Admin Console, selecciona **[!UICONTROL Productos]** en la barra de navegación superior y luego selecciona **[!UICONTROL Recopilación de datos de Adobe Experience Platform]**.

![Imagen que muestra la tarjeta de producto de recopilación de datos en Admin Console](./images/permissions/data-collection-card.png)

#### Seleccione o cree un perfil de producto

La siguiente pantalla muestra una lista de perfiles de producto disponibles para la recopilación de datos en su organización, siendo el perfil predeterminado **[!DNL Default Data Collection All Access]**. Puede elegir editar el perfil de producto predeterminado si lo desea, o bien seleccionar **[!UICONTROL Nuevo perfil]** para crear uno. Si tiene varias funciones o grupos de usuarios en su organización que requieren diferentes niveles de acceso, debe crear un perfil de producto independiente para cada uno de ellos.

![Imagen que muestra los perfiles de producto para la recopilación de datos en Admin Console](./images/permissions/new-profile.png)

Después de seleccionar o crear un perfil de producto, puedes usar los iconos de **[!UICONTROL Editar]** para iniciar [permisos de edición](#edit-permissions) para el perfil, o seleccionar la pestaña **[!UICONTROL Usuarios]** para iniciar [la asignación de usuarios](#assign-users) al perfil.

![Imagen que muestra la pestaña de permisos de un Admin Console de perfil de producto](./images/permissions/edit-permission-categories.png)

#### Edición de permisos para el perfil del producto {#edit-permissions}

Al editar permisos para un perfil, los permisos disponibles se incluyen en la columna izquierda, mientras que los que se incluyen en el perfil se incluyen en la columna derecha. Seleccione los permisos de la lista para moverlos entre cualquiera de las columnas.

![Imagen que muestra los permisos agregados en la columna incluida](./images/permissions/added-permissions.png)

Los permisos se organizan en categorías. Para cambiar entre categorías, seleccione la que desee en el panel de navegación izquierdo.

![Imagen que muestra la sección de derechos de compañía en permisos](./images/permissions/switch-category.png)

Seleccionar **[!UICONTROL Guardar]** una vez que haya terminado de configurar los permisos.

![Imagen que muestra la configuración de permisos que se está guardando para el perfil del producto](./images/permissions/save-permissions.png)

La vista de perfil de producto vuelve a aparecer con los permisos añadidos reflejados.

![Imagen que muestra los permisos añadidos para el perfil del producto](./images/permissions/permissions-added.png)

#### Asignación de usuarios al perfil de producto {#assign-users}

Para asignar usuarios al perfil de producto (y concederles los permisos configurados del perfil), seleccione la pestaña **[!UICONTROL Usuarios]**, y a continuación **[!UICONTROL Agregar usuario]**.

![Imagen que muestra la pestaña de usuarios de un perfil de producto en Admin Console](./images/permissions/manage-users.png)

Para obtener más información sobre la administración de usuarios para un perfil de producto, consulte la [Documentación de Admin Console](https://helpx.adobe.com/es/enterprise/using/manage-product-profiles.html).

## Pasos siguientes

En esta guía se explican los permisos disponibles para la recopilación de datos y cómo administrarlos a través de Admin Console. Para obtener más información sobre la administración de permisos para otras funcionalidades de Adobe Experience Platform, consulte la [documentación de control de acceso](../access-control/home.md).
