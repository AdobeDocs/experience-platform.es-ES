---
title: Configurar el almacén de datos para el SDK web del Experience Platform
description: 'Aprenda a configurar los flujos de datos. '
keywords: configuración;datastreams;datastreamId;edge;id de datastream;Configuración de entorno;edgeConfigId;id;sincronización de id habilitada;ID de contenedor de sincronización de ID;Sandbox;entrada de flujo;conjunto de datos de evento;target;código de cliente;token de propiedad;ID de entorno de Target;destinos de cookies;destinos de url;id de grupo de informes de bloqueo de configuración de Analytics;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: d326267cacf8d678937e8c959de8acbfbbb88c93
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 2%

---


# Configurar un conjunto de datos

La configuración del SDK web de Adobe Experience Platform se divide entre dos lugares. La variable [configurar, comando](configuring-the-sdk.md) en el SDK controla los elementos que se deben gestionar en el cliente, como el `edgeDomain`. Los Datastreams administran todas las demás configuraciones para el SDK. Cuando se envía una solicitud a la red perimetral de Adobe Experience Platform, la variable `edgeConfigId` se utiliza para hacer referencia a la configuración del lado del servidor. Esto le permite actualizar la configuración sin tener que realizar cambios de código en el sitio web.

Su organización debe estar aprovisionada para esta función. Póngase en contacto con el gestor de éxito de los clientes (CSM) para que se le ponga en la lista de permitidos.

## Crear una configuración de conjunto de datos

Puede crear y administrar conjuntos de datos en la interfaz de usuario de recopilación de datos seleccionando **[!UICONTROL Datastreams]** en el panel de navegación izquierdo.

![navegación de la herramienta datastreams](../images/datastreams/config.png)

>[!NOTE]
>
>Mientras que puede acceder a la [!UICONTROL Datastreams] independientemente de si utiliza las funcionalidades de administración de etiquetas de Platform, debe tener permisos de desarrollador para administrar los propios conjuntos de datos. Consulte la [permisos de usuario](../../tags/ui/administration/user-permissions.md) en la documentación de etiquetas para obtener más información.

Cree un conjunto de datos haciendo clic en **[!UICONTROL Nuevo conjunto de datos]** en el área superior derecha de la pantalla. Después de proporcionar un nombre y una descripción, se le pedirá la configuración predeterminada para cada entorno. A continuación se detalla la configuración disponible.

Al crear un conjunto de datos, se crean automáticamente tres entornos con una configuración idéntica. Estos tres entornos son *dev*, *fase* y *prod*. Coinciden con los tres entornos predeterminados para las etiquetas. Cuando crea una biblioteca de etiquetas en un entorno de desarrollo, la biblioteca utiliza automáticamente el entorno de desarrollo de la configuración. Puede editar la configuración en entornos individuales tanto como desee.

