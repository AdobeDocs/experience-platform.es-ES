---
title: Configuración de Edge
seo-title: Configuración de Edge para el SDK web de la plataforma de experiencia
description: 'Obtenga información sobre cómo configurar Experience Platform Edge Network. '
seo-description: 'Obtenga información sobre cómo configurar Experience Platform Edge Network. '
translation-type: tm+mt
source-git-commit: efbc080117754cee01f21c9f9ec409204648e757

---


# Configuración de Edge (Beta)

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La configuración del SDK web de Adobe Experience Platfrom se divide entre dos lugares. El comando [](configuring-the-sdk.md) configure del SDK controla los elementos que deben gestionarse en el cliente, como el `edgeDomain`. La configuración de Edge gestiona el resto de la configuración del SDK. Cuando se envía una solicitud a la red perimetral de la plataforma de experiencia de Adobe, `edgeConfigId` se utiliza para hacer referencia a la configuración del servidor. Esto le permite actualizar la configuración sin tener que realizar cambios de código en el sitio web.

## Creación de un ID de configuración de Edge

Los ID de configuración de Edge se pueden crear en Launch con la herramienta de configuración de Edge. Esta herramienta le permite crear tanto la configuración de borde como entornos dentro de esas configuraciones.

![navegación de la herramienta de configuración de borde](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>La herramienta de configuración de Edge está disponible para los clientes de la lista blanca independientemente de que utilicen Launch como administrador de etiquetas. Además, los usuarios necesitan permisos de desarrollo en Launch. Consulte el artículo Permisos [de](https://docs.adobe.com/content/help/es-ES/launch/using/reference/admin/user-permissions.html) usuario en la documentación de Launch para obtener más información.

Puede crear una configuración de borde haciendo clic en **[UICONTROL Nueva configuración]** de borde en el área superior derecha de la pantalla. Después de proporcionar un nombre y una descripción, se le pedirá la configuración predeterminada para cada entorno.

### Configuración de Entorno predeterminada

Esta configuración predeterminada se utiliza para crear los tres primeros entornos con una configuración idéntica. Estos tres entornos son dev, stage y prod. Coinciden con los tres entornos predeterminados de Launch. Cuando crea una biblioteca de Launch en un entorno dev, la biblioteca utiliza automáticamente el entorno dev de la configuración. Puede editar la configuración de entornos individuales tanto como desee.

El ID utilizado en el SDK `edgeConfigId` es un ID compuesto que especifica la configuración y el entorno. Si no hay entorno, se utiliza el entorno de producción.

### Configuración de Entorno

A continuación se muestran los ajustes disponibles para un entorno. La mayoría de las secciones se pueden habilitar o deshabilitar. Cuando se deshabilita, la configuración se guarda pero no se activa.

#### [!UICONTROL Identity]

La sección de identidad es la única sección que siempre está activada. Tiene dos configuraciones disponibles: Sincronización de ID habilitada e ID de Contenedor de sincronización de ID.

![Sección Identidad de la interfaz de usuario de configuración](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID Sync Enabled]

Controla si el SDK realiza o no sincronizaciones de identidad con socios de terceros.

##### [!UICONTROL ID Sync Container ID]

Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que las distintas sincronizaciones de ID se ejecuten en momentos diferentes. Controla qué contenedor de sincronización de ID se ejecuta para un ID de configuración determinado.

#### Adobe Experience Platform

La configuración que se muestra aquí le permite enviar datos a la plataforma de Adobe Experience. Solo debe activar esta sección si ha adquirido Adobe Experience Platform.

![Bloque de configuración de Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Los Simuladores para pruebas son ubicaciones en la plataforma de Adobe Experience que permiten a los clientes aislar sus datos e implementaciones entre sí. Encontrará más detalles sobre cómo funcionan en la documentación [de](../../sandboxes/home.md)Simuladores para pruebas.

##### [!UICONTROL Streaming Inlet]

Una entrada de flujo continuo es un origen HTTP en Adobe Experience Platform. Se crean en la ficha [!UICONTROL Sources] de Adobe Experience Platform como una API HTTP.

##### [!UICONTROL Event Dataset]

Las configuraciones de Edge admiten el envío de datos a conjuntos de datos que tienen un esquema de clase [!UICONTROL Experience Event].

#### Adobe Target

Para configurar Adobe Destinatario, debe proporcionar un código de cliente. Los demás campos son opcionales.

![Bloque de configuración de Adobe Destinatario](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>La organización asociada con el código de cliente debe coincidir con la organización en la que se crea el ID de configuración.

##### [!UICONTROL Client Code]

ID única de una cuenta de destinatario. Para buscar esto, puede desplazarse a [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] al lado del [!UICONTROL download] botón para [!UICONTROL at.js] o [!UICONTROL mbox.js]

##### [!UICONTROL Property Token]

Destinatario permite a los clientes controlar los permisos mediante el uso de propiedades. Encontrará más información en la sección Permisos [de](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) empresa de la documentación de Destinatario.

El token de propiedad se encuentra en [!UICONTROL Adobe Target] > [!UICONTROL setup] > Propiedades de [UICONTROL]

##### [!UICONTROL Target Environment ID]

[Los Entornos](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) de Adobe Destinatario le ayudan a administrar su implementación en todas las etapas de desarrollo. Esta configuración especifica qué entorno se va a usar con cada entorno.

Adobe recomienda establecer esta configuración de forma diferente para cada uno de sus entornos de configuración `dev`, `stage`y `prod` edge para mantener las cosas simples. Sin embargo, si ya ha [!UICONTROL Adobe Target environments] definido, puede utilizarlos.

#### Adobe Audience Manager

Todo lo que se necesita para enviar datos al Administrador de Audiencias de Adobe es habilitar esta sección. Los demás ajustes son opcionales pero se recomienda.

![Bloque de configuración de Adobe Audiencia Manage](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie Destinations Enabled]

Permite que el SDK comparta información de segmentos a través de [destinos](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de cookies desde el Administrador de Audiencias.

##### [!UICONTROL URL Destinations Enabled]

Permite que el SDK comparta información de segmentos a través de destinos [URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Estos se configuran en el Administrador de Audiencias.

#### Adobe Analytics

Controla si los datos se envían a Adobe Analytics. Encontrará más información en Información general sobre [Analytics](../solution-specific/analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite ID]

El grupo de informes se encuentra en la sección Administración de Adobe Analytics, en [!UICONTROL Admin > ReportSuites]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes.
