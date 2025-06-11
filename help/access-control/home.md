---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
title: Información general sobre el control de acceso
description: El control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 6a466770495b226f890ab67b21c5cb027fd46e02
workflow-type: tm+mt
source-wordcount: '3851'
ht-degree: 0%

---

# Información general sobre el control de acceso

El control de acceso para Adobe Experience Platform se proporciona mediante **[!UICONTROL Permisos]** en [Adobe Experience Cloud](https://experience.adobe.com/). Esta funcionalidad aprovecha las funciones y directivas que vinculan a los usuarios con permisos y zonas protegidas.

## Flujo de trabajo y jerarquía de control de acceso

Para configurar el control de acceso de Experience Platform, debe tener privilegios de administrador de sistemas o productos para una organización que tenga un producto de Experience Platform. La función mínima que puede conceder o retirar permisos es de administrador de productos. Otros roles de administrador que pueden administrar permisos son administradores del sistema (sin restricciones). Consulte el artículo del Centro de ayuda de Adobe sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este punto, cualquier mención de &quot;administrador&quot; en este documento hace referencia a un administrador de productos o superior (como se ha descrito anteriormente).

Un flujo de trabajo superior para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Tras obtener la licencia de Adobe Experience Platform, o de una aplicación o servicio de aplicación que utilice Experience Platform, se envía un correo electrónico al administrador especificado durante la licencia.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** de la lista de productos en la página de información general.
- Para conceder acceso a Experience Platform, se recomienda que el administrador agregue usuarios al perfil de producto predeterminado: `AEP-Default-All-Users`.
- En Permisos de Experience Platform, el administrador puede crear nuevas funciones o editar los permisos y usuarios de cualquier función existente.
- Al crear o editar una función, el administrador agrega usuarios a la función mediante la ficha **[!UICONTROL usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos de datos]&quot; o &quot;[!UICONTROL Administrar esquemas]&quot;) mediante la edición de los permisos de la función. Del mismo modo, el administrador puede asignar acceso a los entornos limitados utilizando la misma opción de edición.
- Cuando los usuarios inician sesión en la interfaz de usuario de Experience Platform, su acceso a las funciones de Experience Platform se basa en los permisos que se les han concedido desde el paso anterior. Por ejemplo, si un usuario no tiene el permiso [!UICONTROL Ver conjuntos de datos], la ficha **[!UICONTROL Conjuntos de datos]** del menú lateral no será visible para ese usuario.

Para ver pasos más detallados sobre cómo administrar el control de acceso en Experience Platform, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a las API de Experience Platform se validan para obtener permisos y devolverán errores si no se encuentran los permisos adecuados en el contexto de usuario actual. Dentro de la interfaz de usuario de, los elementos se ocultan o modifican según los permisos otorgados al usuario actual.

## Permisos {#platform-permissions}

[!UICONTROL Permisos] proporciona una ubicación central para administrar el acceso de Experience Platform en su organización. Mediante [!UICONTROL Permisos], puede conceder a grupos de usuarios permisos de acceso para diversas funciones de Experience Platform, como [!UICONTROL Administrar conjuntos de datos], [!UICONTROL Ver conjuntos de datos] o [!UICONTROL Administrar perfiles].

### Funciones

En la sección [!UICONTROL Roles], los permisos se asignan a los usuarios mediante el uso de funciones. Las funciones permiten conceder permisos a uno o varios usuarios y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante funciones. Los usuarios pueden tener asignada una o varias funciones que pertenezcan a su organización.

### Funciones predeterminadas

Experience Platform viene con dos funciones predeterminadas preconfiguradas. En la tabla siguiente se describe lo que se proporciona en cada perfil predeterminado, incluida la zona protegida a la que otorgan acceso, así como los permisos que otorgan dentro del ámbito de esa zona protegida.

| Función | Acceso a zona protegida | Permisos |
| --- | --- | --- |
| Acceso a todo de producción predeterminado | Prod | Todos los permisos aplicables a Experience Platform, excepto los permisos de administración de zonas protegidas. |
| Administradores de zona protegida | N/A | Proporciona acceso a la zona protegida `Prod` y a los permisos de administración de la zona protegida. |

## Zonas protegidas y permisos

Las zonas protegidas que no son de producción son una forma de virtualización de datos que le permite aislar datos de otras zonas protegidas y que generalmente se utilizan para experimentos, pruebas o ensayos de desarrollo. Los permisos de una función otorgan a los usuarios de la función acceso a las funciones de Experience Platform dentro de los entornos de zona protegida a los que se les ha concedido acceso. Una licencia predeterminada de Experience Platform le concede cinco zonas protegidas (una de producción y cuatro que no son de producción). Puede agregar paquetes de diez zonas protegidas que no sean de producción hasta un máximo de 75 zonas protegidas en total. Póngase en contacto con el administrador de su organización o con su representante de ventas de Adobe para obtener más información.

