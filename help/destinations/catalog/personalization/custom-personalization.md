---
keywords: personalización personalizada; destino; destino personalizado de experience platform;
title: Conexión personalizada personalizada
description: Este destino proporciona personalización externa, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en el sitio para recuperar información de segmentos de Adobe Experience Platform. Este destino proporciona personalización en tiempo real basada en la pertenencia a segmentos de perfil de usuario.
hide: true
hidefromtoc: true
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 7ac7f533bb8547865b53892d371059aa60d2232e
workflow-type: tm+mt
source-wordcount: '973'
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

## Tipo de exportación y frecuencia {#export-type-frequency}

**Solicitud de perfil** : está solicitando todos los segmentos asignados en el destino de personalización personalizado para un solo perfil. Se pueden configurar diferentes destinos de personalización personalizados para diferentes [Almacenes de datos de recopilación de datos de Adobe](../../../edge/datastreams/overview.md).

## Casos de uso {#use-cases}

La variable [!DNL Custom personalization connection] permite utilizar sus propias plataformas de socios de personalización (por ejemplo, [!DNL Optimizely], [!DNL Pega]), mientras que también aprovecha las capacidades de recopilación y segmentación de datos de Experience Platform Edge Network para ofrecer una experiencia de personalización más profunda para los clientes.

Los casos de uso que se describen a continuación incluyen tanto la personalización del sitio como la publicidad dirigida en el sitio.

Para habilitar estos casos de uso, los clientes necesitan una forma rápida y optimizada de recuperar la información del segmento de Experience Platform y enviar esta información a los sistemas designados que configuraron como conexiones de personalización personalizadas en la interfaz de usuario del Experience Platform.

Estos sistemas pueden ser plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en las propiedades web y móviles de los clientes.

### Personalización de la misma página {#same-page}

Un usuario visita una página del sitio web. El cliente puede utilizar la información de visita a la página actual (por ejemplo, la dirección URL de referencia, el idioma del explorador o la información del producto incrustada) para seleccionar la siguiente acción o decisión (por ejemplo, personalización), mediante la conexión de personalización personalizada para plataformas que no sean de Adobe (por ejemplo, [!DNL Pega], [!DNL Optimizely], etc.).

### Personalización de página siguiente {#next-page}

Un usuario visita la Página A de su sitio web. En función de esta interacción, el usuario cumple los requisitos para un conjunto de segmentos. A continuación, el usuario hace clic en un vínculo que los lleva de la página A a la página B. Los segmentos para los que el usuario había cumplido los requisitos durante la interacción anterior en la página A, junto con las actualizaciones de perfil determinadas por la visita actual al sitio web, se utilizarán para activar la siguiente acción o decisión (por ejemplo, qué banner publicitario se mostrará al visitante o, en el caso de pruebas A/B, qué versión de la página se mostrará).

### Personalización de próxima sesión {#next-session}

Un usuario visita varias páginas del sitio web. En función de estas interacciones, el usuario cumple los requisitos para un conjunto de segmentos. A continuación, el usuario finaliza la sesión de navegación actual.

Al día siguiente, el usuario vuelve al mismo sitio web del cliente. Los segmentos para los que se habían clasificado durante la interacción anterior con todas las páginas del sitio web visitadas, junto con las actualizaciones de perfil determinadas por la visita del sitio web actual, se utilizarán para seleccionar la siguiente acción o decisión (por ejemplo, para qué banner publicitario se mostrará al visitante o, en el caso de pruebas A/B, qué versión de la página mostrar).

## Conectarse al destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Acerca de los ID de conjunto de datos"
>abstract="Esta opción determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Debe configurar un conjunto de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Obtenga información sobre cómo configurar un conjunto de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
* **[!UICONTROL Alias de integración]**: Este valor se envía al SDK web del Experience Platform como nombre de objeto JSON.
* **[!UICONTROL ID de almacén de datos]**: Esto determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Consulte [Configuración de un conjunto de datos](../../../edge/datastreams/overview.md) para obtener más información.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

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
