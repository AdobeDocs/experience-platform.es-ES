---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: Información general sobre el control de acceso
description: El control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles de producto del Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---

# Información general sobre el control de acceso

El control de acceso para [!DNL Experience Platform] se proporciona a través de [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto de [!DNL Admin Console], que vinculan a los usuarios con permisos y entornos limitados.

## Jerarquía y flujo de trabajo del control de acceso

Para configurar el control de acceso para [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga una integración de producto [!DNL Experience Platform]. La función mínima que concede o retira permisos es un administrador de perfiles de producto. Otras funciones de administrador que pueden administrar permisos son los administradores de productos (pueden administrar todos los perfiles de un producto) y los administradores de sistemas (sin restricciones). Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este punto, cualquier mención de &quot;administrador&quot; en este documento se refiere a un administrador de perfiles de producto o a una versión posterior (como se describe más arriba).

Un flujo de trabajo de alto nivel para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Después de conceder licencias a Adobe Experience Platform o a un servicio de aplicación/aplicación que utilice un Experience Platform, se envía un correo electrónico al administrador especificado durante la licencia.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** en la lista de productos de la página de información general.
- El administrador puede ver los [perfiles de producto](#product-profiles) predeterminados o crear nuevos perfiles de producto de cliente según sea necesario.
- El administrador puede editar los permisos y usuarios de cualquier perfil de producto existente.
- Al crear o editar un perfil de producto, el administrador agrega usuarios al perfil mediante la pestaña **[!UICONTROL users]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Read Datasets]&quot; o &quot;[!UICONTROL Manage Schemas]&quot;) accediendo a la pestaña **[!UICONTROL permissions]** . Del mismo modo, el administrador puede asignar acceso a entornos limitados utilizando la misma pestaña de permisos.
- Cuando los usuarios inician sesión en la interfaz de usuario [!DNL Experience Platform] , su acceso a las funcionalidades de [!DNL Platform] depende de los permisos que se les han concedido desde el paso 2. Por ejemplo, si un usuario no tiene el permiso &quot;[!UICONTROL View Datasets]&quot;, la pestaña **[!UICONTROL Datasets]** del menú lateral no será visible para ese usuario.

Para obtener más información sobre cómo administrar el control de acceso en [!DNL Experience Platform], consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a las API [!DNL Experience Platform] se validan para obtener permisos y devuelven errores si no se encuentran los permisos adecuados en el contexto de usuario actual. Dentro de la interfaz de usuario, los elementos se ocultarán o alterarán según los permisos otorgados al usuario actual.

## Adobe Admin Console

Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso para su organización. A través de la consola, puede conceder permisos de acceso a grupos de usuarios para varias funciones de [!DNL Platform], como &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;.

### Perfiles de producto

En [!DNL Admin Console], los permisos se asignan a los usuarios mediante el uso de perfiles de producto. Los perfiles de producto le permiten conceder permisos a uno o varios usuarios y también contienen su acceso al ámbito de los entornos limitados que se les asignan a través de perfiles de producto. Los usuarios se pueden asignar a uno o varios perfiles de producto pertenecientes a su organización.

### Perfiles de producto predeterminados

[!DNL Experience Platform] viene con dos perfiles de producto predeterminados preconfigurados. La siguiente tabla describe lo que se proporciona en cada perfil predeterminado, incluido el simulador de pruebas al que conceden acceso, así como los permisos que conceden dentro del ámbito de dicho simulador de pruebas.

| Perfil del producto | Acceso a Simulador para pruebas | Permisos |
| --- | --- | --- |
| Acceso predeterminado a todo en producción | Producción | Todos los permisos aplicables a [!DNL Experience Platform], excepto los permisos de administración de espacio aislado. |
| Administradores de Simulador para pruebas | N/D | Proporciona acceso solo a permisos de administración de espacio aislado. |

## Sandboxes y permisos

Los entornos limitados que no son de producción son una forma de virtualización de datos que le permite aislar los datos de otros entornos limitados y que normalmente se utilizan para experimentos de desarrollo, pruebas o pruebas. Los permisos de un perfil de producto proporcionan a los usuarios del perfil acceso a las funciones [!DNL Platform] dentro de los entornos de entorno limitado a los que se les ha otorgado acceso. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados que no sean de producción hasta un máximo de 75 entornos limitados en total. Póngase en contacto con su administrador de organización de IMS o con su representante de ventas de Adobe para obtener más información.

Para obtener más información sobre los entornos limitados en [!DNL Experience Platform], consulte la [información general de los entornos limitados](../sandboxes/home.md).

### Acceso a entornos limitados

El acceso a los entornos limitados se administra mediante perfiles de producto. Para ver los pasos detallados sobre cómo habilitar el acceso a un simulador para un perfil de producto, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Se puede conceder acceso a los usuarios a uno o más entornos limitados de un perfil de producto. Si se incluye un usuario en dos o más perfiles de producto, ese usuario tendrá acceso a todos los entornos limitados incluidos en esos perfiles.

El permiso &quot;Administración de entornos limitados&quot; permite a los usuarios administrar, ver o restablecer entornos limitados.

### Permisos

La ficha Permisos de un perfil de producto muestra los entornos limitados y los permisos activos para ese perfil:

![permissions-overview](./images/permissions-overview.png)

Los permisos otorgados a través de [!DNL Admin Console] se ordenan por categoría, con algunos permisos que otorgan acceso a varias funcionalidades de bajo nivel.

La siguiente tabla describe los permisos disponibles para [!DNL Experience Platform] en [!DNL Admin Console], con descripciones de las funcionalidades específicas de [!DNL Platform] a las que conceden acceso. Para ver los pasos detallados sobre cómo agregar permisos a un perfil de producto, consulte la [guía del usuario del control de acceso](./ui/overview.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Acceso para leer, crear, editar y eliminar esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Acceso de solo lectura a esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Acceso para leer, crear, editar y eliminar relaciones de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Acceso para leer, crear, editar y eliminar metadatos de identidad para esquemas. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Acceso para leer, crear, editar y eliminar conjuntos de datos. Acceso de solo lectura para esquemas. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Acceso de solo lectura para conjuntos de datos y esquemas. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Acceso de solo lectura a conjuntos de datos y flujos de monitoreo. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Acceso para leer, crear, editar y eliminar conjuntos de datos que se utilizan para perfiles de clientes. Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Acceso para leer, crear, editar y eliminar segmentos. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Acceso de solo lectura a segmentos disponibles. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Acceso para leer, crear, editar y eliminar directivas de combinación. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Acceso de solo lectura a las directivas de combinación disponibles. |
| [!DNL Profile Management] | [!UICONTROL Export Audience for Segment] | Capacidad para exportar un segmento de audiencia evaluado a un conjunto de datos. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Capacidad para generar perfiles para una audiencia mediante la evaluación de una definición de segmento. |
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces] | Acceso para leer, crear, editar y eliminar áreas de nombres de identidad. |
| [!DNL Identities] | [!UICONTROL View Identity Namespaces] | Acceso de solo lectura para áreas de nombres de identidad. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Acceso de solo lectura para entornos limitados pertenecientes a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Posibilidad de restablecer un simulador para pruebas. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Acceso para leer, crear, editar y deshabilitar destinos. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Acceso de solo lectura a destinos disponibles en la pestaña **[!UICONTROL Catalog]** y destinos autenticados en la pestaña **[!UICONTROL Browse]**. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Capacidad para activar datos en destinos activos que se hayan creado. Este permiso requiere que &quot;Ver destinos&quot; o &quot;Administrar [!UICONTROL Destinations”] se concedan al usuario que activará los destinos. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Acceso para leer, crear, editar y deshabilitar orígenes. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Acceso de solo lectura a los orígenes disponibles en la pestaña **[!UICONTROL Catalog]** y a los orígenes autenticados en la pestaña **[!UICONTROL Browse]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Acceso para leer, crear y eliminar etiquetas de uso. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Acceso para leer, crear, editar y eliminar políticas de uso de datos. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Acceso de solo lectura para directivas de uso de datos pertenecientes a su organización. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de Platform. |

## Pasos siguientes

Al leer esta guía, se le han introducido los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar en la [guía del usuario de control de acceso](./ui/overview.md) para conocer los pasos detallados sobre cómo utilizar [!DNL Admin Console] para crear perfiles de producto y asignar permisos para [!DNL Platform].
