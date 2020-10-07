---
title: Configuración de Edge
seo-title: Configuración de Edge para el SDK web Experience Platform
description: 'Obtenga información sobre cómo configurar la red perimetral Experience Platform. '
seo-description: 'Obtenga información sobre cómo configurar la red perimetral Experience Platform. '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---


# Configuración del borde

La configuración del Adobe Experience Platform [!DNL Web SDK] se divide entre dos lugares. El comando [](configuring-the-sdk.md) configure del SDK controla los elementos que deben gestionarse en el cliente, como el `edgeDomain`. La configuración de Edge gestiona el resto de la configuración del SDK. Cuando se envía una solicitud al Adobe Experience Platform [!DNL Edge Network], `edgeConfigId` se utiliza para hacer referencia a la configuración del lado del servidor. Esto le permite actualizar la configuración sin tener que realizar cambios de código en el sitio web.

## Creación de un ID de configuración de Edge

Los ID de configuración de Edge se pueden crear en Adobe [!DNL Launch] con la herramienta de configuración de Edge. Esta herramienta le permite crear tanto la configuración de borde como entornos dentro de esas configuraciones.

![navegación de la herramienta de configuración de borde](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>La herramienta de configuración de Edge está disponible para los clientes de la lista de permitidos, independientemente de si utilizan [!DNL Launch] como administrador de etiquetas. Además, los usuarios necesitan permisos de desarrollo en [!DNL Launch]. Consulte el artículo Permisos [de](https://docs.adobe.com/content/help/es-ES/launch/using/reference/admin/user-permissions.html) usuario en la [!DNL Launch] documentación para obtener más información.

Puede crear una configuración de borde haciendo clic en **[!UICONTROL Nueva configuración]** de borde en el área superior derecha de la pantalla. Después de proporcionar un nombre y una descripción, se le pedirá la configuración predeterminada para cada entorno.

### Configuración de Entorno predeterminada

Esta configuración predeterminada se utiliza para crear los tres primeros entornos con una configuración idéntica. Estos tres entornos son *dev*, *stage* y *prod*. Coinciden con los tres entornos predeterminados de [!DNL Launch]. Cuando crea una [!DNL Launch] biblioteca en un entorno dev, la biblioteca utiliza automáticamente el entorno dev de la configuración. Puede editar la configuración de entornos individuales tanto como desee.

El ID utilizado en el SDK `edgeConfigId` es un ID compuesto que especifica la configuración y el entorno. Si no hay entorno, se utiliza el entorno de producción.

### Configuración de entorno

A continuación se muestran los ajustes disponibles para un entorno. La mayoría de las secciones se pueden habilitar o deshabilitar. Cuando se deshabilita, la configuración se guarda pero no se activa.

#### [!UICONTROL Identidad]

La sección de identidad es la única sección que siempre está activada. Tiene dos configuraciones disponibles: &quot;Sincronizaciones[!UICONTROL de ID habilitadas]&quot; e &quot;ID de Contenedor[!UICONTROL de sincronización de]ID&quot;.

![Sección Identidad de la interfaz de usuario de configuración](../../assets/edge_configuration_identity.png)

##### [!UICONTROL Sincronización de ID habilitada]

Controla si el SDK realiza o no sincronizaciones de identidad con socios de terceros.

##### [!UICONTROL ID de Contenedor de sincronización de ID]

Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que las distintas sincronizaciones de ID se ejecuten en momentos diferentes. Controla qué contenedor de sincronización de ID se ejecuta para un ID de configuración determinado.

#### Adobe Experience Platform

La configuración que se muestra aquí le permite enviar datos al Adobe Experience Platform. Solo debe habilitar esta sección si ha adquirido el Adobe Experience Platform.

![Bloque de configuración de Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Simulador para pruebas]

Los Simuladores para pruebas son ubicaciones del Adobe Experience Platform que permiten a los clientes aislar sus datos e implementaciones entre sí. Para obtener más información sobre cómo funcionan, consulte la documentación [de los](../../sandboxes/home.md)Simuladores para pruebas.

##### [!UICONTROL Entrada de flujo continuo]

Una entrada de flujo continuo es un origen HTTP en el Adobe Experience Platform. Se crean en la ficha &quot;[!UICONTROL Fuentes]&quot; de Adobe Experience Platform como una API HTTP.

##### [!UICONTROL Conjunto de datos de evento]

Las configuraciones de Edge admiten el envío de datos a conjuntos de datos que tienen un esquema de clase [!UICONTROL Experience Evento].

#### Adobe Target

Para configurar Adobe Target, debe proporcionar un código de cliente. Los demás campos son opcionales.

![Bloque de configuración de Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>La organización asociada con el código de cliente debe coincidir con la organización en la que se crea el ID de configuración.

##### [!UICONTROL Código de cliente]

ID única de una cuenta de destinatario. Para encontrarlo, puede navegar a [!UICONTROL Adobe Target] > [!UICONTROL Configuración]> [!UICONTROL Implementación] > [!UICONTROL editar la configuración] al lado del botón de [!UICONTROL descarga]  [!UICONTROL para at.js o para mbox.js]

##### [!UICONTROL Token de propiedad]

[!DNL Target] permite a los clientes controlar los permisos mediante el uso de propiedades. Encontrará más información en la sección Permisos [de](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) Enterprise de la [!DNL Target] documentación.

El token de propiedad se encuentra en [!UICONTROL Adobe Target] > [!UICONTROL Configuración] > [!UICONTROL Propiedades]

##### [!UICONTROL ID de Entorno de destinatario]

[Los entornos](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) de Adobe Target le ayudan a administrar su implementación en todas las etapas de desarrollo. Esta configuración especifica qué entorno se va a usar con cada entorno.

Adobe recomienda que esto se establezca de forma diferente para cada uno de los entornos de configuración `dev`, `stage`y `prod` borde para que las cosas sean sencillas. Sin embargo, si ya tiene definidos entornos de Adobe Target, puede utilizarlos.

#### Adobe Audience Manager

Todo lo que se necesita para enviar datos a Adobe Audience Manager es habilitar esta sección. Los demás ajustes son opcionales pero se recomienda.

![Audiencia de Adobe Administrar bloqueo de configuración](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Destinos de cookies habilitados]

Permite que el SDK comparta información de segmentos mediante [destinos](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de cookies desde [!DNL Audience Manager].

##### [!UICONTROL Destinos de URL habilitados]

Permite que el SDK comparta información de segmentos a través de destinos [URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Estos se configuran en [!DNL Audience Manager].

#### Adobe Analytics

Controla si los datos se envían a Adobe Analytics. Encontrará más información en Información general sobre [Analytics](../solution-specific/analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](../../assets/edge_configuration_aa.png)

##### [!UICONTROL ID del grupo de informes]

El grupo de informes se encuentra en la sección Administración de Adobe Analytics, en [!UICONTROL Administración > Grupos de informes]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes.