Para obtener más información sobre las zonas protegidas en Experience Platform, consulte la [descripción general de las zonas protegidas](../sandboxes/home.md).

### Acceso a zonas protegidas

El acceso a las zonas protegidas se administra mediante funciones. Para ver los pasos detallados sobre cómo habilitar el acceso a una zona protegida para un rol, consulte la [guía de roles de control de acceso basado en atributos](./abac/ui/roles.md).

Se puede otorgar acceso a los usuarios a una o más zonas protegidas dentro de una función. Si un usuario está incluido en dos o más funciones, ese usuario tendrá acceso a todas las zonas protegidas incluidas en esas funciones.

El permiso &quot;Administración de zonas protegidas&quot; permite a los usuarios administrar, ver o restablecer zonas protegidas.

### Permisos de recursos {#permissions}

Los permisos de recursos conceden acceso a funciones específicas de Experience Platform. Los recursos se dividen en categorías que contienen un conjunto de permisos relevantes, que se pueden asignar individualmente a las funciones.

En [!UICONTROL Permisos], el área de trabajo de recursos de un rol muestra los entornos limitados y los permisos activos para ese rol:

![Espacio de trabajo de recursos de un rol con una lista de categorías y permisos seleccionados.](./images/permissions.png)

En la tabla siguiente se describen las categorías de recursos disponibles para Experience Platform y las aplicaciones administradas mediante Permisos:

