---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
title: Información general sobre el control de acceso
description: El control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 866e84e5f7fe5df7444c83756a893964dcd3ed3d
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 4%

---

# Información general sobre el control de acceso

El control de acceso para Adobe Experience Platform se proporciona a través de la variable **[!UICONTROL Permisos]** in [Adobe Experience Cloud](https://experience.adobe.com/). Esta funcionalidad aprovecha las funciones y directivas que vinculan a los usuarios con permisos y zonas protegidas.

## Flujo de trabajo y jerarquía de control de acceso

Para configurar el control de acceso de Experience Platform, debe tener privilegios de administrador de sistemas o productos para una organización que tenga un producto de Experience Platform. La función mínima que puede conceder o retirar permisos es de administrador de productos. Otros roles de administrador que pueden administrar permisos son administradores del sistema (sin restricciones). Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este punto, cualquier mención de &quot;administrador&quot; en este documento hace referencia a un administrador de productos o superior (como se ha descrito anteriormente).

Un flujo de trabajo superior para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Tras obtener la licencia de Adobe Experience Platform, o de una aplicación o servicio de aplicación que utilice Experience Platform, se enviará un correo electrónico al administrador especificado durante la licencia.
- El administrador de inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** en la lista de productos de la página información general.
- Para conceder acceso al Experience Platform, este deberá añadir usuarios al perfil de producto predeterminado: `AEP-Default-All-Users`.
- En Permisos de Experience Platform, el administrador puede crear nuevas funciones o editar los permisos y usuarios para cualquier función existente.
- Al crear o editar una función, el administrador añade usuarios a la función con el **[!UICONTROL usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos de datos]&quot; o &quot;[!UICONTROL Administrar esquemas]&quot;) al editar los permisos de la función. Del mismo modo, el administrador puede asignar acceso a los entornos limitados utilizando la misma opción de edición.
- Cuando los usuarios inician sesión en la interfaz de usuario de Experience Platform, su acceso a las funciones de Experience Platform depende de los permisos que se les han concedido desde el paso anterior. Por ejemplo, si un usuario no tiene la variable [!UICONTROL Ver conjuntos de datos] permiso, el **[!UICONTROL Conjuntos de datos]** pestaña en el menú lateral no será visible para ese usuario.

Para ver los pasos más detallados sobre cómo administrar el control de acceso en Experience Platform, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a las API de Experience Platform se validan para obtener permisos y devolverán errores si no se encuentran los permisos adecuados en el contexto de usuario actual. Dentro de la interfaz de usuario de, los elementos se ocultan o modifican según los permisos otorgados al usuario actual.

## Permisos {#platform-permissions}

[!UICONTROL Permisos] proporciona una ubicación central para administrar el acceso de Experience Platform para su organización. Pasante [!UICONTROL Permisos], puede conceder a grupos de usuarios permisos de acceso para diversas funciones de Experience Platform, como [!UICONTROL Administrar conjuntos de datos], [!UICONTROL Ver conjuntos de datos], o [!UICONTROL Administrar perfiles].

### Funciones

En el [!UICONTROL Funciones] , los permisos se asignan a los usuarios mediante el uso de funciones. Las funciones permiten conceder permisos a uno o varios usuarios y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante funciones. Los usuarios pueden tener asignada una o varias funciones que pertenezcan a su organización.

### Funciones predeterminadas

Experience Platform viene con dos funciones predeterminadas preconfiguradas. En la tabla siguiente se describe lo que se proporciona en cada perfil predeterminado, incluida la zona protegida a la que otorgan acceso, así como los permisos que otorgan dentro del ámbito de esa zona protegida.

| Función | Acceso a zona protegida | Permisos |
| --- | --- | --- |
| Acceso a todo de producción predeterminado | Producción | Todos los permisos aplicables a Experience Platform, excepto los permisos de administración de zonas protegidas. |
| Administradores de zona protegida | N/A | Proporciona acceso solo a los permisos de administración de zonas protegidas. |

## Zonas protegidas y permisos

