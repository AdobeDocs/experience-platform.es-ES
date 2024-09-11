---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
title: Información general sobre el control de acceso
description: El control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 5d5c57dfb9e4abda6b1bca96147a95d063bc17c6
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# Información general sobre el control de acceso

El control de acceso para Adobe Experience Platform se proporciona mediante **[!UICONTROL Permisos]** en [Adobe Experience Cloud](https://experience.adobe.com/). Esta funcionalidad aprovecha las funciones y directivas que vinculan a los usuarios con permisos y zonas protegidas.

## Flujo de trabajo y jerarquía de control de acceso

Para configurar el control de acceso de Experience Platform, debe tener privilegios de administrador de sistemas o productos para una organización que tenga un producto de Experience Platform. La función mínima que puede conceder o retirar permisos es de administrador de productos. Otros roles de administrador que pueden administrar permisos son administradores del sistema (sin restricciones). Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este punto, cualquier mención de &quot;administrador&quot; en este documento hace referencia a un administrador de productos o superior (como se ha descrito anteriormente).

Un flujo de trabajo superior para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Tras obtener la licencia de Adobe Experience Platform, o de una aplicación o servicio de aplicación que utilice Experience Platform, se enviará un correo electrónico al administrador especificado durante la licencia.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** de la lista de productos en la página de información general.
- Para conceder acceso al Experience Platform, se recomienda que agregue usuarios al perfil de producto predeterminado: `AEP-Default-All-Users`.
- En Permisos de Experience Platform, el administrador puede crear nuevas funciones o editar los permisos y usuarios para cualquier función existente.
- Al crear o editar una función, el administrador agrega usuarios a la función mediante la ficha **[!UICONTROL usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos de datos]&quot; o &quot;[!UICONTROL Administrar esquemas]&quot;) mediante la edición de los permisos de la función. Del mismo modo, el administrador puede asignar acceso a los entornos limitados utilizando la misma opción de edición.
- Cuando los usuarios inician sesión en la interfaz de usuario de Experience Platform, su acceso a las funciones de Experience Platform depende de los permisos que se les han concedido desde el paso anterior. Por ejemplo, si un usuario no tiene el permiso [!UICONTROL Ver conjuntos de datos], la ficha **[!UICONTROL Conjuntos de datos]** del menú lateral no será visible para ese usuario.

Para ver pasos más detallados sobre cómo administrar el control de acceso en Experience Platform, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a las API de Experience Platform se validan para obtener permisos y devolverán errores si no se encuentran los permisos adecuados en el contexto de usuario actual. Dentro de la interfaz de usuario de, los elementos se ocultan o modifican según los permisos otorgados al usuario actual.

## Permisos {#platform-permissions}

[!UICONTROL Permisos] proporciona una ubicación central para administrar el acceso de Experience Platform para su organización. Mediante [!UICONTROL Permisos], puede conceder a grupos de usuarios permisos de acceso para diversas funciones de Experience Platform, como [!UICONTROL Administrar conjuntos de datos], [!UICONTROL Ver conjuntos de datos] o [!UICONTROL Administrar perfiles].

### Funciones

En la sección [!UICONTROL Roles], los permisos se asignan a los usuarios mediante el uso de funciones. Las funciones permiten conceder permisos a uno o varios usuarios y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante funciones. Los usuarios pueden tener asignada una o varias funciones que pertenezcan a su organización.

### Funciones predeterminadas

Experience Platform viene con dos funciones predeterminadas preconfiguradas. En la tabla siguiente se describe lo que se proporciona en cada perfil predeterminado, incluida la zona protegida a la que otorgan acceso, así como los permisos que otorgan dentro del ámbito de esa zona protegida.

| Función | Acceso a zona protegida | Permisos |
| --- | --- | --- |
| Acceso a todo de producción predeterminado | Producción | Todos los permisos aplicables a Experience Platform, excepto los permisos de administración de zonas protegidas. |
| Administradores de zona protegida | N/A | Proporciona acceso solo a los permisos de administración de zonas protegidas. |

## Zonas protegidas y permisos

Las zonas protegidas que no son de producción son una forma de virtualización de datos que le permite aislar datos de otras zonas protegidas y que generalmente se utilizan para experimentos, pruebas o ensayos de desarrollo. Los permisos de una función otorgan a los usuarios de la función acceso a las funciones de Experience Platform dentro de los entornos de zona protegida a los que se les ha concedido acceso. Una licencia de Experience Platform predeterminada le concede cinco zonas protegidas (una de producción y cuatro que no son de producción). Puede agregar paquetes de diez zonas protegidas que no sean de producción hasta un máximo de 75 zonas protegidas en total. Póngase en contacto con el administrador de su organización o con el representante de ventas de Adobe para obtener más información.

Para obtener más información sobre las zonas protegidas en Experience Platform, consulte la [descripción general de las zonas protegidas](../sandboxes/home.md).

### Acceso a zonas protegidas

