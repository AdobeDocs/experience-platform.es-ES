---
title: Configurar el almacén de datos para el SDK web del Experience Platform
description: 'Aprenda a configurar los flujos de datos. '
keywords: configuración;datastreams;datastreamId;edge;id de configuración perimetral;Configuración de entorno;edgeConfigId;id;sincronización de id habilitada;ID de contenedor de sincronización de ID;Sandbox;entrada de flujo;conjunto de datos de evento;target;código de cliente;token de propiedad;ID de entorno de Target;destinos de cookies;destinos de url;id de grupo de informes de bloqueo de configuración de Analytics;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---


# Configuración de un conjunto de datos

La configuración del SDK web de Adobe Experience Platform se divide entre dos lugares. El comando [configure](configuring-the-sdk.md) del SDK controla los elementos que deben manejarse en el cliente, como `edgeDomain`. Los Datastreams administran todas las demás configuraciones para el SDK. Cuando se envía una solicitud a la red perimetral de Adobe Experience Platform, se utiliza la `edgeConfigId` para hacer referencia a la configuración del servidor. Esto le permite actualizar la configuración sin tener que realizar cambios de código en el sitio web.

Su organización debe estar aprovisionada para esta función. Póngase en contacto con el gestor de éxito de los clientes (CSM) para que se le ponga en la lista de permitidos.

## Creación de una configuración de almacén de datos

Los Datastreams se pueden crear en el Adobe [!DNL Experience Platform Launch] mediante la herramienta de configuración Datastream.

![navegación de la herramienta datastreams](../../assets/datastreams_config.png)

>[!NOTE]
>
>La herramienta de configuración de conjuntos de datos está disponible para los clientes de la lista de permitidos independientemente de si utilizan [!DNL Experience Platform Launch] como administrador de etiquetas. Además, los usuarios requieren permisos de desarrollo en [!DNL Experience Platform Launch]. Consulte el artículo [Permisos de usuario](../../tags/ui/administration/user-permissions.md) en la documentación de [!DNL Experience Platform Launch] para obtener más información.

Cree un conjunto de datos haciendo clic en **[!UICONTROL Nuevo conjunto de datos]** en el área superior derecha de la pantalla. Después de proporcionar un nombre y una descripción, se le pedirá la configuración predeterminada para cada entorno. A continuación se detalla la configuración disponible.

Al crear un conjunto de datos, se crean automáticamente tres entornos con una configuración idéntica. Estos tres entornos son *dev*, *stage* y *prod*. Coinciden con los tres entornos predeterminados en [!DNL Experience Platform Launch]. Cuando crea una biblioteca [!DNL Experience Platform Launch] en un entorno de desarrollo, la biblioteca utiliza automáticamente el entorno de desarrollo a partir de la configuración. Puede editar la configuración en entornos individuales tanto como desee.

El ID utilizado en el SDK como `edgeConfigId` es un ID compuesto que especifica la configuración y el entorno (por ejemplo, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Si no hay ningún entorno presente en el ID compuesto (por ejemplo, `stage` en el ejemplo anterior), se utiliza el entorno de producción.

A continuación se muestran los ajustes disponibles para cada entorno de configuración. La mayoría de las secciones pueden habilitarse o deshabilitarse. Cuando está desactivado, la configuración se guarda, pero no está activa.

## [!UICONTROL Configuración de ] ID de terceros

La sección ID de terceros es la única sección que siempre está activada. Tiene dos configuraciones disponibles: &quot;[!UICONTROL Sincronización de ID de terceros habilitada]&quot; y &quot;[!UICONTROL ID de contenedor de sincronización de ID de terceros]&quot;.

![Sección Identidad de la interfaz de usuario de configuración](../../assets/edge_configuration_identity.png)

### [!UICONTROL Sincronización de ID de terceros habilitada]

Controla si el SDK realiza o no sincronizaciones de identidad con socios de terceros.

### [!UICONTROL ID de contenedor de sincronización de ID de terceros]

Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que diferentes sincronizaciones de ID se ejecuten en momentos diferentes. Esto controla qué contenedor de sincronizaciones de ID se ejecuta para un ID de configuración determinado.

## Configuración de Adobe Experience Platform

La configuración que se muestra aquí le permite enviar datos a Adobe Experience Platform. Solo debe habilitar esta sección si ha comprado Adobe Experience Platform.

![Bloque de configuración de Adobe Experience Platform](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Los entornos limitados son ubicaciones en Adobe Experience Platform que permiten a los clientes aislar entre sí sus datos e implementaciones. Para obtener más información sobre cómo funcionan, consulte la [Documentación de entornos limitados](../../sandboxes/home.md).

### [!UICONTROL Entrada de flujo continuo]

Una entrada de flujo continuo es una fuente HTTP en Adobe Experience Platform. Se crean en la pestaña &quot;[!UICONTROL Sources]&quot; de Adobe Experience Platform as a HTTP API.

### [!UICONTROL Conjunto de datos del evento]

Los conjuntos de datos admiten el envío de datos a conjuntos de datos que tienen un esquema de clase [!UICONTROL Experience Event].

## Configuración de Adobe Target

Para configurar Adobe Target, debe proporcionar un código de cliente. Los demás campos son opcionales.

![Bloque de configuración de Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>La organización asociada con el código de cliente debe coincidir con la organización en la que se creó el ID de configuración.

### [!UICONTROL Código de cliente]

ID exclusivo de una cuenta de destino. Para encontrar esto, puede navegar a [!UICONTROL Adobe Target] > [!UICONTROL Configuración] [!UICONTROL Implementación] > [!UICONTROL editar configuración] junto al botón [!UICONTROL descargar] para [!UICONTROL at.js] o [!UICONTROL mbox.js]

### [!UICONTROL Token de propiedad]

[!DNL Target] permite a los clientes controlar los permisos mediante el uso de propiedades. Puede encontrar más información en la sección [Permisos de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=es) de la documentación de [!DNL Target].

El token de propiedad se puede encontrar en [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL ID de entorno de Target]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Los entornos de Adobe Target le ayudan a administrar su implementación en todas las etapas de desarrollo. Esta configuración especifica qué entorno se va a utilizar con cada entorno.

Adobe recomienda configurarlo de forma diferente para cada uno de los entornos del conjunto de datos `dev`, `stage` y `prod` para mantener las cosas simples. Sin embargo, si ya tiene definidos entornos de Adobe Target, puede utilizarlos.

## Configuración de Adobe Audience Manager

Todo lo que se necesita para enviar datos a Adobe Audience Manager es habilitar esta sección. Los demás ajustes son opcionales, pero se recomienda.

![Bloque de configuración de Audience Manager de Adobe](../../assets/edge_configuration_aam.png)

### [!UICONTROL Destinos de cookies habilitados]

Permite al SDK compartir información de segmentos a través de [Cookie Destinations](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) desde [!DNL Audience Manager].

### [!UICONTROL Destinos de URL habilitados]

Permite que el SDK comparta información de segmentos a través de [Destinos de URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Estos se configuran en [!DNL Audience Manager].

## Configuración de Adobe Analytics

Controla si los datos se envían a Adobe Analytics. Encontrará más información en la [Información general de Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](../../assets/edge_configuration_aa.png)

### [!UICONTROL ID del grupo de informes]

El grupo de informes se encuentra en la sección Administración de Adobe Analytics en [!UICONTROL Administración > Grupos de informes]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes.
