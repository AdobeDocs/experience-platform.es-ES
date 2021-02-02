---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
topic: overview
title: Control de acceso general
description: Control de acceso para Adobe Experience Platform se proporciona a través de Adobe Admin Console. Esta funcionalidad aprovecha los perfiles del producto en el Admin Console, que vinculan a los usuarios con permisos y entornos limitados.
translation-type: tm+mt
source-git-commit: c277caabe851c81f66b822c07a25f4b94466eef0
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 2%

---


# Control de acceso general

El control de acceso para [!DNL Experience Platform] se proporciona a través de [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en [!DNL Admin Console], que vinculan a los usuarios con permisos y entornos limitados.

## Jerarquía de controles de acceso y flujo de trabajo

Para configurar control de acceso para [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga una [!DNL Experience Platform] integración de producto. La función mínima que otorga o retira permisos es un administrador de perfil de productos. Otras funciones de administrador que pueden administrar permisos son los administradores de productos (pueden administrar todos los perfiles de un producto) y los administradores de sistemas (sin restricciones). Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

>[!NOTE]
>
>A partir de este momento, cualquier mención de &quot;administrador&quot; en este documento se refiere a un administrador de perfiles de productos o a una versión posterior (como se describe anteriormente).

Un flujo de trabajo de alto nivel para obtener y asignar permisos de acceso se puede resumir de la siguiente manera:

- Después de otorgar licencias a Adobe Experience Platform o a un servicio de aplicaciones/aplicaciones que utiliza Experience Platform, se envía un correo electrónico al administrador especificado durante la licencia.
- El administrador inicia sesión en [Adobe Admin Console](#adobe-admin-console) y selecciona **Adobe Experience Platform** de la lista de productos en la página de información general.
- El administrador puede realizar la vista de los [perfiles de productos](#product-profiles) predeterminados o crear nuevos perfiles de productos de clientes según sea necesario.
- El administrador puede editar los permisos y usuarios de cualquier perfil de producto existente.
- Al crear o editar un perfil de producto, el administrador agrega usuarios al perfil mediante la ficha **[!UICONTROL usuarios]** y concede permisos a estos usuarios (como &quot;[!UICONTROL Leer conjuntos de datos]&quot; o &quot;[!UICONTROL Administrar Esquemas]&quot;) accediendo a la ficha **[!UICONTROL permisos]**. Del mismo modo, el administrador puede asignar acceso a los entornos limitados mediante la misma ficha de permisos.
- Cuando los usuarios inician sesión en la interfaz de usuario [!DNL Experience Platform], su acceso a las capacidades [!DNL Platform] depende de los permisos que se les han concedido desde el Paso 2. Por ejemplo, si un usuario no tiene el permiso &quot;[!UICONTROL Conjuntos de datos de Vista]&quot;, la ficha **[!UICONTROL Conjuntos de datos]** del menú lateral no estará visible para ese usuario.

Para ver los pasos más detallados sobre cómo administrar el control de acceso en [!DNL Experience Platform], consulte la [guía del usuario de control de acceso](./ui/overview.md).

Todas las llamadas a [!DNL Experience Platform] API se validan para obtener permisos y devolverán errores si no se encuentran los permisos adecuados en el contexto de usuario actual. Dentro de la interfaz de usuario, los elementos se ocultarán o alterarán según los permisos concedidos al usuario actual.

## Adobe Admin Console

Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso de su organización. A través de la consola, puede otorgar a grupos de usuarios permisos de acceso para diversas funciones [!DNL Platform], como &quot;[!UICONTROL Administrar conjuntos de datos]&quot;, &quot;[!UICONTROL conjuntos de datos de Vista]&quot; o &quot;[!UICONTROL Administrar Perfiles]&quot;.

### Perfiles del producto

En [!DNL Admin Console], los permisos se asignan a los usuarios mediante el uso de perfiles de productos. Los perfiles de producto le permiten otorgar permisos a uno o varios usuarios, y también contienen su acceso al ámbito de los entornos limitados que se les asignan mediante perfiles de producto. Los usuarios pueden asignarse a uno o varios perfiles de productos pertenecientes a su organización.

### Perfiles de producto predeterminados

[!DNL Experience Platform] viene con dos perfiles de producto predeterminados preconfigurados. La siguiente tabla describe lo que se proporciona en cada perfil predeterminado, incluido el simulador para pruebas al que conceden acceso, así como los permisos que conceden dentro del ámbito de ese simulador para pruebas.

| Perfil del producto | Acceso a Simulador para pruebas | Permisos |
| --- | --- | --- |
| Acceso total a producción predeterminada | Producción | Todos los permisos aplicables a [!DNL Experience Platform], excepto los permisos de administración de Simulador para pruebas. |
| Administradores de Simuladores para pruebas | N/D | Proporciona acceso solamente a los permisos de administración de Simuladores para pruebas. |

## Simuladores y permisos

Los entornos limitados que no son de producción son una forma de virtualización de datos que le permite aislar datos de otros entornos limitados y que generalmente se utilizan para experimentos de desarrollo, pruebas o pruebas. Los permisos de un perfil de producto proporcionan a los usuarios del perfil acceso a [!DNL Platform] funciones dentro de los entornos de simulación de pruebas a los que se les ha concedido acceso. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados sin producción hasta un máximo de 75 entornos limitados en total. Póngase en contacto con el administrador de la organización IMS o con el representante de ventas de Adobe para obtener más información.

Para obtener más información acerca de los entornos limitados en [!DNL Experience Platform], consulte la [información general de los entornos limitados](../sandboxes/home.md).

### Acceso a los entornos limitados

El acceso a los entornos limitados se administra mediante perfiles de productos. Para ver los pasos detallados sobre cómo habilitar el acceso a un simulador para un perfil de productos, consulte la [guía del usuario de control de acceso](./ui/overview.md).

Se puede otorgar a los usuarios acceso a uno o más entornos limitados dentro de un perfil de producto. Si un usuario está incluido en dos o más perfiles de productos, tendrá acceso a todos los entornos limitados incluidos en esos perfiles.

El permiso &quot;Administración de Simuladores para pruebas&quot; permite a los usuarios administrar, vista o restablecer entornos limitados.

### Permisos

La ficha Permisos de un perfil de producto muestra los entornos limitados y los permisos que están activos para ese perfil:

![permissions-overview](./images/permissions-overview.png)

Los permisos concedidos mediante [!DNL Admin Console] se ordenan por categoría, y algunos permisos conceden acceso a varias funcionalidades de bajo nivel.

La siguiente tabla describe los permisos disponibles para [!DNL Experience Platform] en [!DNL Admin Console], con descripciones de las capacidades específicas a las que conceden acceso. [!DNL Platform] Para ver los pasos detallados sobre cómo agregar permisos a un perfil de productos, consulte la [guía del usuario de control de acceso](./ui/overview.md).

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
| [!DNL Destinations] | [!UICONTROL Administrar destinos] | Acceso para leer, crear, editar y deshabilitar destinos. |
| [!DNL Destinations] | [!UICONTROL Destinos de vista] | Acceso de sólo lectura a destinos disponibles en la ficha **[!UICONTROL Catálogo]** y destinos autenticados en la ficha **[!UICONTROL Examinar]**. |
| [!DNL Destinations] | [!UICONTROL Activar destinos] | Capacidad para activar datos en destinos activos que se hayan creado. Este permiso requiere que &quot;Destinos de Vista&quot; o &quot;Administrar [!UICONTROL Destinos&quot;] se concedan al usuario que activará los destinos. |
| [!DNL Data Ingestion] | [!UICONTROL Administrar fuentes] | Acceso para leer, crear, editar y deshabilitar fuentes. |
| [!DNL Data Ingestion] | [!UICONTROL Fuentes de vista] | Acceso de sólo lectura a orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y orígenes autenticados en la ficha **[!UICONTROL Examinar]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Administrar área de trabajo de ciencias de datos] | Acceso para leer, crear, editar y eliminar en [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Aplicar etiquetas de uso de datos] | Acceso para leer, crear y eliminar etiquetas de uso. |
| [!DNL Data Governance] | [!UICONTROL Administrar directivas de uso de datos] | Acceso para leer, crear, editar y eliminar directivas de uso de datos. |
| [!DNL Data Governance] | [!UICONTROL Políticas de uso de datos de vista] | Acceso de sólo lectura para directivas de uso de datos pertenecientes a su organización. |
| [!DNL Query Service] | [!UICONTROL Administrar Consultas] | Acceso para leer, crear, editar y eliminar consultas SQL estructuradas para datos de plataforma. |

## Pasos siguientes

Al leer esta guía, usted ha sido presentado a los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar con la [guía del usuario de control de acceso](./ui/overview.md) para obtener pasos detallados sobre cómo utilizar [!DNL Admin Console] para crear perfiles de productos y asignar permisos para [!DNL Platform].