El acceso a las zonas protegidas se administra mediante funciones. Para ver los pasos detallados sobre cómo habilitar el acceso a una zona protegida para un rol, consulte la [guía de roles de control de acceso basado en atributos](./abac/ui/roles.md).

Se puede otorgar acceso a los usuarios a una o más zonas protegidas dentro de una función. Si un usuario está incluido en dos o más funciones, ese usuario tendrá acceso a todas las zonas protegidas incluidas en esas funciones.

El permiso &quot;Administración de zonas protegidas&quot; permite a los usuarios administrar, ver o restablecer zonas protegidas.

### Permisos de recursos {#permissions}

La ficha del recurso [!UICONTROL Permisos] dentro de un rol muestra los entornos limitados y los permisos activos para ese rol:

![permisos-información general](./images/permissions.png)

Los permisos que se conceden mediante los permisos de recurso se ordenan por categoría, con algunos permisos que conceden acceso a varias funcionalidades de bajo nivel.

En la tabla siguiente se describen los permisos disponibles para los Experience Platform en la función, con descripciones de las funciones de Experience Platform específicas a las que otorgan acceso. Para ver los pasos detallados sobre cómo agregar permisos a un rol, consulte la [guía de roles de control de acceso basado en atributos](./abac/ui/roles.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL AI Assistant] | [!UICONTROL Habilitar el asistente de IA] | Posibilidad de hacer preguntas al [asistente de IA](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL Ver datos operativos] | Acceso para obtener respuestas a [consultas de perspectivas operacionales](../ai-assistant/home.md##operational-insights). |
| [!DNL Alerts] | [!UICONTROL Ver historial de alertas] | Acceso de solo lectura para el historial de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acceso para leer, editar y eliminar alertas. |
| [!DNL Alerts] | [!UICONTROL Ver alertas] | Acceso de solo lectura para alertas. |
| [!DNL Alerts] | [!UICONTROL Administrar alertas] | Acceso para leer, crear, editar y eliminar el historial de alertas. |
| [!DNL Computed Attributes] | [!UICONTROL Ver atributos calculados] | Acceso de solo lectura para la pestaña de atributos calculados, inventario y detalles. |
| [!DNL Computed Attributes] | [!UICONTROL Administrar atributos calculados] | Acceso para leer, crear, eliminar borradores y desactivar atributos calculados. |
| [!DNL Dashboards] | [!UICONTROL Ver tablero de uso de licencias] | Acceso de solo lectura para ver el panel de uso de licencias. |
| [!DNL Dashboards] | [!UICONTROL Administrar paneles estándar] | Agregue atributos personalizados que aún no estén en el almacén de datos. |
| [!DNL Data Governance] | [!UICONTROL Administrar etiquetas de uso] | Acceso para leer, crear y eliminar etiquetas de uso. |
| [!DNL Data Governance] | [!UICONTROL Administrar Políticas De Uso De Datos] | Acceso para leer, crear, editar y eliminar políticas de uso de datos. |
| [!DNL Data Governance] | [!UICONTROL Ver directivas de uso de datos] | Acceso de solo lectura para directivas de uso de datos pertenecientes a su organización. |
| [!DNL Data Governance] | [!UICONTROL Ver registro de actividad de usuario] | Acceso de solo lectura para ver [registros de auditoría](../landing/governance-privacy-security/audit-logs/overview.md) registrados de actividades de Platform. |
| [!DNL Data Ingestion] | [!UICONTROL Administrar orígenes] | Acceso para leer, crear, editar y deshabilitar orígenes. |
| [!DNL Data Ingestion] | [!UICONTROL Ver orígenes] | Acceso de solo lectura a orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y orígenes autenticados en la ficha **[!UICONTROL Examinar]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acceso para crear, aceptar y rechazar protocolos de enlace de socios para conectar dos organizaciones y habilitar [!DNL Segment Match] flujos. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Acceso para leer, crear, editar y publicar fuentes de [!DNL Segment Match] con socios activos. |
| [!DNL Data Lifecycle] | [!UICONTROL Ver ciclo de vida de datos] | Acceso de solo lectura para el ciclo vital de datos. |
| [!DNL Data Lifecycle] | [!UICONTROL Administrar ciclo de vida de datos] | Acceso para leer, crear, editar y eliminar datos durante el ciclo vital. |
| [!DNL Data Modeling] | [!UICONTROL Administrar esquemas] | Acceso para leer, crear, editar y eliminar esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Esquemas de vista] | Acceso de solo lectura a esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Administrar relaciones] | Acceso para leer, crear, editar y eliminar relaciones de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Administrar metadatos de identidad] | Acceso para leer, crear, editar y eliminar metadatos de identidad para esquemas. |
| [!DNL Data Management] | [!UICONTROL Administrar conjuntos de datos] | Acceso para leer, crear, editar y eliminar conjuntos de datos. Acceso de solo lectura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Ver conjuntos de datos] | Acceso de solo lectura para conjuntos de datos y esquemas. |
| [!DNL Data Management] | [!UICONTROL Supervisión de datos] | Acceso de solo lectura a la monitorización de conjuntos de datos y flujos. |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar Workspace de ciencia de datos] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| [!DNL Destinations] | [!UICONTROL Ver destinos] | Acceso de solo lectura para ver los destinos disponibles en la ficha **[!UICONTROL Catálogo]** y los destinos autenticados en la ficha **[!UICONTROL Examinar]**. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear y eliminar conexiones y cuentas de destino. |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Permite a los usuarios activar segmentos en destinos existentes. Habilita el paso de asignación en el flujo de trabajo de activación. Este permiso también requiere que se conceda el permiso [!UICONTROL Ver destinos] al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Activar segmento sin asignación] | Permite a los usuarios activar segmentos en destinos existentes sin mostrar el [paso de asignación](../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden agregar y eliminar segmentos en flujos de trabajo de activación, pero no pueden agregar ni eliminar atributos o identidades asignados. Este permiso también requiere que se conceda el permiso [!UICONTROL Ver destinos] al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Administrar y activar destinos de conjuntos de datos] | Capacidad para leer, crear, editar y deshabilitar flujos de exportación de conjuntos de datos. Capacidad para activar también datos en conjuntos de datos activos que se han creado. Este permiso también requiere que se conceda el permiso [!UICONTROL Ver destinos] al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Creación de destino] | Capacidad para crear destinos usando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Identity Management] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver áreas de nombres de identidad] | Acceso de solo lectura para áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver gráfico de identidad] | Acceso de solo lectura para gráficos de identidad. |
| [!DNL Intelligent Services] | [!UICONTROL Ver Attribution AI] | Acceso de solo lectura para configuraciones y perspectivas de Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Administrar Attribution AI] | Acceso para leer, crear, editar y eliminar modelos de Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Ver inteligencia artificial aplicada al cliente] | Acceso para leer o ver modelos de inteligencia artificial aplicada al cliente. |
| [!DNL Intelligent Services] | [!UICONTROL Administrar la inteligencia artificial aplicada al cliente] | Acceso para crear, actualizar, eliminar, habilitar o deshabilitar modelos de inteligencia artificial aplicada al cliente. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfiles] | Ingeste datos de varias fuentes, cree perfiles sólidos para clientes individuales y almacene datos habilitados para perfiles en el lago de datos y el almacén de datos del perfil del cliente en tiempo real. |
| [!DNL Profile Management] | [!UICONTROL Ver perfiles] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar segmentos] | Acceso para leer, crear, editar y eliminar segmentos. |
| [!DNL Profile Management] | [!UICONTROL Ver segmentos] | Acceso de solo lectura a segmentos disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar directivas de combinación] | Acceso para leer, crear, editar y eliminar políticas de combinación. |
| [!DNL Profile Management] | [!UICONTROL Ver directivas de combinación] | Acceso de solo lectura a las políticas de combinación disponibles. |
| [!DNL Profile Management] | [!UICONTROL Importar audiencias] | Acceso para leer, crear, editar y eliminar audiencias importadas. |
| [!DNL Profile Management] | [!UICONTROL Exportar audiencia para el segmento] | Capacidad para exportar un segmento de audiencia evaluado a un conjunto de datos. |
| [!DNL Profile Management] | [!UICONTROL Evaluar un segmento en una audiencia] | Capacidad para generar perfiles para una audiencia evaluando una definición de segmento. |
| [!DNL Profile Management] | [!UICONTROL Ver IA B2B] | Acceso de solo lectura a los ajustes y configuraciones de todos los servicios AI/ML de B2B. |
| [!DNL Profile Management] | [!UICONTROL Administrar IA B2B] | Acceso para leer, crear, editar y eliminar ajustes y configuraciones para todos los servicios AI/ML de B2B. |
| [!DNL Profile Management] | [!UICONTROL Ver perfil B2B] | Acceso de solo lectura a perfiles de entidad B2B (como Cuenta, Oportunidad, etc.), ajustes y configuraciones para todos los servicios AI/ML B2B y widgets de tablero B2B. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfil B2B] | Acceso para leer, crear, editar y eliminar perfiles de entidad B2B (como Cuenta, Oportunidad, etc.). Acceso de solo lectura para ajustes y configuraciones de todos los servicios AI/ML de B2B y widgets de tablero B2B. |
| [!DNL Query Service] | [!UICONTROL Administrar consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de Platform. |
| [!DNL Query Service] | [!UICONTROL Administrar integración del servicio de consultas] | Acceso para crear, actualizar y eliminar credenciales que no caducan para el acceso al servicio de consultas. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar zonas protegidas] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Ver zonas protegidas] | Acceso de solo lectura para zonas protegidas que pertenecen a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer una zona protegida] | Capacidad para restablecer una zona protegida. |

## Pasos siguientes

Al leer esta guía, se le han presentado los principios principales del control de acceso en Experience Platform. Ahora puede continuar con la [guía del usuario de control de acceso basado en atributos](./abac/overview.md) para ver los pasos detallados sobre cómo usar Experience Cloud para crear funciones y asignar permisos para Experience Platform.
