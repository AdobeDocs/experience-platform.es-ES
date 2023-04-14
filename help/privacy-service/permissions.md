---
title: Administrar permisos para Privacy Service
description: Obtenga información sobre cómo administrar los permisos de usuario para Adobe Experience Platform Privacy Service mediante Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 1%

---

# Administrar permisos para Privacy Service

>[!IMPORTANT]
>
>Se han mejorado los permisos de Adobe Experience Platform Privacy Service para aumentar su nivel de granularidad. Estos cambios permiten a los administradores de la organización conceder acceso a más usuarios con la función y el nivel de permiso deseados. Los usuarios de cuentas técnicas deben actualizar sus permisos de Privacy Service, ya que esta actualización inminente constituye un cambio radical para ellos. La aplicación de este cambio de permisos tendrá lugar en **13 de abril de 2023**. Consulte la documentación sobre [migración de credenciales de API heredadas](#migrate-tech-accounts) para obtener instrucciones sobre la resolución de este problema.
>
>Las cuentas técnicas están disponibles para los clientes empresariales y se crean mediante la consola de desarrolladores de Adobe. La Adobe ID de un titular de cuenta técnica finaliza en `@techacct.adobe.com`. Si no está seguro de si es titular de una cuenta técnica, póngase en contacto con el administrador de su organización.

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

>[!NOTE]
>
>Todos los Privacy Service y [!UICONTROL Exclusión de la venta] los permisos son distintos y están separados entre sí sin superposición funcional. Esto es posible, ya que la API de Privacy Service se considera idempotente.

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de lectura de privacidad] | Determina si el usuario puede ver solicitudes de acceso y eliminación existentes, junto con sus detalles. |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de escritura de privacidad] | Determina si un usuario puede crear nuevas solicitudes de acceso y eliminación. |
| [!UICONTROL Permisos de Privacy Service] | [!UICONTROL Permiso de lectura (acceso) de la entrega de contenido] | Cuando el Privacy Service procesa una solicitud de acceso, se envía a ese cliente un archivo ZIP que contiene los datos del cliente. Al buscar los detalles de una solicitud de acceso, este permiso determina si el usuario puede acceder al vínculo de descarga del archivo ZIP de la solicitud. |
| [!UICONTROL Permisos de exclusión de venta] | [!UICONTROL Permiso de lectura: exclusión de la venta] | Determina si el usuario puede ver solicitudes de exclusión de venta existentes, junto con sus detalles. |
| [!UICONTROL Permisos de exclusión de venta] | [!UICONTROL Permiso de escritura - Exclusión de venta] | Determina si un usuario puede crear nuevas solicitudes de exclusión de la venta. |

{style="table-layout:auto"}

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

