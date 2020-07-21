---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Control de acceso general
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 3%

---


# Control de acceso general

Control de acceso para [!DNL Experience Platform] se proporciona a través de [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en [!DNL Admin Console], que vinculan a los usuarios con permisos y entornos limitados.

## Jerarquía de Controles de acceso y flujo de trabajo

Para configurar control de acceso para [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga una integración de [!DNL Experience Platform] producto. La función mínima que otorga o retira permisos es la de administrador **[!UICONTROL de perfil de]** productos. Otras funciones de administrador que pueden administrar permisos son los administradores **[!UICONTROL de]** productos (pueden administrar todos los perfiles de un producto) y los administradores **** del sistema (sin restricciones). Consulte el artículo del Centro de ayuda de Adobe sobre funciones [](https://helpx.adobe.com/enterprise/using/admin-roles.html) administrativas para obtener más información.

>[!NOTE]
>
>A partir de este momento, cualquier mención de &quot;administrador&quot; en este documento se refiere a un administrador de perfiles de productos o a una versión posterior (como se describe anteriormente).

Un flujo de trabajo de alto nivel para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Tras suscribirse a Adobe Experience Platform, se envía un correo electrónico al administrador especificado en el formulario de registro.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona el **Adobe Experience Platform** de la lista de productos en la página de información general.
- El administrador puede realizar la vista de los perfiles [predeterminados del](#product-profiles) producto o crear nuevos perfiles de productos del cliente según sea necesario.
- El administrador puede editar los permisos y usuarios de cualquier perfil de producto existente.
- Al crear o editar un perfil de producto, el administrador agrega usuarios al perfil mediante la ficha **[!UICONTROL Usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos]de datos&quot; o &quot;[!UICONTROL Administrar Esquemas]&quot;) accediendo a la ficha **[!UICONTROL Permisos]** . Del mismo modo, el administrador puede asignar acceso a los entornos limitados mediante la misma ficha de permisos.
- Cuando los usuarios inician sesión en la interfaz de usuario, su acceso a [!DNL Experience Platform] [!DNL Platform] las funciones depende de los permisos que se les han concedido desde el paso 2. Por ejemplo, si un usuario no tiene el permiso &quot;Conjuntos[!UICONTROL de datos de]Vista&quot;, la ficha *[!UICONTROL Conjuntos]* de datos del menú lateral no estará visible para ese usuario.

Para ver los pasos más detallados sobre cómo administrar el control de acceso en [!DNL Experience Platform], consulte la guía [del usuario de](./ui/overview.md)control de acceso.

Todas las llamadas a [!DNL Experience Platform] API se validan para obtener permisos y devuelven errores si no se encuentran los permisos correspondientes en el contexto de usuario actual. Dentro de la interfaz de usuario, los elementos se ocultarán o alterarán según los permisos concedidos al usuario actual.

## Adobe Admin Console

Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso para su organización. A través de la consola, puede otorgar a grupos de usuarios permisos de acceso para diversas [!DNL Platform] funciones, como &quot;[!UICONTROL Administrar conjuntos]de datos&quot;, &quot;Conjuntos de datos de[!UICONTROL Vista]&quot; o &quot;[!UICONTROL Administrar Perfiles]&quot;.

### perfiles del producto

En el [!DNL Admin Console], los permisos se asignan a los usuarios mediante el uso de perfiles **[!UICONTROL de]** productos. Los perfiles de producto le permiten otorgar permisos a uno o varios usuarios, y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante perfiles de producto. Los usuarios pueden asignarse a uno o varios perfiles de productos pertenecientes a su organización.

### perfiles de producto predeterminados

[!DNL Experience Platform] viene con dos perfiles de producto predeterminados preconfigurados. La siguiente tabla describe lo que se proporciona en cada perfil predeterminado, incluido el simulador para pruebas al que conceden acceso, así como los permisos que conceden dentro del ámbito de ese simulador para pruebas.

| Perfil del producto | Acceso a Simulador para pruebas | Permisos |
| --- | --- | --- |
| Producción predeterminada - Acceso total | Producción | Todos los permisos aplicables a [!DNL Experience Platform], excepto los permisos de administración de Simulador para pruebas. |
| Administración predeterminada de Simulador para pruebas | N/D | Proporciona acceso solamente a los permisos de administración de Simuladores para pruebas. |

## Simuladores y permisos

[!DNL Experience Platform] proporciona acceso a un entorno limitado de producción y le permite crear **entornos** limitados que no sean de producción. Los entornos limitados que no son de producción son una forma de virtualización de datos que le permite aislar datos de otros entornos limitados y que generalmente se utilizan para experimentos de desarrollo, pruebas o pruebas. Los **[!UICONTROL permisos]** de un perfil de productos proporcionan a los usuarios del perfil acceso a [!DNL Platform] las funciones de los entornos del simulador para pruebas a los que se les ha concedido acceso.

Para obtener más información sobre los entornos limitados de [!DNL Experience Platform], consulte la información general [de los](../sandboxes/home.md)entornos limitados.

### Acceso a los entornos limitados

El acceso a los entornos limitados se administra mediante perfiles de productos. Para ver los pasos detallados sobre cómo habilitar el acceso a un simulador para un perfil de productos, consulte la guía del usuario de [control de acceso](./ui/overview.md).

Se puede otorgar a los usuarios acceso a uno o más entornos limitados dentro de un perfil de producto. Si un usuario está incluido en dos o más perfiles de productos, tendrá acceso a todos los entornos limitados incluidos en esos perfiles.

El permiso &quot;Administración de Simuladores para pruebas&quot; permite a los usuarios administrar, vista o restablecer entornos limitados.

### Permisos

La ficha **Permisos** de un perfil de producto muestra los entornos limitados y los permisos que están activos para ese perfil:

![](./images/permissions-overview.png)

Los permisos que se conceden a través del [!DNL Admin Console] se ordenan por categoría, y algunos permisos conceden acceso a varias funcionalidades de bajo nivel.

La siguiente tabla describe los permisos disponibles para [!DNL Experience Platform] en la [!DNL Admin Console], con descripciones de las [!DNL Platform] capacidades específicas a las que conceden acceso. Para ver los pasos detallados sobre cómo agregar permisos a un perfil de productos, consulte la guía del usuario de [control de acceso](./ui/overview.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Administrar Esquemas] | Acceso para leer, crear, editar y eliminar esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Esquemas de vistas] | Acceso de sólo lectura a esquemas y recursos relacionados. |
| [!DNL Data Management] | [!UICONTROL Administrar conjuntos de datos] | Acceso para leer, crear, editar y eliminar conjuntos de datos. Acceso de solo lectura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Conjuntos de datos de vistas] | Acceso de sólo lectura para conjuntos de datos y esquemas. |
| [!DNL Data Management] | [!UICONTROL Monitoreo de datos] | Acceso de sólo lectura a conjuntos de datos y flujos de monitoreo. |
| [!DNL Profile Management] | [!UICONTROL Administrar Perfiles] | Acceso para leer, crear, editar y eliminar conjuntos de datos que se utilizan para perfiles de clientes. Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Perfiles de Vista] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportar Audiencia para segmento] | Capacidad para exportar un segmento de audiencia evaluado a un conjunto de datos. |
| [!DNL Identities] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar Áreas de nombres de identidad. |
| [!DNL Identities] | [!UICONTROL Áreas de nombres de identidad de Vista] | Acceso de sólo lectura para Áreas de nombres de identidad. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar Simuladores] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Entornos aislados de vistas] | Acceso de sólo lectura para entornos limitados pertenecientes a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer un Simulador para pruebas] | Capacidad para restablecer un entorno limitado. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear, editar y deshabilitar destinos.* |
| [!DNL Destinations] | [!UICONTROL Destinos de Vista] | Acceso de sólo lectura a los destinos disponibles en la ficha *[!UICONTROL Catálogo]* y a los destinos autenticados en la ficha *[!UICONTROL Examinar]* .* |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Capacidad para activar datos en destinos activos que se hayan creado. Este permiso requiere que se concedan &quot;Destinos de Vista&quot; o &quot;Administrar [!UICONTROL destinos&quot;] al usuario que activará los destinos.* |
| [!DNL Data Ingestion] | [!UICONTROL Administrar fuentes] | Acceso para leer, crear, editar y deshabilitar fuentes. |
| [!DNL Data Ingestion] | [!UICONTROL Fuentes de Vista] | Acceso de sólo lectura a los orígenes disponibles en la ficha *[!UICONTROL Catálogo]* y a los orígenes autenticados en la ficha *[!UICONTROL Examinar]* . |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar área de trabajo de ciencias de datos] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |

_(*) Este permiso requiere disposiciones para[!DNL Real-time Customer Data Platform]. Para obtener más información sobre CDP en tiempo real, lea la información general[de CDP en tiempo](https://docs.adobe.com/content/help/es-ES/experience-platform/rtcdp/overview.html)real._

## Pasos siguientes

Al leer esta guía, usted ha sido presentado a los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar en la guía [del usuario de](./ui/overview.md) control de acceso para ver los pasos detallados sobre cómo utilizar [!DNL Admin Console] para crear perfiles de productos y asignar permisos para [!DNL Platform].