| Categoría | Descripción |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Configurar, administrar y ver permisos para [!DNL Adobe Mix Modeler]. |
| [!DNL AI Assistant] | Configure los permisos de [!DNL AI Assistant]. |
| [!DNL Alerts] | Configure los permisos de administración, resolución y visualización para el historial de alertas y alertas. |
| [!DNL B2B Account Lists] | Configure los permisos de administración, visualización y publicación para listas de cuentas B2B, incluidas acciones como agregar, quitar, importar y eliminar cuentas de listas de cuentas. |
| [!DNL B2B Admin Configurations] | Configure los permisos de administración y visualización de administración para las configuraciones de administración B2B, incluidas las conexiones de administración de recursos digitales, los repositorios de recursos y los eventos. |
| [!DNL B2B Assets] | Configure y vea permisos para recursos B2B, incluidos correos electrónicos, SMS, páginas de aterrizaje, fragmentos, plantillas e imágenes. |
| [!DNL B2B Buying Groups] | Configure y vea permisos de para grupos de compra B2B, incluidas funciones como intereses de soluciones, funciones, plantillas y estado de grupos de compra. |
| [!DNL B2B Channel Configurations] | Configure permisos de administración y visualización para configuraciones de canal B2B, incluida la configuración de límites de comunicación, credenciales de API y seguridad. |
| [!DNL B2B Dashboards] | Configure permisos de visualización para paneles B2B, incluidas funciones como participación de cuentas, compra de fases de grupo, aumento de cuentas y cobertura de contactos. |
| [!DNL B2B Journeys] | Configure los permisos de administración, visualización y publicación para recorridos B2B, incluidas funciones como acciones de cuenta y persona, detectores de eventos y rutas divididas. |
| [!DNL Campaigns] | Configure los permisos de administración, publicación y visualización de campañas en Journey Optimizer. |
| [!DNL Channel Configurations] | Configure las funciones de administración, visualización y exportación de configuraciones de canal, como subdominios, grupos de IP, ajustes preestablecidos de mensaje, registros PTR, listas de supresión, configuración de página de aterrizaje, configuración de SMS y enrutamiento de archivos. |
| [!DNL Collaborations] | Configure los permisos de administración y visualización para las funciones de Real-Time Customer Data Profile Collaboration. |
| [!DNL Computed Attributes] | Configure los permisos de administración y visualización para los atributos calculados de borrador o publicados. |
| [!DNL Customer Managed Keys] | Configure y administre permisos para claves administradas por el cliente. |
| [!DNL Dashboards] | Configure los permisos de administración y visualización en los paneles estándar, personalizados y con licencia. |
| [!DNL Data Collection] | Configure los permisos de administración y visualización de flujos de datos. |
| [!DNL Data Governance] | Configure y aplique permisos de administración, aplicación y visualización para funciones de control de datos como etiquetas, políticas y registros de actividades. |
| [!DNL Data Ingestion] | Configure permisos de administración y visualización para funciones de ingesta de datos como fuentes y uso compartido de audiencias. |
| [!DNL Data Lifecycle] | Configure los permisos de administración y visualización para las funciones de higiene de datos. |
| [!DNL Data Management] | Configure permisos de administración y visualización para funciones de administración de datos como conjuntos de datos y monitorización de conjuntos de datos y flujos. |
| [!DNL Data Modeling] | Configure permisos de administración y visualización para funciones de modelado de datos como esquemas, relaciones y metadatos de identidad. |
| [!DNL Data Science Workspace] | Configure los permisos de administración de [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | Configure y vea permisos para decisiones, ofertas y funciones de estrategia de clasificación en la administración de decisiones. |
| [!DNL Destinations] | Configure y vea permisos para destinos, incluidas funciones como la activación y la creación con Destinos SDK. |
| [!DNL Federated Data] | Configure los permisos de administración y visualización para las funciones de datos federados. |
| [!DNL Identity Management] | Configure permisos de administración y visualización para funciones del servicio de identidad, como áreas de nombres de identidad y el gráfico de identidades. |
| [!DNL Intelligent Service] | Configure y vea permisos de administración para la inteligencia artificial aplicada a la atribución y la inteligencia artificial aplicada al cliente en el servicio inteligente. |
| [!DNL IP Warmup Configurations] | Configure y vea permisos para planes de calentamiento de IP y vea permisos para ver informes de calentamiento de IP. |
| [!DNL Journey Optimizer Library] | Configure y administre permisos en los elementos de biblioteca de Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Configure los permisos de administración y visualización de reglas de frecuencia en Adobe Journey Optimizer. |
| [!DNL Journeys] | Configure los permisos de administración, publicación y visualización de recorridos, incluidas funciones como informes de recorridos, eventos, fuentes de datos y acciones. |
| [!DNL Messages] | Configure los permisos de administración, publicación y visualización de mensajes, incluidas funciones como la vista previa y la prueba de mensajes. |
| [!DNL Privacy Service] | Configure y vea permisos para las funciones de Privacy Service. |
| [!DNL Profile Management] | Configure los permisos de administración, visualización, exportación y evaluación para funciones del servicio de perfil como audiencias, perfiles y políticas de combinación. |
| [!DNL Prospects] | Configure y vea permisos para esquemas, perfiles y audiencias de clientes potenciales, incluidas funciones como ver el acordeón de clientes potenciales. |
| [!DNL Query Service] | Configure permisos de administración para las funciones del servicio de consultas, como credenciales que no caducan y consultas SQL estructuradas. |
| [!DNL Reports] | Configure los permisos de visualización de los informes de canal. |
| [!DNL Sandbox Administration] | Configure los permisos de administrar, ver y restablecer al administrar zonas protegidas. |
| [!DNL Traits Configuration] | Configure y visualice rasgos mediante la interfaz de usuario de atributos calculados. |
| [!DNL Translation Services] | Configure y vea permisos de administración para servicios de traducción para proyectos, tareas, revisiones, recursos internos, configuración y proveedores. |

En la tabla siguiente se describen los permisos disponibles para Experience Platform en la función, con descripciones de las funciones específicas de Experience Platform a las que otorgan acceso. Para ver los pasos detallados sobre cómo agregar permisos a un rol, consulte la [guía de roles de control de acceso basado en atributos](./abac/ui/roles.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Administrar datos armonizados de Adobe Mix Modeler] | La capacidad de ver y modificar datos armonizados. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Ver datos armonizados de Adobe Mix Modeler] | Acceso de solo lectura a datos armonizados. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Administrar configuraciones de modelos de Adobe Mix Modeler] | La capacidad para ver y modificar configuraciones de modelos. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Ver configuraciones de modelos Adobe Mix Modeler] | Acceso de solo lectura a configuraciones de modelos. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Administrar configuraciones de planes de modelos Adobe Mix Modeler] | La capacidad de ver y modificar configuraciones de planes. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Ver configuraciones de planes de modelos Adobe Mix Modeler] | Acceso de solo lectura a configuraciones de planes. |
| [!DNL AI Assistant] | [!UICONTROL Habilitar el asistente de IA] | Capacidad para hacer preguntas sobre [[!DNL [AI assistant]]](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL Ver datos operativos] | Acceso para obtener respuestas a [consultas de perspectivas operacionales](../ai-assistant/home.md##operational-insights). |
| [!DNL AI Assistant] | [!UICONTROL Generar contenido] | Permitir que los usuarios generen contenido mediante [!DNL AI Assistant]. |
| [!DNL AI Assistant] | [!UICONTROL Administrar kit de marca] | Permitir que los usuarios creen directrices de marca utilizando [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL Ver historial de alertas] | Acceso de solo lectura para el historial de alertas. |
| [!DNL Alerts] | [!UICONTROL Resolver alertas] | Acceso para leer, editar y eliminar alertas. |
| [!DNL Alerts] | [!UICONTROL Ver alertas] | Acceso de solo lectura para alertas. |
| [!DNL Alerts] | [!UICONTROL Administrar alertas] | Acceso para leer, crear, editar y eliminar alertas. |
| [!DNL B2B Account Lists] | [!UICONTROL Administrar listas de cuentas B2B] | Capacidad para ver y acceder a **[!UICONTROL Listas de cuentas]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Listas de cuentas]** deben tener acceso a todas las funciones CRUD de Listas de cuentas: `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Administrar configuraciones de administración B2B] | Capacidad para ver y acceder a **[!UICONTROL Configuraciones de administración B2B]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Configuraciones de administración B2B]** deben tener acceso a todas las funciones CRUD de credenciales de API de SMS: `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Administrar Assets B2B] | Capacidad para ver y acceder a **[!UICONTROL Assets]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Assets]** deben tener acceso a todas las funciones de Assets CRUD: `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Administrar plantillas B2B] | Capacidad para ver y acceder a **[!UICONTROL Plantillas]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Plantillas]** deben tener acceso a todas las funciones de plantillas CRUD: `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Administrar fragmentos B2B] | Capacidad para ver y acceder a **[!UICONTROL Fragmentos]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Fragmentos]** deben tener acceso a todas las funciones de CRUD de los fragmentos: `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Administrar grupos de compra B2B] | Capacidad para ver **[!UICONTROL grupos de compra]** y acceder a ellos en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Grupos de compra]** deben tener acceso a todas las funciones de CRUD de los grupos de compra: `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Administrar paneles de participación B2B] | Capacidad para ver y acceder a **[!UICONTROL Tablero]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Paneles]** deben tener acceso a todas las funciones de CRUD de los paneles: `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Administrar configuraciones de canales B2B] | Capacidad para ver **[!UICONTROL Canales]** y obtener acceso a ellos en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Canales]** deben tener acceso a todas las funciones de canales CRUD: `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Administrar Recorridos de cuenta B2B] | Capacidad para ver y acceder a **[!UICONTROL Recorridos de la cuenta]** en la navegación izquierda. Los usuarios con acceso a **[!UICONTROL Recorridos de cuenta]** deben tener acceso a todas las funciones de CRUD de Recorridos de cuenta: `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Administrar campañas] | Acceso para leer, crear, editar y eliminar campañas. |
| [!DNL Campaigns] | [!UICONTROL Aprobar y publicar campañas] | La capacidad para aprobar y publicar campañas. |
| [!DNL Campaigns] | [!UICONTROL Publicar campañas] | Capacidad para publicar campañas. |
| [!DNL Campaigns] | [!UICONTROL Ver campañas] | Acceso de solo lectura a campañas. |
| [!DNL Campaigns] | [!UICONTROL Ver informe de campañas] | Acceso de solo lectura a los informes de campaña. |
| [!DNL Channel Configurations] | [!UICONTROL Configuración general de vista de mensajes] | Acceso de solo lectura a la configuración general de los mensajes. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar delegaciones de subdominios] | Acceso para leer, crear, editar y eliminar delegaciones de subdominios. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar grupos de IP] | Acceso para leer, crear y editar grupos de IP. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar mensajes Configuración general] | Acceso para leer, crear, editar y eliminar mensajes de la configuración general. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar ajustes preestablecidos de mensajes] | Acceso para leer, crear, editar y eliminar mensajes de ajustes preestablecidos. |
| [!DNL Channel Configurations] | [!UICONTROL Ver ajustes preestablecidos de mensajes] | Acceso de solo lectura a los ajustes preestablecidos de mensajes. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar registros PTR] | Acceso para leer y editar registros PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Ver registros PTR] | Acceso de solo lectura a registros PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar supresión] | Acceso para leer, crear, editar y eliminar reglas de supresión. |
| [!DNL Channel Configurations] | [!UICONTROL Ver lista de supresión] | Acceso de solo lectura a la lista de supresión. |
| [!DNL Channel Configurations] | [!UICONTROL Lista de supresión de exportación] | Acceso para exportar la lista de supresión como archivo CSV. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar configuración de página de aterrizaje] | Acceso para leer, crear, editar y eliminar la configuración de la página de aterrizaje. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar configuración de SMS] | Acceso para leer, crear, editar y eliminar la configuración de SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar subdominios de SMS] | Acceso para leer, crear, editar y eliminar subdominios de SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar enrutamiento de archivos] | Acceso para leer, crear, editar y eliminar rutas de archivos. |
| [!DNL Channel Configurations] | [!UICONTROL Ver enrutamiento de archivos] | Acceso de sólo lectura a las rutas de archivos. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar lista de semilla] | La capacidad de crear y editar la lista de semilla. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar configuración de idioma] | La capacidad de crear y editar la configuración de idioma. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar subdominios web] | La capacidad de crear y editar subdominios web de CJM. |
| [!DNL Channel Configurations] | [!UICONTROL Administrar credenciales push] | La capacidad de crear, editar y eliminar credenciales push. |
| [!DNL Collaborations] | [!UICONTROL Administrar instancias de Collaboration] | Ver, crear, actualizar y eliminar las instancias de colaboración de una organización. Descubra las instancias de colaboración de otras organizaciones. |
| [!DNL Collaborations] | [!UICONTROL Leer instancias de Collaboration] | Lea las instancias de colaboración de una organización y descubra las instancias de colaboración de otras organizaciones. |
| [!DNL Collaborations] | [!UICONTROL Administrar invitaciones de conexión] | Vea, cree y elimine invitaciones a conexiones iniciadas por su organización. Aceptar y rechazar la invitación de conexión iniciada por otras organizaciones. |
| [!DNL Collaborations] | [!UICONTROL Leer Invitaciones De Conexión] | Acceso de solo lectura a las invitaciones de conexión. |
| [!DNL Collaborations] | [!UICONTROL Administrar conexiones de Collaboration] | Un anunciante puede ver, crear y actualizar la configuración, así como enviar y eliminar conexiones. Un editor puede ver, aceptar o rechazar conexiones. |
| [!DNL Collaborations] | [!UICONTROL Leer conexiones de Collaboration] | Acceso de solo lectura a conexiones. |
| [!DNL Collaborations] | [!UICONTROL Administrar datos de audiencia] | Incorporar y descubrir audiencias. Actualice las audiencias públicas, privadas y personalizadas y administre la configuración de metadatos del inventario de audiencias. |
| [!DNL Collaborations] | [!UICONTROL Leer datos de audiencia] | Leer y descubrir audiencias. |
| [!DNL Collaborations] | [!UICONTROL Administrar datos de medición] | Incorpore, actualice y elimine datos de medición. |
| [!DNL Collaborations] | [!UICONTROL Leer datos de medición] | Acceso de solo lectura a los datos de medición. |
| [!DNL Collaborations] | [!UICONTROL Administrar proyectos] | Ver, crear, actualizar y eliminar proyectos para cualquiera de las actividades de detección, uso compartido, activación y medición. |
| [!DNL Collaborations] | [!UICONTROL Leer proyectos] | Vea proyectos para cualquiera de las actividades de detección, uso compartido, activación y medición. |
| [!DNL Collaborations] | [!UICONTROL Actividades de usuario de lectura] | Acceso de solo lectura a actividades de usuario. |
| [!DNL Collaborations] | [!UICONTROL Exportar actividades de usuario] | Exportar actividades de usuario. |
| [!DNL Collaborations] | [!UICONTROL Leer la supervisión de crédito de Collaboration] | Supervisión del crédito a nivel de organización e instancia. |
| [!DNL Computed Attributes] | [!UICONTROL Ver atributos calculados] | Acceso de solo lectura para la pestaña de atributos calculados, inventario y detalles. |
| [!DNL Computed Attributes] | [!UICONTROL Administrar atributos calculados] | Acceso para leer, crear, eliminar borradores y desactivar atributos calculados. |
| [!DNL Customer Managed Keys] | [!UICONTROL Administrar claves administradas por el cliente] | Acceso para ver y configurar las claves administradas por el cliente. |
| [!DNL Dashboards] | [!UICONTROL Ver tablero de uso de licencias] | Acceso de solo lectura para ver el panel de uso de licencias. |
| [!DNL Dashboards] | [!UICONTROL Administrar paneles estándar] | Agregue atributos personalizados que aún no estén en el almacén de datos. |
| [!DNL Dashboards] | [!UICONTROL Ver paneles estándar] | Acceso de solo lectura a los paneles Perfiles, Destinos y Segmentos. También permite el acceso a los paneles en la navegación izquierda y a la pestaña de inventario e integraciones de los paneles. |
| [!DNL Dashboards] | [!UICONTROL Administrar paneles personalizados] | Acceso para crear o editar un tablero. |
| [!DNL Dashboards] | [!UICONTROL Ver paneles personalizados] | Acceso de solo lectura a los paneles definidos por el usuario. |
| [!DNL Dashboards] | [!UICONTROL Administrar horarios de informes] | Capacidad para crear programaciones. |
| [!DNL Dashboards] | [!UICONTROL Exportar datos de panel] | Controla la capacidad de un usuario para exportar datos de tablas desde paneles de modo de consulta profesional. |
| [!DNL Data Collection] | [!UICONTROL Administrar flujos de datos] | Acceso para leer, crear y editar flujos de datos. |
| [!DNL Data Collection] | [!UICONTROL Ver flujos de datos] | Acceso de solo lectura a flujos de datos. |
| [!DNL Data Governance] | [!UICONTROL Administrar etiquetas de uso] | Acceso para leer, crear y eliminar etiquetas de uso. |
| [!DNL Data Governance] | [!UICONTROL Administrar Políticas De Uso De Datos] | Acceso para leer, crear, editar y eliminar políticas de uso de datos. |
| [!DNL Data Governance] | [!UICONTROL Ver directivas de uso de datos] | Acceso de solo lectura para directivas de uso de datos pertenecientes a su organización. |
| [!DNL Data Governance] | [!UICONTROL Ver registro de actividad de usuario] | Acceso de solo lectura para ver [registros de auditoría](../landing/governance-privacy-security/audit-logs/overview.md) registrados de actividades de Experience Platform. |
| [!DNL Data Governance] | [!UICONTROL Ver consola de privacidad] | Acceso de solo lectura a las consolas de privacidad. |
| [!DNL Data Ingestion] | [!UICONTROL Administrar orígenes] | Acceso para leer, crear, editar y deshabilitar orígenes. |
| [!DNL Data Ingestion] | [!UICONTROL Ver orígenes] | Acceso de solo lectura a orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y orígenes autenticados en la ficha **[!UICONTROL Examinar]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Acceso para crear, aceptar y rechazar el uso compartido de socios para conectar dos organizaciones y habilitar [!DNL Segment Match] flujos. |
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
| [!DNL Decision Management] | [!UICONTROL Administrar Experience Decisioning] | Capacidad para administrar entidades de experience decisioning. |
| [!DNL Decision Management] | [!UICONTROL Ver Experience Decisioning] | Acceso de solo lectura a entidades de Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Administrar decisiones] | Acceso para leer, crear, editar y eliminar entidades de toma de decisiones. |
| [!DNL Decisions Management] | [!UICONTROL Ver decisiones] | Acceso de solo lectura a entidades de decisión. |
| [!DNL Decision Management] | [!UICONTROL Administrar ofertas] | Acceso para leer, crear, editar y eliminar todas las ofertas y componentes. Acceso de solo lectura a decisiones y colecciones. |
| [!DNL Decsion Management] | [!UICONTROL Administrar estrategias de clasificación] | Acceso para leer, crear, editar y eliminar informes personalizados y utilizar funciones de acción. |
| [!DNL Destinations] | [!UICONTROL Ver destinos] | Acceso de solo lectura para ver los destinos disponibles en la ficha **[!UICONTROL Catálogo]** y los destinos autenticados en la ficha **[!UICONTROL Examinar]**. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear y eliminar destinos, conexiones y cuentas de destino. |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Capacidad para activar datos en destinos activos que se han creado. Este permiso también requiere que se conceda [!UICONTROL Ver destinos] o [!UICONTROL Administrar destinos] al usuario que activará los destinos. |
| [!DNL Destinations] | [!UICONTROL Activar segmento sin asignación] | Capacidad para activar audiencias en destinos existentes, sin mostrar el [paso de asignación](../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden agregar y eliminar audiencias en flujos de trabajo de activación, pero no pueden agregar ni eliminar atributos o identidades asignados. Este permiso también requiere que se conceda el permiso [!UICONTROL Ver destinos] al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Administrar y activar destinos de conjuntos de datos] | Capacidad para leer, crear, editar y deshabilitar flujos de exportación de conjuntos de datos. Capacidad para activar también datos en conjuntos de datos activos que se han creado. Este permiso también requiere que se conceda el permiso [!UICONTROL Ver destinos] al usuario que activará los datos en los destinos. |
| [!DNL Destinations] | [!UICONTROL Creación de destino] | Capacidad para crear destinos usando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Administrar datos federados] | La capacidad de acceder a todas las funciones de datos federados, como la creación de esquemas, modelos y composiciones. |
| [!DNL Identity Management] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver áreas de nombres de identidad] | Acceso de solo lectura para áreas de nombres de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver gráfico de identidad] | Acceso de solo lectura para gráficos de identidad. |
| [!DNL Identity Management] | [!UICONTROL Administrar configuración de identidad] | Acceso para leer, crear y editar la configuración de identidad. |
| [!DNL Identity Management] | [!UICONTROL Ver configuración de identidad] | Acceso de solo lectura a la configuración de identidad. |
| [!DNL Intelligent Services] | [!UICONTROL Ver inteligencia artificial aplicada a la atribución] | Acceso de solo lectura para la configuración y las perspectivas de Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Administrar inteligencia artificial aplicada a la atribución] | Acceso para leer, crear, editar y eliminar modelos de inteligencia artificial aplicada a la atribución. |
| [!DNL Intelligent Services] | [!UICONTROL Ver inteligencia artificial aplicada al cliente] | Acceso para leer o ver modelos de inteligencia artificial aplicada al cliente. |
| [!DNL Intelligent Services] | [!UICONTROL Administrar la inteligencia artificial aplicada al cliente] | Acceso para crear, actualizar, eliminar, habilitar o deshabilitar modelos de inteligencia artificial aplicada al cliente. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Ver planes de calentamiento de IP] | Acceso de solo lectura a planes de calentamiento de IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Administrar planes de calentamiento de IP] | La capacidad de administrar planes de calentamiento de IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Ver informes de calentamiento de IP] | Acceso de solo lectura a informes de calentamiento de IP. |
| [!DNL Journeys] | [!UICONTROL Administrar Recorridos] | Acceso para leer, crear, editar y eliminar recorridos. |
| [!DNL Journeys] | [!UICONTROL Ver Recorridos] | Acceso de solo lectura a recorrido. |
| [!DNL Journeys] | [!UICONTROL Ver informe de Recorridos] | Informe de acceso de solo lectura a recorridos. |
| [!DNL Journeys] | [!UICONTROL Administrar eventos, fuentes de datos y acciones de Recorrido] | Acceso para leer, crear, editar y eliminar eventos, fuentes de datos o acciones. |
| [!DNL Journeys] | [!UICONTROL Ver eventos, fuentes de datos y acciones de Recorridos] | Acceso de solo lectura a eventos, fuentes de datos o acciones. |
| [!DNL Journeys] | [!UICONTROL Aprobar y publicar Recorridos] | Capacidad para aprobar y publicar recorridos cuando se aplica una directiva. |
| [!DNL Journeys] | [!UICONTROL Publicar Recorridos] | Capacidad para publicar recorridos. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Administrar elementos de biblioteca] | La capacidad de añadir y eliminar expresiones guardadas. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publicar fragmentos] | La capacidad de publicar fragmentos de contenido. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simular contenido] | Acceso a la opción de simular contenido para la vista previa y la revisión. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Ver reglas de frecuencia] | Acceso de solo lectura a reglas de frecuencia. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Administrar reglas de frecuencia] | Acceso para leer, crear, editar o eliminar reglas de frecuencia. |
| [!DNL Messages] | [!UICONTROL Administrar mensajes] | Acceso para leer, crear, editar y eliminar mensajes. |
| [!DNL Messages] | [!UICONTROL Ver mensajes] | Acceso de solo lectura a los mensajes. |
| [!DNL Messages] | [!UICONTROL Ver informe de mensajes] | Acceso para leer y editar informes de mensajes. |
| [!DNL Messages] | [!UICONTROL Publicar mensajes] | Capacidad para publicar mensajes. |
| [!DNL Messages] | [!UICONTROL Administrar vista previa y prueba de mensajes] | Capacidad para aprobar y publicar mensajes cuando se aplica una directiva. |
| [!DNL Privacy Service] | [!UICONTROL Administrar Privacy Service] | Acceso a flujos de trabajo de privacidad de lectura y escritura. |
| [!DNL Privacy Service] | [!UICONTROL Ver Privacy Service] | Acceso de solo lectura a flujos de trabajo de privacidad. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfiles] | Acceso para leer, crear, editar y eliminar conjuntos de datos que se utilizan para perfiles de clientes. Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Ver perfiles] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar segmentos] | Acceso para leer, crear, editar y eliminar audiencias. |
| [!DNL Profile Management] | [!UICONTROL Ver segmentos] | Acceso de solo lectura a audiencias disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar directivas de combinación] | Acceso para leer, crear, editar y eliminar políticas de combinación. |
| [!DNL Profile Management] | [!UICONTROL Ver directivas de combinación] | Acceso de solo lectura a las políticas de combinación disponibles. |
| [!DNL Profile Management] | [!UICONTROL Importar audiencias] | Capacidad para utilizar el flujo de trabajo de carga de CSV para importar nuevas audiencias. |
| [!DNL Profile Management] | [!UICONTROL Exportar segmento de audiencia] | Capacidad para exportar una audiencia evaluada a un conjunto de datos. |
| [!DNL Profile Management] | [!UICONTROL Evaluar un segmento en una audiencia] | Capacidad para generar perfiles para una audiencia evaluando una definición de segmento. |
| [!DNL Profile Management] | [!UICONTROL Ver IA B2B] | Acceso de solo lectura a los ajustes y configuraciones de todos los servicios AI/ML de B2B. |
| [!DNL Profile Management] | [!UICONTROL Administrar IA B2B] | Acceso para leer, crear, editar y eliminar ajustes y configuraciones para todos los servicios AI/ML de B2B. |
| [!DNL Profile Management] | [!UICONTROL Ver perfil B2B] | Acceso de solo lectura a perfiles de entidad B2B (como Cuenta, Oportunidad, etc.), ajustes y configuraciones para todos los servicios AI/ML B2B y widgets de tablero B2B. |
| [!DNL Profile Management] | [!UICONTROL Administrar perfil B2B] | Acceso para leer, crear, editar y eliminar perfiles de entidad B2B (como Cuenta, Oportunidad, etc.). Acceso de solo lectura para ajustes y configuraciones de todos los servicios AI/ML de B2B y widgets de tablero B2B. |
| [!DNL Profile Management] | [!UICONTROL Administrar Valores De Búsqueda] | Capacidad para crear o eliminar audiencias de similitud. |
| [!DNL Profile Management] | [!UICONTROL Ver experiencia B2B] | Capacidad para ver perfiles y atributos B2B. |
| [!DNL Profile Management] | [!UICONTROL Ver configuración de perfil] | Acceso de solo lectura a todas las configuraciones de perfil. |
| [!DNL Profile Management] | [!UICONTROL Administrar configuración de perfil] | Acceso para leer y editar todas las configuraciones de perfil. |
| [!DNL Prospects] | [!UICONTROL Ver clientes potenciales] | Acceso de solo lectura a esquemas, perfiles, audiencias y el acordeón del cliente potencial. |
| [!DNL Prospects] | [!UICONTROL Administrar clientes potenciales] | Capacidad para crear y administrar esquemas, perfiles y audiencias de clientes potenciales. Acceso de solo lectura al acordeón del cliente potencial. |
| [!DNL Query Service] | [!UICONTROL Administrar consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de Experience Platform. |
| [!DNL Query Service] | [!UICONTROL Administrar integración del servicio de consultas] | Acceso para crear, actualizar y eliminar credenciales que no caducan para el acceso al servicio de consultas. |
| [!DNL Query Service] | [!UICONTROL Administrar sesiones de consulta] | Capacidad para expulsar sesiones existentes. |
| [!DNL Query Service] | [!UICONTROL Administrar Lista de permitidos] | Capacidad para administrar restricciones de IP para su organización. |
| [!DNL Reports] | [!UICONTROL Ver informes de canal] | La capacidad de ver y modificar informes de canal. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar zonas protegidas] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Ver zonas protegidas] | Acceso de solo lectura para zonas protegidas que pertenecen a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer una zona protegida] | Capacidad para restablecer una zona protegida. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar paquetes] | Acceso para crear, importar o exportar paquetes. |
| [!DNL Sandbox Administration] | [!UICONTROL Compartir paquetes] | Acceso para compartir paquetes entre diferentes organizaciones. |
| [!DNL Traits Configurations] | [!UICONTROL Ver rasgos] | Acceso de solo lectura para características. |
| [!DNL Traits Configurations] | [!UICONTROL Administrar características] | Acceso para administrar características. |
| [!DNL Translation Service] | [!UICONTROL Administrar proyectos de traducción] | La capacidad de administrar proyectos de traducción. |
| [!DNL Translation Service] | [!UICONTROL Ver proyectos de traducción] | Acceso de solo lectura a proyectos de traducción. |
| [!DNL Translation Service] | [!UICONTROL Administrar tareas de traducción] | La capacidad de administrar las tareas de traducción. |
| [!DNL Translation Service] | [!UICONTROL Ver tareas de traducción] | Acceso de solo lectura a tareas de traducción. |
| [!DNL Translation Service] | [!UICONTROL Administrar revisiones de traducción] | La capacidad de administrar revisiones de traducción. |
| [!DNL Translation Service] | [!UICONTROL Ver críticas de traducción] | Acceso de solo lectura a las revisiones de traducción. |
| [!DNL Translation Service] | [!UICONTROL Administrar traducción internamente] | La capacidad de administrar la traducción interna. |
| [!DNL Translation Service] | [!UICONTROL Ver traducción internamente] | Acceso de solo lectura a la traducción interna. |
| [!DNL Translation Service] | [!UICONTROL Administrar configuración de traducción] | La capacidad de los administradores para administrar la configuración de traducción. |
| [!DNL Translation Service] | [!UICONTROL Administrar proveedores de traducción] | La capacidad de administrar proveedores de traducción. |

## Pasos siguientes

Al leer esta guía, se le han presentado los principios principales del control de acceso en Experience Platform. Ahora puede continuar con la [guía del usuario de control de acceso basado en atributos](./abac/overview.md) para ver los pasos detallados sobre cómo usar Experience Cloud para crear funciones y asignar permisos para Experience Platform.