Las zonas protegidas que no son de producción son una forma de virtualización de datos que le permite aislar datos de otras zonas protegidas y que generalmente se utilizan para experimentos, pruebas o ensayos de desarrollo. Los permisos de una función otorgan a los usuarios de la función acceso a las funciones de Experience Platform dentro de los entornos de zona protegida a los que se les ha concedido acceso. Una licencia de Experience Platform predeterminada le concede cinco zonas protegidas (una de producción y cuatro que no son de producción). Puede agregar paquetes de diez zonas protegidas que no sean de producción hasta un máximo de 75 zonas protegidas en total. Póngase en contacto con el administrador de su organización o con el representante de ventas de Adobe para obtener más información.

Para obtener más información sobre los entornos limitados de Experience Platform, consulte la [información general sobre zonas protegidas](../sandboxes/home.md).

### Acceso a zonas protegidas

El acceso a las zonas protegidas se administra mediante funciones. Para ver los pasos detallados sobre cómo habilitar el acceso a una zona protegida para una función, consulte la [guía de funciones de control de acceso basado en atributos](./abac/ui/roles.md).

Se puede otorgar acceso a los usuarios a una o más zonas protegidas dentro de una función. Si un usuario está incluido en dos o más funciones, ese usuario tendrá acceso a todas las zonas protegidas incluidas en esas funciones.

El permiso &quot;Administración de zonas protegidas&quot; permite a los usuarios administrar, ver o restablecer zonas protegidas.

### Permisos de recursos {#permissions}

El recurso [!UICONTROL Permisos] dentro de una función muestra los entornos limitados y los permisos activos para esa función:

![permissions-overview](./images/permissions.png)

Los permisos que se conceden mediante los permisos de recurso se ordenan por categoría, con algunos permisos que conceden acceso a varias funcionalidades de bajo nivel.