Para obtener más información sobre la administración de usuarios para un perfil de producto, consulte la [documentación del Admin Console](https://helpx.adobe.com/es/enterprise/using/manage-product-profiles.html).

### Migración de credenciales de API heredadas al perfil {#migrate-tech-accounts}

>[!NOTE]
>
>Esta sección solo se aplica a las credenciales de API existentes creadas antes de que los permisos de Privacy Service se integraran en Adobe Admin Console. Para nuevas credenciales, los perfiles de producto (y sus permisos) se asignan mediante [Proyectos de la consola de Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/projects/) en su lugar.<br><br>Consulte la sección sobre [asignación de perfiles de producto a un proyecto](./api/getting-started.md#product-profiles) en la guía de introducción a la API de Privacy Service para obtener más información.

Anteriormente, las cuentas técnicas no requerían un perfil de producto para la integración y los permisos. Sin embargo, debido a las recientes mejoras en los permisos de Privacy Service, ahora es necesario migrar las credenciales de API heredadas al perfil del producto. Esta actualización permite conceder permisos granulares a los titulares de cuentas técnicas. Siga los pasos que se proporcionan a continuación para actualizar los permisos de cuenta técnica para el Privacy Service.

#### Actualizar permisos de cuenta técnica {#update-tech-account-permissions}

El primer paso para asignar un conjunto de permisos para la cuenta técnica es ir al [Adobe Admin Console](https://adminconsole.adobe.com/) y cree un nuevo perfil de producto para Privacy Service.

En la interfaz de usuario del Admin Console, seleccione **Productos** desde la barra de navegación, seguida de **[!UICONTROL Experience Cloud]** y **[!UICONTROL Adobe Experience Platform Privacy Service]** en la barra lateral izquierda. La variable [!UICONTROL Perfiles de producto] se abre. Select **Nuevo perfil** para crear un nuevo perfil de producto para Privacy Service.

![La pestaña Perfiles de producto del Privacy Service del Experience Platform en Adobe Admin Console con el perfil nuevo resaltado.](./images/permissions/create-product-profile.png)

La variable [!UICONTROL Crear un nuevo perfil de producto] se abre. Puede encontrar instrucciones completas sobre cómo crear un perfil de producto en la [Guía de la interfaz de usuario para crear perfiles](../access-control/ui/create-profile.md).

Una vez guardado el nuevo perfil de producto, vaya a la [Consola de Adobe Developer](https://developer.adobe.com/console/home) e inicie sesión en ese producto o proyecto. Select **[!UICONTROL Proyectos]** desde la barra de navegación superior, seguida de la tarjeta de su proyecto.

>[!NOTE]
>
>Es posible que tenga que borrar la caché o esperar algún tiempo para que el nuevo proyecto aparezca en la lista de proyectos de Developer Console.

Una vez que haya iniciado sesión en el proyecto, seleccione la **[!UICONTROL API de Privacy Service]** integración desde la barra lateral izquierda.

![La pestaña Proyectos de la consola de Adobe Developer con la API de proyectos y Privacy Service resaltada.](./images/permissions/login-to-dev-console-project.png)

Aparece el panel de integración de la API del Privacy Service. Desde este tablero, puede editar el perfil de producto asociado a ese proyecto. Select **[!UICONTROL Editar perfiles de producto]** para iniciar el proceso. La variable [!UICONTROL Configuración de API] se abre.

![Panel de integración de la API del Privacy Service en la consola de Adobe Developer con Editar perfiles de producto resaltado](./images/permissions/edit-product-profiles.png)

La variable [!UICONTROL Configuración de API] muestra los perfiles de producto disponibles que existen actualmente en el servicio. Se correlacionan con los perfiles de producto creados en Admin Console. En la lista de perfiles de producto disponibles, active la casilla del nuevo perfil de producto que creó para la cuenta técnica en admin console. Esto asocia automáticamente esta cuenta técnica con los permisos del perfil de producto seleccionado. Select **[!UICONTROL Guardar la API configurada]** para confirmar la configuración.

>[!NOTE]
>
>Si una cuenta técnica ya está asociada con un perfil de producto, ya se seleccionará una de las casillas de verificación de la lista de perfiles de producto disponibles.

![El cuadro de diálogo Configurar API en la consola de Adobe Developer con un perfil de producto y la casilla Guardar API configurada están resaltadas.](./images/permissions/select-profile-for-tech-account.png)

#### Confirmar que se ha aplicado la configuración {#confirm-applied-settings}

Para confirmar que la configuración se ha aplicado a la cuenta. Vuelva a la [Admin Console](https://adminconsole.adobe.com/) y vaya al perfil de producto recién creado. Seleccione el **[!UICONTROL Credenciales de API]** para ver una lista de los proyectos asociados. El proyecto utilizado en Developer Console donde asignó el perfil de producto a la cuenta técnica se muestra en la lista de credenciales. El nombre de cada credencial de API está compuesto por el nombre del proyecto con un número generado aleatoriamente que se suprime hasta el final. Seleccione una credencial para abrir el [!UICONTROL Detalles] panel.

![Un perfil de producto en el Admin Console con la pestaña de credenciales de API y una fila de credenciales de proyecto resaltadas.](./images/permissions/confirm-credentials-in-admin-console.png)

La variable [!UICONTROL Detalles] contiene información sobre las credenciales de API, incluido el ID técnico asociado, la clave de API, la fecha de creación y de última modificación, así como los productos de Adobe asociados.

![Panel Detalles resaltados de una credencial de API en el Admin Console.](./images/permissions/admin-console-details-panel.png)

## Pasos siguientes

Esta guía abarcaba los permisos disponibles para Privacy Service y cómo administrarlos a través de Admin Console.

Para ver los pasos sobre cómo crear una nueva integración de API después de configurar perfiles de producto, consulte la [guía de introducción a la API de Privacy Service](./api/getting-started.md). Para obtener más información sobre la administración de permisos para otras funciones de Adobe Experience Platform, consulte la [documentación de control de acceso](../access-control/home.md).
