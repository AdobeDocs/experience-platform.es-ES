---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
title: Información general sobre el control de acceso
description: El control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 56f1cbc622450b154e6e29a8116789b316901f66
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 3%

---

# Información general sobre el control de acceso

Control de acceso para [!DNL Experience Platform] se proporciona a través de [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto en [!DNL Admin Console], que vinculan a los usuarios con permisos y zonas protegidas.

## Flujo de trabajo y jerarquía de control de acceso

Para configurar el control de acceso de [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga un [!DNL Experience Platform] integración del producto. La función mínima que concede o retira permisos es un administrador de perfil de producto. Otros roles de administrador que pueden administrar permisos son administradores de productos (pueden administrar todos los perfiles de un producto) y administradores de sistemas (sin restricciones). Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este punto, cualquier mención de &quot;administrador&quot; en este documento hace referencia a un administrador de perfil de producto o superior (como se ha descrito anteriormente).

Un flujo de trabajo superior para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Tras obtener la licencia de Adobe Experience Platform, o de una aplicación o servicio de aplicación que utilice Experience Platform, se enviará un correo electrónico al administrador especificado durante la licencia.
- El administrador de inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** en la lista de productos de la página información general.
- El administrador puede ver el valor predeterminado [perfiles de producto](#product-profiles) o cree nuevos perfiles de producto de clientes según sea necesario.
- El administrador puede editar los permisos y usuarios de cualquier perfil de producto existente.
- Al crear o editar un perfil de producto, el administrador agrega usuarios al perfil mediante la variable **[!UICONTROL usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos de datos]&quot; o &quot;[!UICONTROL Administrar esquemas]&quot;) accediendo al **[!UICONTROL permissions]** pestaña. Del mismo modo, el administrador puede asignar acceso a los entornos limitados utilizando la misma pestaña de permisos.
- Cuando los usuarios inician sesión en [!DNL Experience Platform] interfaz de usuario, su acceso a [!DNL Platform] Las capacidades de están controladas por los permisos que se les han concedido desde el paso 2. Por ejemplo, si un usuario no tiene la variable &quot;[!UICONTROL Ver conjuntos de datos]&quot;, la variable **[!UICONTROL Conjuntos de datos]** pestaña en el menú lateral no será visible para ese usuario.

Para ver los pasos más detallados sobre cómo administrar el control de acceso en [!DNL Experience Platform], consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a [!DNL Experience Platform] Las API se validan para obtener permisos y devolverán errores si no se encuentran los permisos adecuados en el contexto del usuario actual. Dentro de la interfaz de usuario de, los elementos se ocultan o modifican según los permisos otorgados al usuario actual.

## Adobe Admin Console

Adobe Admin Console proporciona una ubicación central para administrar los derechos de productos de Adobe y el acceso para su organización. A través de la consola, puede conceder a grupos de usuarios permisos de acceso para varios [!DNL Platform] funcionalidades, como &quot;[!UICONTROL Administrar conjuntos de datos]&quot;, &quot;[!UICONTROL Ver conjuntos de datos]&quot;, o &quot;[!UICONTROL Administrar perfiles]&quot;.

### Perfiles de producto

En el [!DNL Admin Console], los permisos se asignan a los usuarios mediante el uso de perfiles de producto. Los perfiles de producto le permiten conceder permisos a uno o varios usuarios y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante perfiles de producto. Los usuarios pueden asignarse a uno o varios perfiles de producto que pertenezcan a su organización.

### Perfiles de producto predeterminados

[!DNL Experience Platform] viene con dos perfiles de producto predeterminados preconfigurados. En la tabla siguiente se describe lo que se proporciona en cada perfil predeterminado, incluida la zona protegida a la que otorgan acceso, así como los permisos que otorgan dentro del ámbito de esa zona protegida.

| Perfil del producto | Acceso a zona protegida | Permisos |
| --- | --- | --- |
| Acceso a todo de producción predeterminado | Producción | Todos los permisos aplicables a [!DNL Experience Platform], excepto para permisos de administración de zona protegida. |
| Administradores de zona protegida | N/A | Proporciona acceso solo a los permisos de administración de zonas protegidas. |

## Zonas protegidas y permisos

Las zonas protegidas que no son de producción son una forma de virtualización de datos que le permite aislar datos de otras zonas protegidas y que generalmente se utilizan para experimentos, pruebas o ensayos de desarrollo. Los permisos de un perfil de producto proporcionan a los usuarios del perfil acceso a [!DNL Platform] funciones dentro de los entornos de zona protegida a los que se les ha concedido acceso. Una licencia de Experience Platform predeterminada le concede cinco zonas protegidas (una de producción y cuatro que no son de producción). Puede agregar paquetes de diez zonas protegidas que no sean de producción hasta un máximo de 75 zonas protegidas en total. Póngase en contacto con el administrador de su organización de IMS o con el representante de ventas de su Adobe para obtener más información.

Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [información general sobre zonas protegidas](../sandboxes/home.md).

### Acceso a zonas protegidas

El acceso a las zonas protegidas se administra mediante perfiles de producto. Para ver los pasos detallados sobre cómo habilitar el acceso a una zona protegida para un perfil de producto, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Se puede otorgar acceso a los usuarios a una o más zonas protegidas dentro de un perfil de producto. Si se incluye un usuario en dos o más perfiles de producto, ese usuario tendrá acceso a todas las zonas protegidas incluidas en esos perfiles.

El permiso &quot;Administración de zonas protegidas&quot; permite a los usuarios administrar, ver o restablecer zonas protegidas.

### Permisos {#permissions}

La pestaña Permisos dentro de un perfil de producto muestra los entornos limitados y los permisos activos para ese perfil:

![permissions-overview](./images/permissions.png)

Permisos que se conceden mediante la variable [!DNL Admin Console] se ordenan por categoría, con algunos permisos que otorgan acceso a varias funcionalidades de bajo nivel.

En la tabla siguiente se describen los permisos disponibles para [!DNL Experience Platform] en el [!DNL Admin Console], con descripciones de lo específico [!DNL Platform] a las que conceden acceso. Para ver los pasos detallados sobre cómo agregar permisos a un perfil de producto, consulte la [guía del usuario de control de acceso](./ui/overview.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Ver historial de alertas] | Acceso de solo lectura para el historial de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acceso para leer, editar y eliminar alertas. |
| [!DNL Alerts] | [!UICONTROL Ver alertas] | Acceso de solo lectura para alertas. |
| [!DNL Alerts] | [!UICONTROL Administrar alertas] | Acceso para leer, crear, editar y eliminar el historial de alertas. |
| [!DNL Data Hygiene] | [!UICONTROL Ver higiene de datos] | Acceso de solo lectura para la higiene de los datos. |
| [!DNL Data Hygiene] | [!UICONTROL Administrar higiene de datos] | Acceso para leer, crear, editar y eliminar la higiene de los datos. |
| [!DNL Data Modeling] | [!UICONTROL Administrar esquemas] | Acceso para leer, crear, editar y eliminar esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Esquemas de vistas] | Acceso de solo lectura a esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Administrar relaciones] | Acceso para leer, crear, editar y eliminar relaciones de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Administrar metadatos de identidad] | Acceso para leer, crear, editar y eliminar metadatos de identidad para esquemas. |
| [!DNL Data Management] | [!UICONTROL Administrar conjuntos de datos] | Acceso para leer, crear, editar y eliminar conjuntos de datos. Acceso de solo lectura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Ver conjuntos de datos] | Acceso de solo lectura para conjuntos de datos y esquemas. |
| [!DNL Data Management] | [!UICONTROL Monitorización de datos] | Acceso de solo lectura a la monitorización de conjuntos de datos y flujos. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfiles] | Acceso para leer, crear, editar y eliminar conjuntos de datos que se utilizan para perfiles de clientes. Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Ver perfiles] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar segmentos] | Acceso para leer, crear, editar y eliminar segmentos. |
| [!DNL Profile Management] | [!UICONTROL Ver segmentos] | Acceso de solo lectura a segmentos disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar políticas de combinación] | Acceso para leer, crear, editar y eliminar políticas de combinación. |
| [!DNL Profile Management] | [!UICONTROL Ver directivas de combinación] | Acceso de solo lectura a las políticas de combinación disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportar audiencia para segmento] | Capacidad para exportar un segmento de audiencia evaluado a un conjunto de datos. |
| [!DNL Profile Management] | [!UICONTROL Evaluación de un segmento para una audiencia] | Capacidad para generar perfiles para una audiencia evaluando una definición de segmento. |
| [!DNL Identity Management] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver espacios de nombres de identidad] | Acceso de solo lectura para áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver gráfico de identidad] | Acceso de solo lectura para gráficos de identidad. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar zonas protegidas] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Entornos aislados de vistas] | Acceso de solo lectura para zonas protegidas que pertenecen a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer una zona protegida] | Capacidad para restablecer una zona protegida. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear, editar y deshabilitar destinos. |
| [!DNL Destinations] | [!UICONTROL Ver destinos] | Acceso de solo lectura a destinos disponibles en **[!UICONTROL Catálogo]** y destinos autenticados en la pestaña **[!UICONTROL Examinar]** pestaña. |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Capacidad para activar datos en destinos activos que se han creado. Este permiso requiere: [!UICONTROL Ver destinos] o [!UICONTROL Administrar destinos] se concederá al usuario que activará los destinos. |
| [!DNL Destinations] | [!UICONTROL Administrar y activar destinos de conjuntos de datos] | Capacidad para leer, crear, editar y deshabilitar flujos de exportación de conjuntos de datos. Capacidad para activar también datos en conjuntos de datos activos que se han creado. |
| [!DNL Destinations] | [!UICONTROL Creación de destino] | Capacidad para crear destinos mediante [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Administrar fuentes] | Acceso para leer, crear, editar y deshabilitar orígenes. |
| [!DNL Data Ingestion] | [!UICONTROL Ver orígenes] | Acceso de solo lectura a fuentes disponibles en el **[!UICONTROL Catálogo]** pestaña y fuentes autenticadas en la **[!UICONTROL Examinar]** pestaña. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acceso para crear, aceptar y rechazar protocolos de enlace de socios para conectar dos organizaciones de IMS y habilitar [!DNL Segment Match] flujos. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Acceso para leer, crear, editar y publicar [!DNL Segment Match] se alimenta con socios activos. |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar Data Science Workspace] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| Control de datos | [!UICONTROL Aplicar etiquetas de uso de datos] | Acceso para leer, crear y eliminar etiquetas de uso. |
| Control de datos | [!UICONTROL Administrar políticas de uso de datos] | Acceso para leer, crear, editar y eliminar políticas de uso de datos. |
| Control de datos | [!UICONTROL Ver directivas de uso de datos] | Acceso de solo lectura para directivas de uso de datos pertenecientes a su organización. |
| Control de datos | [!UICONTROL Ver registro de actividades de usuario] | Acceso de solo lectura a la vista grabada [registros de auditoría](../landing/governance-privacy-security/audit-logs/overview.md) de actividades de Platform. |
| [!DNL Dashboards] | [!UICONTROL Ver tablero de uso de licencias] | Acceso de solo lectura para ver el panel de uso de licencias. |
| [!DNL Dashboards] | [!UICONTROL Administrar paneles estándar] | Agregue atributos personalizados que aún no estén en el almacén de datos. |
| [!DNL Query Service] | [!UICONTROL Administrar consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de Platform. |
| [!DNL Query Service] | [!UICONTROL Administración de integración de Query Service] | Acceso para crear, actualizar y eliminar credenciales que no caducan para el acceso al servicio de consultas. |

## Pasos siguientes

Al leer esta guía, se le han introducido los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar con el [guía del usuario de control de acceso](./ui/overview.md) para ver los pasos detallados sobre cómo usar la variable [!DNL Admin Console] para crear perfiles de producto y asignar permisos para [!DNL Platform].
