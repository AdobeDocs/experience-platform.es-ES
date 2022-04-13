---
keywords: personalización personalizada; destino; destino personalizado de experience platform;
title: Conexión personalizada personalizada
description: Este destino proporciona personalización externa, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en el sitio para recuperar información de segmentos de Adobe Experience Platform. Este destino proporciona personalización en tiempo real basada en la pertenencia a segmentos de perfil de usuario.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: c83c7e2a74a6bf4a7a4c9c04ccebfd0296c89bce
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 1%

---

# Conexión personalizada personalizada {#custom-personalization-connection}

## Información general {#overview}

Este destino proporciona una forma de recuperar información de segmentos de Adobe Experience Platform a plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en sitios web de clientes.

## Requisitos previos {#prerequisites}

Esta integración cuenta con la tecnología [SDK web de Adobe Experience Platform](../../../edge/home.md) o [SDK de Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/). Debe utilizar uno de estos SDK para utilizar este destino.

>[!IMPORTANT]
>
>Antes de crear una conexión de personalización personalizada, lea la guía sobre cómo [configurar destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform.

## Export type and frequency {#export-type-frequency}

**Solicitud de perfil** : está solicitando todos los segmentos asignados en el destino de personalización personalizado para un solo perfil. Different custom personalization destinations can be set up for different [Adobe Data Collection datastreams](../../../edge/fundamentals/datastreams.md).

## Casos de uso {#use-cases}

La variable [!DNL Custom personalization connection] permite utilizar sus propias plataformas de socios de personalización (por ejemplo, [!DNL Optimizely], [!DNL Pega]), mientras que también aprovecha las capacidades de recopilación y segmentación de datos de Experience Platform Edge Network para ofrecer una experiencia de personalización más profunda para los clientes.

Los casos de uso que se describen a continuación incluyen tanto la personalización del sitio como la publicidad dirigida en el sitio.

To enable these use cases, customers need a quick, streamlined way of retrieving segment information from Experience Platform and sending this information to their designated systems that they configured as custom personalization connections in the Experience Platform UI.

Estos sistemas pueden ser plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en las propiedades web y móviles de los clientes.

### Personalización de la misma página {#same-page}

Un usuario visita una página del sitio web. El cliente puede utilizar la información de visita a la página actual (por ejemplo, la dirección URL de referencia, el idioma del explorador o la información del producto incrustada) para seleccionar la siguiente acción o decisión (por ejemplo, personalización), mediante la conexión de personalización personalizada para plataformas que no sean de Adobe (por ejemplo, [!DNL Pega], [!DNL Optimizely], etc.).

### Personalización de página siguiente {#next-page}

Un usuario visita la Página A de su sitio web. En función de esta interacción, el usuario cumple los requisitos para un conjunto de segmentos. A continuación, el usuario hace clic en un vínculo que los lleva de la página A a la página B. Los segmentos para los que el usuario había cumplido los requisitos durante la interacción anterior en la página A, junto con las actualizaciones de perfil determinadas por la visita actual al sitio web, se utilizarán para activar la siguiente acción o decisión (por ejemplo, qué banner publicitario se mostrará al visitante o, en el caso de pruebas A/B, qué versión de la página se mostrará).

### Personalización de próxima sesión {#next-session}

Un usuario visita varias páginas del sitio web. En función de estas interacciones, el usuario cumple los requisitos para un conjunto de segmentos. A continuación, el usuario finaliza la sesión de navegación actual.

Al día siguiente, el usuario vuelve al mismo sitio web del cliente. The segments they had qualified for during the previous interaction with all the visited website pages, together with the profile updates determined by the current website visit, will be used to select the next action / decision (for example, which advertising banner to display to the visitor, or, in case of A/B testing, which version of the page to display).

## Conectarse al destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Acerca de los ID de conjunto de datos"
>abstract="Esta opción determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Debe configurar un conjunto de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Obtenga información sobre cómo configurar un conjunto de datos"

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Connection parameters {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
* **[!UICONTROL Alias de integración]**: Este valor se envía al SDK web del Experience Platform como nombre de objeto JSON.
* **[!UICONTROL Datastream ID]**: This determines in which Data Collection datastream the segments will be included in the response to the page. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Consulte [Configuración de un conjunto de datos](../../../edge/fundamentals/datastreams.md) para obtener más información.

## Activar segmentos en este destino {#activate}

Lectura [Activar perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Si está utilizando [Etiquetas en Adobe Experience Platform](../../../tags/home.md) para implementar el SDK web de Experience Platform, utilice el [enviar evento finalizado](../../../edge/extension/event-types.md) y su acción de Custom Code tendrá una `event.destinations` que puede utilizar para ver los datos exportados.

Here is a sample value for the `event.destinations` variable:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

If you are not using [Tags](../../../tags/home.md) to deploy the Experience Platform Web SDK, use the [handling responses from events](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) functionality to see the exported data.

The JSON response from Adobe Experience Platform can be parsed to find the corresponding integration alias of the application you are integrating with Adobe Experience Platform. The segment IDs can be passed into the application&#39;s code as targeting parameters. A continuación se muestra un ejemplo de cómo se vería esto específico para la respuesta de destino.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Data usage and governance {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. For detailed information on how [!DNL Adobe Experience Platform] enforces data governance, read the [Data Governance overview](../../../data-governance/home.md).
