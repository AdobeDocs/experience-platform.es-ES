---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: Control de acceso general
description: Control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles del producto en el Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
translation-type: tm+mt
source-git-commit: ccb7286e47aa4cf6356d22f84111b0c0fb30dfa8
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 3%

---


# Control de acceso general

Control de acceso para [!DNL Experience Platform] se proporciona a través del [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en [!DNL Admin Console], que vinculan a los usuarios con permisos y entornos limitados.

## Jerarquía de controles de acceso y flujo de trabajo

Para configurar control de acceso para [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga una integración de [!DNL Experience Platform] producto. La función mínima que otorga o retira permisos es un administrador de perfil de productos. Otras funciones de administrador que pueden administrar permisos son los administradores de productos (pueden administrar todos los perfiles de un producto) y los administradores de sistemas (sin restricciones). Consulte el artículo de Adobe Help Center sobre funciones [](https://helpx.adobe.com/enterprise/using/admin-roles.html) administrativas para obtener más información.

>[!NOTE]
>
>A partir de este momento, cualquier mención de &quot;administrador&quot; en este documento se refiere a un administrador de perfiles de productos o a una versión posterior (como se describe anteriormente).

Un flujo de trabajo de alto nivel para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Después de otorgar licencias a Adobe Experience Platform o a un servicio de aplicaciones/aplicaciones que utiliza Experience Platform, se envía un correo electrónico al administrador especificado durante la licencia.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** en la lista de productos de la página de información general.
- El administrador puede realizar la vista de los perfiles [predeterminados del](#product-profiles) producto o crear nuevos perfiles de productos del cliente según sea necesario.
- El administrador puede editar los permisos y usuarios de cualquier perfil de producto existente.
- Al crear o editar un perfil de producto, el administrador agrega usuarios al perfil mediante la ficha **[!UICONTROL Usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos]de datos&quot; o &quot;[!UICONTROL Administrar Esquemas]&quot;) accediendo a la ficha **[!UICONTROL Permisos]** . Del mismo modo, el administrador puede asignar acceso a los entornos limitados mediante la misma ficha de permisos.
- Cuando los usuarios inician sesión en la interfaz de usuario, su acceso a [!DNL Experience Platform] [!DNL Platform] las funciones depende de los permisos que se les han concedido desde el paso 2. Por ejemplo, si un usuario no tiene el permiso &quot;Conjuntos[!UICONTROL de datos de]Vista&quot;, la ficha **[!UICONTROL Conjuntos]** de datos del menú lateral no estará visible para ese usuario.

Para ver los pasos más detallados sobre cómo administrar el control de acceso en [!DNL Experience Platform], consulte la guía [del usuario de](./ui/overview.md)control de acceso.

Todas las llamadas a [!DNL Experience Platform] API se validan para obtener permisos y devuelven errores si no se encuentran los permisos correspondientes en el contexto de usuario actual. Dentro de la interfaz de usuario, los elementos se ocultarán o alterarán según los permisos concedidos al usuario actual.

## Adobe Admin Console

Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso de su organización. A través de la consola, puede otorgar a grupos de usuarios permisos de acceso para diversas [!DNL Platform] funciones, como &quot;[!UICONTROL Administrar conjuntos]de datos&quot;, &quot;Conjuntos de datos de[!UICONTROL Vista]&quot; o &quot;[!UICONTROL Administrar Perfiles]&quot;.

### Perfiles del producto

En la página [!DNL Admin Console], los permisos se asignan a los usuarios mediante el uso de perfiles de producto. Los perfiles de producto le permiten otorgar permisos a uno o varios usuarios, y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante perfiles de producto. Los usuarios pueden asignarse a uno o varios perfiles de productos pertenecientes a su organización.

### Perfiles de producto predeterminados

[!DNL Experience Platform] viene con dos perfiles de producto predeterminados preconfigurados. La siguiente tabla describe lo que se proporciona en cada perfil predeterminado, incluido el simulador para pruebas al que conceden acceso, así como los permisos que conceden dentro del ámbito de ese simulador para pruebas.

| Perfil del producto | Acceso a Simulador para pruebas | Permisos |
| --- | --- | --- |
| Producción predeterminada - Acceso total | Producción | Todos los permisos aplicables a [!DNL Experience Platform], excepto los permisos de administración de Simulador para pruebas. |
| Administración predeterminada de Simulador para pruebas | N/D | Proporciona acceso solamente a los permisos de administración de Simuladores para pruebas. |

## Simuladores y permisos

Los entornos limitados que no son de producción son una forma de virtualización de datos que le permite aislar datos de otros entornos limitados y que generalmente se utilizan para experimentos de desarrollo, pruebas o pruebas. Los permisos de un perfil de productos proporcionan a los usuarios del perfil acceso a [!DNL Platform] las funciones de los entornos de la zona de pruebas a los que se les ha concedido acceso. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados sin producción hasta un máximo de 75 entornos limitados en total. Póngase en contacto con el administrador de la organización IMS o con el representante de ventas de Adobe para obtener más información.

Para obtener más información sobre los entornos limitados de [!DNL Experience Platform], consulte la información general [de los](../sandboxes/home.md)entornos limitados.

### Acceso a los entornos limitados

El acceso a los entornos limitados se administra mediante perfiles de productos. Para ver los pasos detallados sobre cómo habilitar el acceso a un simulador para un perfil de productos, consulte la guía del usuario de [control de acceso](./ui/overview.md).

Se puede otorgar a los usuarios acceso a uno o más entornos limitados dentro de un perfil de producto. Si un usuario está incluido en dos o más perfiles de productos, tendrá acceso a todos los entornos limitados incluidos en esos perfiles.

El permiso &quot;Administración de Simuladores para pruebas&quot; permite a los usuarios administrar, vista o restablecer entornos limitados.

### Permisos

La ficha Permisos de un perfil de producto muestra los entornos limitados y los permisos que están activos para ese perfil:

![permissions-overview](./images/permissions-overview.png)

Los permisos que se conceden a través del [!DNL Admin Console] se ordenan por categoría, y algunos permisos conceden acceso a varias funcionalidades de bajo nivel.

La siguiente tabla describe los permisos disponibles para [!DNL Experience Platform] en la [!DNL Admin Console], con descripciones de las [!DNL Platform] capacidades específicas a las que conceden acceso. Para ver los pasos detallados sobre cómo agregar permisos a un perfil de productos, consulte la guía del usuario de [control de acceso](./ui/overview.md).

| Categoría | Permiso | Descripción |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Administrar esquemas] | Acceso para leer, crear, editar y eliminar esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Esquemas de vistas] | Acceso de sólo lectura a esquemas y recursos relacionados. |
| [!DNL Data Modeling] | [!UICONTROL Administrar relaciones] | Acceso para leer, crear, editar y eliminar relaciones de esquema. |
| [!DNL Data Modeling] | [!UICONTROL Administrar metadatos de identidad] | Acceso para leer, crear, editar y eliminar metadatos de identidad para esquemas. |
| [!DNL Data Management] | [!UICONTROL Administrar conjuntos de datos] | Acceso para leer, crear, editar y eliminar conjuntos de datos. Acceso de solo lectura para esquemas. |
| [!DNL Data Management] | [!UICONTROL Conjuntos de datos de vistas] | Acceso de sólo lectura para conjuntos de datos y esquemas. |
| [!DNL Data Management] | [!UICONTROL Monitoreo de datos] | Acceso de sólo lectura a conjuntos de datos y flujos de monitoreo. |
| [!DNL Profile Management] | [!UICONTROL Administrar Perfiles] | Acceso para leer, crear, editar y eliminar conjuntos de datos que se utilizan para perfiles de clientes. Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Perfiles de vista] | Acceso de solo lectura a perfiles disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar segmentos] | Acceso para leer, crear, editar y eliminar segmentos. |
| [!DNL Profile Management] | [!UICONTROL Segmentos de vista] | Acceso de sólo lectura a segmentos disponibles. |
| [!DNL Profile Management] | [!UICONTROL Administrar directivas de combinación] | Acceso para leer, crear, editar y eliminar directivas de combinación. |
| [!DNL Profile Management] | [!UICONTROL Directivas de combinación de vistas] | Acceso de sólo lectura a directivas de combinación disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportar Audiencia para segmento] | Capacidad para exportar un segmento de audiencia evaluado a un conjunto de datos. |
| [!DNL Profile Management] | [!UICONTROL Evaluar un segmento en una Audiencia] | Capacidad para generar perfiles para una audiencia mediante la evaluación de una definición de segmento. |
| [!DNL Identities] | [!UICONTROL Administrar áreas de nombres de identidad] | Acceso para leer, crear, editar y eliminar Áreas de nombres de identidad. |
| [!DNL Identities] | [!UICONTROL Ver espacios de nombres de identidad] | Acceso de sólo lectura para Áreas de nombres de identidad. |
| [!DNL Sandbox Administration] | [!UICONTROL Administrar Simuladores] | Acceso para leer, crear, editar y eliminar entornos limitados. |
| [!DNL Sandbox Administration] | [!UICONTROL Entornos aislados de vistas] | Acceso de sólo lectura para entornos limitados pertenecientes a su organización. |
| [!DNL Sandbox Administration] | [!UICONTROL Restablecer un Simulador para pruebas] | Capacidad para restablecer un entorno limitado. |
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear, editar y deshabilitar destinos.* |
| [!DNL Destinations] | [!UICONTROL Destinos de vista] | Acceso de sólo lectura a los destinos disponibles en la ficha **[!UICONTROL Catálogo]** y a los destinos autenticados en la ficha **[!UICONTROL Examinar]** .* |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Capacidad para activar datos en destinos activos que se hayan creado. Este permiso requiere que se concedan &quot;Destinos de Vista&quot; o &quot;Administrar [!UICONTROL destinos&quot;] al usuario que activará los destinos.* |
| [!DNL Data Ingestion] | [!UICONTROL Administrar fuentes] | Acceso para leer, crear, editar y deshabilitar fuentes. |
| [!DNL Data Ingestion] | [!UICONTROL Fuentes de vista] | Acceso de sólo lectura a los orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y a los orígenes autenticados en la ficha **[!UICONTROL Examinar]** . |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar área de trabajo de ciencias de datos] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Aplicar etiquetas de uso de datos] | Acceso para leer, crear y eliminar etiquetas de uso. |
| [!DNL Data Governance] | [!UICONTROL Administrar directivas de uso de datos] | Acceso para leer, crear, editar y eliminar directivas de uso de datos. |
| [!DNL Data Governance] | [!UICONTROL Políticas de uso de datos de vista] | Acceso de sólo lectura para directivas de uso de datos pertenecientes a su organización. |
| [!DNL Query Service] | [!UICONTROL Administrar Consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de plataforma. |

_(*) Este permiso requiere disposiciones para [!DNL Real-time Customer Data Platform]. Para obtener más información sobre CDP en tiempo real, lea la información general [de CDP en tiempo](https://docs.adobe.com/content/help/es-ES/experience-platform/rtcdp/overview.html)real._

## Pasos siguientes

Al leer esta guía, usted ha sido presentado a los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar en la guía [del usuario de](./ui/overview.md) control de acceso para ver los pasos detallados sobre cómo utilizar [!DNL Admin Console] para crear perfiles de productos y asignar permisos para [!DNL Platform].