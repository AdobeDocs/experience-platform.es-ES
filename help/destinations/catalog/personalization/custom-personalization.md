---
keywords: personalización personalizada; destino; destino personalizado de experience platform;
title: Conexión personalizada personalizada
description: Este destino proporciona personalización externa, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en el sitio para recuperar información de segmentos de Adobe Experience Platform. Este destino proporciona personalización en tiempo real basada en la pertenencia a segmentos de perfil de usuario.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: ee9ed1c17a566f37b4ad79df7c66f8b2ffb4b879
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---

# Conexión personalizada personalizada {#custom-personalization-connection}

## Información general {#overview}

Este destino proporciona una forma de recuperar información de segmentos de Adobe Experience Platform a plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en sitios web de clientes.

## Requisitos previos {#prerequisites}

Esta integración cuenta con la tecnología [SDK web de Adobe Experience Platform](../../../edge/home.md) o [SDK de Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/). Debe utilizar uno de estos SDK para utilizar este destino.

## Tipo de exportación {#export-type}

**Solicitud de perfil** : está solicitando todos los segmentos asignados en el destino de personalización personalizado para un solo perfil. Se pueden configurar diferentes destinos de personalización personalizados para diferentes [Almacenes de datos de recopilación de datos de Adobe](../../../edge/fundamentals/datastreams.md).

## Casos de uso {#use-cases}

Este destino comparte audiencias con servidores de publicidad y aplicaciones de personalización que no son de Adobe, que se utilizarán en tiempo real para decidir qué usuarios de publicidad deben ver en un sitio web.

### Caso de uso n.º 1

**Personalización de una página de inicio**

Un sitio web de ventas y alquiler de casa quiere personalizar su página de inicio en función de las cualificaciones de los segmentos en Adobe Experience Platform. La empresa puede seleccionar qué audiencias deben obtener una experiencia personalizada y asignarlas al destino de personalización personalizado que se ha configurado para su aplicación de personalización que no es de Adobe como criterios de objetivo.

**Publicidad en el sitio dirigida**

Con un destino personalizado independiente para su servidor de publicidad, el mismo sitio web puede dirigirse a la publicidad en el sitio con un conjunto diferente de segmentos de Adobe Experience Platform como criterios de objetivo.

## Conectarse al destino {#connect}

>[!IMPORTANT]
>
>Antes de crear una conexión de personalización personalizada, le recomendamos que lea nuestra guía sobre cómo [configurar destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform.

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Acerca de los ID de conjunto de datos"
>abstract="Esta opción determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Debe configurar un conjunto de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Aprenda a configurar un conjunto de datos."

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
* **[!UICONTROL Alias de integración]**: Este valor se envía al SDK web del Experience Platform como nombre de objeto JSON.
* **[!UICONTROL ID de almacén de datos]**: Esto determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Consulte [Configuración de un conjunto de datos](../../../edge/fundamentals/datastreams.md) para obtener más información.

## Activar segmentos en este destino {#activate}

Lectura [Activar perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Si está utilizando [Etiquetas en Adobe Experience Platform](../../../tags/home.md) para implementar el SDK web de Experience Platform, utilice el [enviar evento finalizado](../../../edge/extension/event-types.md) y su acción de Custom Code tendrá una `event.destinations` que puede utilizar para ver los datos exportados.

Este es un valor de muestra para la variable `event.destinations` variable:

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

Si no usa [Etiquetas](../../../tags/home.md) para implementar el SDK web de Experience Platform, utilice el [gestión de respuestas de eventos](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) para ver los datos exportados.

La respuesta JSON de Adobe Experience Platform se puede analizar para encontrar el alias de integración correspondiente de la aplicación que está integrando con Adobe Experience Platform. Los ID de segmento se pueden pasar al código de la aplicación como parámetros de objetivo. A continuación se muestra un ejemplo de cómo se vería esto específico para la respuesta de destino.

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


## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](../../../data-governance/home.md).
