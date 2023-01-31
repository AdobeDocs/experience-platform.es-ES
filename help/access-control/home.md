---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
title: Información general sobre el control de acceso
description: El control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles de producto del Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 56f1cbc622450b154e6e29a8116789b316901f66
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 3%

---

# Información general sobre el control de acceso

Control de acceso para [!DNL Experience Platform] se proporciona a través de la variable [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto de [!DNL Admin Console], que vinculan a los usuarios con permisos y entornos limitados.

## Jerarquía y flujo de trabajo del control de acceso

Para configurar el control de acceso para [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga una [!DNL Experience Platform] integración de productos. La función mínima que concede o retira permisos es un administrador de perfiles de producto. Otras funciones de administrador que pueden administrar permisos son los administradores de productos (pueden administrar todos los perfiles de un producto) y los administradores de sistemas (sin restricciones). Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este punto, cualquier mención de &quot;administrador&quot; en este documento se refiere a un administrador de perfiles de producto o a una versión posterior (como se describe más arriba).

Un flujo de trabajo de alto nivel para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Después de conceder licencias a Adobe Experience Platform o a un servicio de aplicación/aplicación que utilice un Experience Platform, se envía un correo electrónico al administrador especificado durante la licencia.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** de la lista de productos de la página de información general.
- El administrador puede ver el valor predeterminado [perfiles de producto](#product-profiles) o cree nuevos perfiles de producto de cliente según sea necesario.
- El administrador puede editar los permisos y usuarios de cualquier perfil de producto existente.
- Al crear o editar un perfil de producto, el administrador agrega usuarios al perfil mediante la variable **[!UICONTROL usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos de datos]&quot; o &quot;[!UICONTROL Administrar esquemas]&quot;) accediendo al **[!UICONTROL permissions]** pestaña . Del mismo modo, el administrador puede asignar acceso a entornos limitados utilizando la misma pestaña de permisos.
- Cuando los usuarios inician sesión en la [!DNL Experience Platform] interfaz de usuario, su acceso a [!DNL Platform] está impulsada por los permisos que se les han concedido desde el paso 2. Por ejemplo, si un usuario no tiene el &quot;[!UICONTROL Ver conjuntos de datos]&quot;, el **[!UICONTROL Conjuntos de datos]** en el menú lateral no será visible para ese usuario.

Para obtener más información sobre cómo administrar el control de acceso en [!DNL Experience Platform], consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a [!DNL Experience Platform] Las API se validan para permisos y devolverán errores si no se encuentran los permisos adecuados en el contexto de usuario actual. Dentro de la interfaz de usuario, los elementos se ocultarán o alterarán según los permisos otorgados al usuario actual.

## Adobe Admin Console

Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso para su organización. A través de la consola, puede conceder a grupos de usuarios permisos de acceso para varios [!DNL Platform] , como &quot;[!UICONTROL Administrar conjuntos de datos]&quot;, &quot;[!UICONTROL Ver conjuntos de datos]&quot;, o &quot;[!UICONTROL Administrar perfiles]&quot;.

### Perfiles de producto

En el [!DNL Admin Console], los permisos se asignan a los usuarios mediante el uso de perfiles de producto. Los perfiles de producto le permiten conceder permisos a uno o varios usuarios y también contienen su acceso al ámbito de los entornos limitados que se les asignan a través de perfiles de producto. Los usuarios se pueden asignar a uno o varios perfiles de producto pertenecientes a su organización.

### Perfiles de producto predeterminados

[!DNL Experience Platform] viene con dos perfiles de producto predeterminados preconfigurados. La siguiente tabla describe lo que se proporciona en cada perfil predeterminado, incluido el simulador de pruebas al que conceden acceso, así como los permisos que conceden dentro del ámbito de dicho simulador de pruebas.

| Perfil del producto | Acceso a Simulador para pruebas | Permisos |
| --- | --- | --- |
| Acceso predeterminado a todo en producción | Producción | Todos los permisos aplicables a [!DNL Experience Platform], excepto para permisos de administración de espacio aislado. |
| Administradores de Simulador para pruebas | N/A | Proporciona acceso solo a permisos de administración de espacio aislado. |

## Sandboxes y permisos

Los entornos limitados que no son de producción son una forma de virtualización de datos que le permite aislar los datos de otros entornos limitados y que normalmente se utilizan para experimentos de desarrollo, pruebas o pruebas. Los permisos de un perfil de producto proporcionan a los usuarios del perfil acceso a [!DNL Platform] funciones dentro de los entornos de entorno limitado a los que se les ha concedido acceso. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados que no sean de producción hasta un máximo de 75 entornos limitados en total. Póngase en contacto con su administrador de organización de IMS o con su representante de ventas de Adobe para obtener más información.

Para obtener más información sobre los entornos limitados en [!DNL Experience Platform], consulte la [información general sobre los entornos limitados](../sandboxes/home.md).

### Acceso a entornos limitados

El acceso a los entornos limitados se administra mediante perfiles de producto. Para ver los pasos detallados sobre cómo habilitar el acceso a un simulador para un perfil de producto, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Se puede conceder acceso a los usuarios a uno o más entornos limitados de un perfil de producto. Si se incluye un usuario en dos o más perfiles de producto, ese usuario tendrá acceso a todos los entornos limitados incluidos en esos perfiles.

El permiso &quot;Administración de entornos limitados&quot; permite a los usuarios administrar, ver o restablecer entornos limitados.

### Permisos {#permissions}

La ficha Permisos de un perfil de producto muestra los entornos limitados y los permisos activos para ese perfil:

![permissions-overview](./images/permissions.png)

Permisos que se conceden mediante la variable [!DNL Admin Console] se ordenan por categoría, con algunos permisos que otorgan acceso a varias funcionalidades de bajo nivel.

La siguiente tabla describe los permisos disponibles para [!DNL Experience Platform] en el [!DNL Admin Console], con descripciones de las [!DNL Platform] a las que conceden acceso. Para ver los pasos detallados sobre cómo agregar permisos a un perfil de producto, consulte la [guía del usuario de control de acceso](./ui/overview.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Ver historial de alertas] | Acceso de solo lectura para el historial de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acceso para leer, editar y eliminar alertas. |
| [!DNL Alerts] | [!UICONTROL Ver alertas] | Acceso de solo lectura para alertas. |
| [!DNL Alerts] | [!UICONTROL Administrar alertas] | Acceso para leer, crear, editar y eliminar el historial de alertas. |
| [!DNL Data Hygiene] | [!UICONTROL Ver higiene de datos] | Acceso de solo lectura para la higiene de los datos. |
| [!DNL Data Hygiene] | [!UICONTROL Administrar la higiene de los datos] | Acceso para leer, crear, editar y eliminar la higiene de los datos. |
| [!DNL Data Modeling] | [!UICONTROL Administrar esquemas] | Acceso para leer, crear, editar y eliminar esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Esquemas de vistas] | Acceso de solo lectura a esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Administrar relaciones] | Acceso para leer, crear, editar y eliminar relaciones de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Administrar metadatos de identidad] | Acceso para leer, crear, editar y eliminar metadatos de identidad para esquemas. |
| [!DNL Data Management] | [!UICONTROL Administrar conjuntos de datos] | Acceso para leer, crear, editar y eliminar conjuntos de datos. Acceso de solo lectura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Ver conjuntos de datos] | Acceso de solo lectura para conjuntos de datos y esquemas. |
| [!DNL Data Management] | [!UICONTROL Supervisión de datos] | Acceso de solo lectura a conjuntos de datos y flujos de monitoreo. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfiles] | Acceso para leer, crear, editar y eliminar conjuntos de datos que se utilizan para perfiles de clientes. Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Ver perfiles] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar segmentos] | Acceso para leer, crear, editar y eliminar segmentos. |
| [!DNL Profile Management] | [!UICONTROL Ver segmentos] | Acceso de solo lectura a segmentos disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar directivas de combinación] | Acceso para leer, crear, editar y eliminar directivas de combinación. |
| [!DNL Profile Management] | [!UICONTROL Ver directivas de combinación] | Acceso de solo lectura a las directivas de combinación disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportar audiencia para segmentos] | Capacidad para exportar un segmento de audiencia evaluado a un conjunto de datos. |
| [!DNL Profile Management] | [!UICONTROL Evaluar un segmento en una audiencia] | Capacidad para generar perfiles para una audiencia mediante la evaluación de una definición de segmento. |
| [!DNL Identity Management] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver espacios de nombres de identidad] | Acceso de solo lectura para áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver gráfico de identidad] | Acceso de solo lectura para gráficos de identidad. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar entornos limitados] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Entornos aislados de vistas] | Acceso de solo lectura para entornos limitados pertenecientes a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer un Simulador para pruebas] | Posibilidad de restablecer un simulador para pruebas. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear, editar y deshabilitar destinos. |
| [!DNL Destinations] | [!UICONTROL Ver destinos] | Acceso de solo lectura a destinos disponibles en la variable **[!UICONTROL Catálogo]** y destinos autenticados en la **[!UICONTROL Examinar]** pestaña . |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Capacidad para activar datos en destinos activos que se hayan creado. Este permiso requiere: [!UICONTROL Ver destinos] o [!UICONTROL Administrar destinos] se concede al usuario que activará los destinos. |
| [!DNL Destinations] | [!UICONTROL Administrar y activar destinos de conjuntos de datos] | Capacidad para leer, crear, editar y deshabilitar flujos de exportación de conjuntos de datos. Capacidad para activar también datos en conjuntos de datos activos que se han creado. |
| [!DNL Destinations] | [!UICONTROL Creación de destinos] | Capacidad para crear destinos mediante [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Administrar fuentes] | Acceso para leer, crear, editar y deshabilitar orígenes. |
| [!DNL Data Ingestion] | [!UICONTROL Ver fuentes] | Acceso de solo lectura a los orígenes disponibles en la **[!UICONTROL Catálogo]** y fuentes autenticadas en la **[!UICONTROL Examinar]** pestaña . |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acceso para crear, aceptar y rechazar apretadores de manos de socios para conectar dos organizaciones IMS y habilitar [!DNL Segment Match] flujos. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Acceso para leer, crear, editar y publicar [!DNL Segment Match] fuentes con socios activos. |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar Data Science Workspace] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| Control de datos | [!UICONTROL Aplicar etiquetas de uso de datos] | Acceso para leer, crear y eliminar etiquetas de uso. |
| Control de datos | [!UICONTROL Administrar políticas de uso de datos] | Acceso para leer, crear, editar y eliminar políticas de uso de datos. |
| Control de datos | [!UICONTROL Ver directivas de uso de datos] | Acceso de solo lectura para directivas de uso de datos pertenecientes a su organización. |
| Control de datos | [!UICONTROL Ver registro de actividades del usuario] | Acceso de solo lectura para ver grabado [registros de auditoría](../landing/governance-privacy-security/audit-logs/overview.md) de las actividades de la plataforma. |
| [!DNL Dashboards] | [!UICONTROL Ver panel de uso de licencias] | Acceso de solo lectura para ver el panel de uso de licencias. |
| [!DNL Dashboards] | [!UICONTROL Administrar tableros estándar] | Agregue atributos personalizados que aún no estén en el almacén de datos. |
| [!DNL Query Service] | [!UICONTROL Administrar consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de Platform. |
| [!DNL Query Service] | [!UICONTROL Administrar integración del servicio de consultas] | Acceso para crear, actualizar y eliminar credenciales no caducadas para el acceso al servicio de consulta. |

## Pasos siguientes

Al leer esta guía, se le han introducido los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar con el [guía del usuario de control de acceso](./ui/overview.md) para ver los pasos detallados sobre cómo usar la variable [!DNL Admin Console] para crear perfiles de producto y asignar permisos para [!DNL Platform].