En la tabla siguiente se describen los permisos disponibles para los Experience Platform en la función, con descripciones de las funciones de Experience Platform específicas a las que otorgan acceso. Para ver los pasos detallados sobre cómo agregar permisos a una función, consulte la [guía de funciones de control de acceso basado en atributos](./abac/ui/roles.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Ver historial de alertas] | Acceso de solo lectura para el historial de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acceso para leer, editar y eliminar alertas. |
| [!DNL Alerts] | [!UICONTROL Ver alertas] | Acceso de solo lectura para alertas. |
| [!DNL Alerts] | [!UICONTROL Administrar alertas] | Acceso para leer, crear, editar y eliminar el historial de alertas. |
| [!DNL Computed Attributes] | [!UICONTROL Ver atributos calculados] | Acceso de solo lectura para la pestaña de atributos calculados, inventario y detalles. |
| [!DNL Computed Attributes] | [!UICONTROL Administrar atributos calculados] | Acceso para leer, crear, eliminar borradores y desactivar atributos calculados. |
| [!DNL Data Lifecycle] | [!UICONTROL Ver ciclo vital de datos] | Acceso de solo lectura para el ciclo vital de datos. |
| [!DNL Data Lifecycle] | [!UICONTROL Administrar ciclo de vida de datos] | Acceso para leer, crear, editar y eliminar datos durante el ciclo vital. |
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
| [!DNL Profile Management] | [!UICONTROL Ver IA B2B] | Acceso de solo lectura a los ajustes y configuraciones de todos los servicios AI/ML de B2B. |
| [!DNL Profile Management] | [!UICONTROL Administración de IA B2B] | Acceso para leer, crear, editar y eliminar ajustes y configuraciones para todos los servicios AI/ML de B2B. |
| [!DNL Profile Management] | [!UICONTROL Ver perfil B2B] | Acceso de solo lectura a perfiles de entidad B2B (como Cuenta, Oportunidad, etc.), ajustes y configuraciones para todos los servicios AI/ML B2B y widgets de tablero B2B. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfil B2B] | Acceso para leer, crear, editar y eliminar perfiles de entidad B2B (como Cuenta, Oportunidad, etc.). Acceso de solo lectura para ajustes y configuraciones de todos los servicios AI/ML de B2B y widgets de tablero B2B. |
| [!DNL Identity Management] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver espacios de nombres de identidad] | Acceso de solo lectura para áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver gráfico de identidad] | Acceso de solo lectura para gráficos de identidad. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar zonas protegidas] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Entornos aislados de vistas] | Acceso de solo lectura para zonas protegidas que pertenecen a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer una zona protegida] | Capacidad para restablecer una zona protegida. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear y eliminar flujos de activación de destino y cuentas de destino. |
| [!DNL Destinations] | [!UICONTROL Ver destinos] | Acceso de solo lectura a destinos disponibles en **[!UICONTROL Catálogo]** y destinos autenticados en la pestaña **[!UICONTROL Examinar]** pestaña. |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Permite a los usuarios activar segmentos en destinos existentes. Habilita el paso de asignación en el flujo de trabajo de activación. Este permiso requiere: [!UICONTROL Ver destinos] o [!UICONTROL Administrar destinos] se concederá al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Activar segmento sin asignación] | Permite a los usuarios activar segmentos en destinos existentes, sin mostrar el [paso de asignación](../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden añadir y quitar segmentos en flujos de trabajo de activación, pero no pueden agregar ni quitar atributos o identidades asignados. Este permiso requiere lo siguiente [!UICONTROL Activar destinos] permiso que se concederá al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Administrar y activar destinos de conjuntos de datos] | Capacidad para leer, crear, editar y deshabilitar flujos de exportación de conjuntos de datos. Capacidad para activar también datos en conjuntos de datos activos que se han creado. |
| [!DNL Destinations] | [!UICONTROL Creación de destino] | Capacidad para crear destinos mediante [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Administrar fuentes] | Acceso para leer, crear, editar y deshabilitar orígenes. |
| [!DNL Data Ingestion] | [!UICONTROL Ver orígenes] | Acceso de solo lectura a fuentes disponibles en el **[!UICONTROL Catálogo]** pestaña y fuentes autenticadas en la **[!UICONTROL Examinar]** pestaña. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acceso para crear, aceptar y rechazar protocolos de enlace de socios para conectar dos organizaciones y habilitar [!DNL Segment Match] flujos. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Acceso para leer, crear, editar y publicar [!DNL Segment Match] se alimenta con socios activos. |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar Data Science Workspace] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| Control de datos | [!UICONTROL Administrar etiquetas de uso] | Acceso para leer, crear y eliminar etiquetas de uso. |
| Control de datos | [!UICONTROL Administrar políticas de uso de datos] | Acceso para leer, crear, editar y eliminar políticas de uso de datos. |
| Control de datos | [!UICONTROL Ver directivas de uso de datos] | Acceso de solo lectura para directivas de uso de datos pertenecientes a su organización. |
| Control de datos | [!UICONTROL Ver registro de actividades de usuario] | Acceso de solo lectura a la vista grabada [registros de auditoría](../landing/governance-privacy-security/audit-logs/overview.md) de actividades de Platform. |
| [!DNL Dashboards] | [!UICONTROL Ver tablero de uso de licencias] | Acceso de solo lectura para ver el panel de uso de licencias. |
| [!DNL Dashboards] | [!UICONTROL Administrar paneles estándar] | Agregue atributos personalizados que aún no estén en el almacén de datos. |
| [!DNL Query Service] | [!UICONTROL Administrar consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de Platform. |
| [!DNL Query Service] | [!UICONTROL Administración de integración de Query Service] | Acceso para crear, actualizar y eliminar credenciales que no caducan para el acceso al servicio de consultas. |

## Pasos siguientes

Al leer esta guía, se le han presentado los principios principales del control de acceso en Experience Platform. Ahora puede continuar con el [guía del usuario de control de acceso basado en atributos](./abac/overview.md) para ver los pasos detallados sobre cómo usar Experience Cloud para crear funciones y asignar permisos de Experience Platform.