El ID utilizado en el SDK como la variable `edgeConfigId` es un ID compuesto que especifica la configuración y el entorno (por ejemplo, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Si no hay ningún entorno presente en el ID compuesto (por ejemplo, `stage` en el ejemplo anterior), se utiliza el entorno de producción.

A continuación se muestran los ajustes disponibles para cada entorno de configuración. La mayoría de las secciones pueden habilitarse o deshabilitarse. Cuando está desactivado, la configuración se guarda, pero no está activa.

## [!UICONTROL ID de terceros] configuración

La sección ID de terceros es la única sección que siempre está activada. Tiene dos configuraciones disponibles: &quot;[!UICONTROL Sincronización de ID de terceros habilitada]&quot; y &quot;[!UICONTROL ID de contenedor de sincronización de ID de terceros]&quot;.

![Sección Identidad de la interfaz de usuario de configuración](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Sincronización de ID de terceros habilitada]

Controla si el SDK realiza o no sincronizaciones de identidad con socios de terceros.

### [!UICONTROL ID de contenedor de sincronización de ID de terceros]

Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que diferentes sincronizaciones de ID se ejecuten en momentos diferentes. Esto controla qué contenedor de sincronizaciones de ID se ejecuta para un ID de configuración determinado.

## Configuración de Adobe Experience Platform

La configuración que se muestra aquí le permite enviar datos a Adobe Experience Platform. Solo debe habilitar esta sección si ha comprado Adobe Experience Platform.

![Bloque de configuración de Adobe Experience Platform](../images/datastreams/platform-config.png)

| Campo | Descripción |
| --- | --- |
| [!UICONTROL Entorno de pruebas] | **(Obligatorio)** Seleccione el entorno limitado de Platform al que desee enviar los datos. Los entornos limitados son particiones virtuales en Adobe Experience Platform que le permiten aislar los datos y las implementaciones de otras personas de su organización.<br><br>Si crea un conjunto de datos sin seleccionar un simulador de pruebas, podrá seleccionar un simulador de pruebas más adelante.<br><br>Una vez creado un conjunto de datos y seleccionado un simulador para pruebas, el simulador de pruebas no se puede cambiar. La variable [!UICONTROL Sandbox] por lo tanto, el campo de selección no está disponible al editar un conjunto de datos existente con un entorno limitado seleccionado.<br><br> La variable [!UICONTROL Sandbox] por lo tanto, el campo de selección no está disponible al editar un conjunto de datos existente.<br><br>Para obtener más información sobre la función de los entornos limitados en el Experience Platform, consulte la [documentación de entornos limitados](../../sandboxes/home.md). |
| [!UICONTROL Conjunto de datos del evento] | **(Obligatorio)** Seleccione el conjunto de datos de Platform al que se transmitirán los datos de eventos del cliente. Este esquema debe utilizar la variable [Clase XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Conjunto de datos de perfil] | Seleccione el conjunto de datos de Platform al que se enviarán los datos de atributos del cliente. Este esquema debe utilizar la variable [Clase de perfil individual XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Seleccione esta casilla de verificación para habilitar el Offer decisioning para una implementación del SDK web de Platform. Consulte la guía de [uso del Offer decisioning con el SDK web de Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) para obtener más información sobre la implementación. Para obtener más información sobre las funciones de Offer decisioning, consulte la [Documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=es). |
| [!UICONTROL Segmentación de Edge] | Active esta casilla de verificación para habilitar [segmentación de arista](../../segmentation/ui/edge-segmentation.md) para este conjunto de datos. Cuando el SDK web de Platform envía datos a través de un conjunto de datos habilitado para la segmentación perimetral, cualquier pertenencia de segmento actualizada para el perfil en cuestión se devuelve en la respuesta.<br><br>Esta opción se puede utilizar en combinación con [!UICONTROL Destinos de personalización] para [casos de uso de personalización de páginas siguientes](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinos de personalización] | Cuando se utiliza en combinación con la variable [!UICONTROL Segmentación de Edge] , esta opción permite que el conjunto de datos se conecte a motores de personalización como Adobe Target. Consulte la documentación de destinos para ver los pasos específicos sobre [configuración de destinos de personalización](../../destinations/ui/configure-personalization-destinations.md). |

## Configuración de Adobe Target

Para configurar Adobe Target, debe proporcionar un código de cliente. Los demás campos son opcionales.

![Bloque de configuración de Adobe Target](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>La organización asociada con el código de cliente debe coincidir con la organización en la que se creó el ID de configuración.

### [!UICONTROL Código de cliente]

ID exclusivo de una cuenta de destino. Para encontrarlo, puede navegar hasta [!UICONTROL Adobe Target] > [!UICONTROL Configuración]> [!UICONTROL Implementación] > [!UICONTROL editar configuración] junto a la variable [!UICONTROL descargar] para [!UICONTROL at.js] o [!UICONTROL mbox.js]

### [!UICONTROL Token de propiedad]

[!DNL Target] permite a los clientes controlar los permisos mediante el uso de propiedades. Los detalles se encuentran en la [Permisos de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=es) de la sección [!DNL Target] documentación.

El token de propiedad se puede encontrar en [!UICONTROL Adobe Target] > [!UICONTROL configuración] > [!UICONTROL Propiedades]

### [!UICONTROL ID de entorno de Target]

[Entornos](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) en Adobe Target, le ayuda a administrar su implementación en todas las etapas de desarrollo. Esta configuración especifica qué entorno se va a utilizar con cada entorno.

Adobe recomienda configurar esto de forma diferente para cada uno de los `dev`, `stage`y `prod` entornos de datastream para mantener las cosas simples. Sin embargo, si ya tiene definidos entornos de Adobe Target, puede utilizarlos.

## Configuración de Adobe Audience Manager

Todo lo que se necesita para enviar datos a Adobe Audience Manager es habilitar esta sección. Los demás ajustes son opcionales, pero se recomienda.

![Bloque de configuración de Audience Manager de Adobe](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Destinos de cookies habilitados]

Permite al SDK compartir información de segmentos mediante [Destinos de cookies](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) from [!DNL Audience Manager].

### [!UICONTROL Destinos de URL habilitados]

Permite al SDK compartir información de segmentos mediante [Destinos de URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Estos se configuran en [!DNL Audience Manager].

## Configuración de Adobe Analytics

Controla si los datos se envían a Adobe Analytics. Los detalles adicionales se encuentran en la [Información general de Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL ID del grupo de informes]

El grupo de informes se encuentra en la sección Administración de Adobe Analytics, en [!UICONTROL Administración > Grupos de informes]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes.
