---
title: Creación de una configuración perimetral para el SDK web del Experience Platform
description: 'Aprenda a configurar la red perimetral del Experience Platform. '
keywords: configuración;edge;id de configuración perimetral;Configuración de entorno;edgeConfigId;identidad;sincronización de id habilitada;ID de contenedor de sincronización de ID;Sandbox;entrada de flujo;conjunto de datos de evento;target;código de cliente;token de propiedad;ID de entorno de Target;destinos de cookie;destinos de url;id de grupo de informes del bloque de configuración de Analytics;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
translation-type: tm+mt
source-git-commit: d4ed6c8fa9c86eb2beec829ab24c381b665c2f03
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# Crear una configuración de Edge

La configuración del SDK web de Adobe Experience Platform se divide entre dos lugares. El comando [configure](configuring-the-sdk.md) del SDK controla los elementos que deben manejarse en el cliente, como `edgeDomain`. La configuración perimetral gestiona todas las demás configuraciones para el SDK. Cuando se envía una solicitud a la red perimetral de Adobe Experience Platform, se utiliza la `edgeConfigId` para hacer referencia a la configuración del servidor. Esto le permite actualizar la configuración sin tener que realizar cambios de código en el sitio web.

Su organización debe estar aprovisionada para esta función. Póngase en contacto con el gestor de éxito de los clientes (CSM) para que se le ponga en la lista de permitidos.

## Creación de una configuración de Edge

Las configuraciones de Edge se pueden crear en el Adobe [!DNL Experience Platform Launch] mediante la herramienta de configuración de Edge.

![navegación de la herramienta de configuración de borde](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>La herramienta de configuración perimetral está disponible para los clientes de la lista de permitidos independientemente de si utilizan [!DNL Experience Platform Launch] como administrador de etiquetas. Además, los usuarios requieren permisos de desarrollo en [!DNL Experience Platform Launch]. Consulte el artículo [Permisos de usuario](https://docs.adobe.com/content/help/es-ES/launch/using/reference/admin/user-permissions.html) en la documentación de [!DNL Experience Platform Launch] para obtener más información.

Cree una configuración de Edge haciendo clic en **[!UICONTROL New Edge Configuration]** en el área superior derecha de la pantalla. Después de proporcionar un nombre y una descripción, se le pedirá la configuración predeterminada para cada entorno. A continuación se detalla la configuración disponible.

Al crear una configuración edge, se crean automáticamente tres entornos con configuraciones idénticas. Estos tres entornos son *dev*, *stage* y *prod*. Coinciden con los tres entornos predeterminados en [!DNL Experience Platform Launch]. Cuando crea una biblioteca [!DNL Experience Platform Launch] en un entorno de desarrollo, la biblioteca utiliza automáticamente el entorno de desarrollo a partir de la configuración. Puede editar la configuración en entornos individuales tanto como desee.

El ID utilizado en el SDK como `edgeConfigId` es un ID compuesto que especifica la configuración y el entorno (por ejemplo, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Si no hay ningún entorno presente en el ID compuesto (por ejemplo, `stage` en el ejemplo anterior), se utiliza el entorno de producción.

A continuación encontrará los ajustes disponibles para cada entorno de configuración. La mayoría de las secciones pueden habilitarse o deshabilitarse. Cuando está desactivado, la configuración se guarda, pero no está activa.

## [!UICONTROL Third Party ID] Configuración

La sección ID de terceros es la única sección que siempre está activada. Tiene dos configuraciones disponibles: &quot;[!UICONTROL Third Party ID Sync Enabled]&quot; y &quot;[!UICONTROL Third Party ID Sync Container ID]&quot;.

![Sección Identidad de la interfaz de usuario de configuración](../../assets/edge_configuration_identity.png)

### [!UICONTROL Third Party ID Sync Enabled]

Controla si el SDK realiza o no sincronizaciones de identidad con socios de terceros.

### [!UICONTROL Third Party ID Sync Container ID]

Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que diferentes sincronizaciones de ID se ejecuten en momentos diferentes. Esto controla qué contenedor de sincronizaciones de ID se ejecuta para un ID de configuración determinado.

## Configuración de Adobe Experience Platform

La configuración que se muestra aquí le permite enviar datos a Adobe Experience Platform. Solo debe habilitar esta sección si ha comprado Adobe Experience Platform.

![Bloque de configuración de Adobe Experience Platform](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Los entornos limitados son ubicaciones en Adobe Experience Platform que permiten a los clientes aislar entre sí sus datos e implementaciones. Para obtener más información sobre cómo funcionan, consulte la [Documentación de entornos limitados](../../sandboxes/home.md).

### [!UICONTROL Streaming Inlet]

Una entrada de flujo continuo es una fuente HTTP en Adobe Experience Platform. Se crean en la pestaña &quot;[!UICONTROL Sources]&quot; de Adobe Experience Platform as a HTTP API.

### [!UICONTROL Event Dataset]

Las configuraciones de Edge admiten el envío de datos a conjuntos de datos que tienen un esquema de clase [!UICONTROL Experience Event].

## Configuración de Adobe Target

Para configurar Adobe Target, debe proporcionar un código de cliente. Los demás campos son opcionales.

![Bloque de configuración de Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>La organización asociada con el código de cliente debe coincidir con la organización en la que se creó el ID de configuración.

### [!UICONTROL Client Code]

ID exclusivo de una cuenta de destino. Para encontrar esto, puede navegar a [!UICONTROL Adobe Target] > [!UICONTROL Setup] [!UICONTROL Implementation] > [!UICONTROL edit settings] junto al botón [!UICONTROL download] para [!UICONTROL at.js] o [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] permite a los clientes controlar los permisos mediante el uso de propiedades. Puede encontrar más información en la sección [Permisos de Enterprise](https://docs.adobe.com/content/help/es-ES/target/using/administer/manage-users/enterprise/properties-overview.html) de la documentación de [!DNL Target].

El token de propiedad se puede encontrar en [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Los entornos de Adobe Target le ayudan a administrar su implementación en todas las etapas de desarrollo. Esta configuración especifica qué entorno se va a utilizar con cada entorno.

Adobe recomienda configurarlo de forma diferente para cada uno de los entornos de configuración de Edge `dev`, `stage` y `prod` para mantener las cosas simples. Sin embargo, si ya tiene definidos entornos de Adobe Target, puede utilizarlos.

## Configuración de Adobe Audience Manager

Todo lo que se necesita para enviar datos a Adobe Audience Manager es habilitar esta sección. Los demás ajustes son opcionales, pero se recomienda.

![Bloque de configuración de Audience Manager de Adobe](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Permite al SDK compartir información de segmentos a través de [Cookie Destinations](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) desde [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Permite que el SDK comparta información de segmentos a través de [Destinos de URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Estos se configuran en [!DNL Audience Manager].

## Configuración de Adobe Analytics

Controla si los datos se envían a Adobe Analytics. Encontrará más información en la [Información general de Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

El grupo de informes se encuentra en la sección Administración de Adobe Analytics, en [!UICONTROL Admin > ReportSuites]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes.
