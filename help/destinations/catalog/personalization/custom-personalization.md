---
keywords: personalización personalizada; destino; destino personalizado de experience platform;
title: Conexión de personalización personalizada
description: Este destino proporciona personalización externa, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en el sitio para recuperar información de segmentos de Adobe Experience Platform. Este destino proporciona personalización en tiempo real en función del abono a segmentos del perfil del usuario.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# Conexión de personalización personalizada {#custom-personalization-connection}

## Registro de cambios de destino {#changelog}

Con la versión beta del **[!UICONTROL Personalización personalizada]** conector de destino, podría estar viendo dos **[!UICONTROL Personalización personalizada]** tarjetas en el catálogo de destinos.

El **[!UICONTROL Personalización personalizada con atributos]** El conector de está actualmente en versión beta y solo está disponible para un número selecto de clientes. Además de la funcionalidad proporcionada por **[!UICONTROL Personalización personalizada]**, el **[!UICONTROL Personalización personalizada con atributos]** El conector añade un [paso de asignación](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) al flujo de trabajo de activación, que le permite asignar atributos de perfil a su destino de personalización personalizado, lo que permite la personalización de la misma página y de la página siguiente basada en atributos.

>[!IMPORTANT]
>
>Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, la variable **[!UICONTROL Personalización personalizada con atributos]** El destino requiere que utilice el [API del servidor de red perimetral](/help/server-api/overview.md) para la recopilación de datos. Además, todas las llamadas a la API de servidor deben realizarse en un [contexto autenticado](../../../server-api/authentication.md).
>
>Si ya utiliza el SDK web o el SDK móvil para la integración, puede recuperar atributos mediante la API de servidor de dos formas:
>
> * Añada una integración del lado del servidor que recupere atributos a través de la API del servidor.
> * Actualice la configuración del lado del cliente con un código Javascript personalizado para recuperar atributos mediante la API del servidor.
>
> Si no cumple los requisitos anteriores, la personalización se basará únicamente en la pertenencia a segmentos, idéntica a la experiencia ofrecida por el **[!UICONTROL Personalización personalizada]** conector.

![Imagen de las dos tarjetas de destino de personalización personalizadas en una vista en paralelo.](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## Información general {#overview}

Este destino proporciona una forma de recuperar información de segmentos de Adobe Experience Platform para plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en los sitios web de los clientes.

## Requisitos previos {#prerequisites}

Esta integración funciona con el [SDK web de Adobe Experience Platform](../../../edge/home.md) o el [SDK de Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/). Debe utilizar uno de estos SDK para utilizar este destino.

>[!IMPORTANT]
>
>Antes de crear una conexión de personalización personalizada, lea la guía sobre cómo [configuración de destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para los casos de uso de personalización de la misma página y de la página siguiente, en varios componentes de Experience Platform.

## Tipo y frecuencia de exportación {#export-type-frequency}

**Solicitud de perfil** : está solicitando todos los segmentos asignados en el destino de personalización personalizado para un solo perfil. Se pueden configurar diferentes destinos de personalización personalizados para diferentes [Adobe de flujos de datos de recopilación](../../../edge/datastreams/overview.md).

## Casos de uso {#use-cases}

El [!DNL Custom Personalization Connection] le permite utilizar sus propias plataformas de socios de personalización (por ejemplo, [!DNL Optimizely], [!DNL Pega]), así como sistemas propietarios (por ejemplo, CMS interno), a la vez que aprovecha las capacidades de segmentación y recopilación de datos de Experience Platform Edge Network para impulsar una experiencia de personalización más profunda para los clientes.

Los casos de uso que se describen a continuación incluyen personalización del sitio y publicidad en el sitio segmentada.

Para habilitar estos casos de uso, los clientes necesitan una forma rápida y optimizada de recuperar la información de segmentos de Experience Platform y enviarla a sus sistemas designados que configuraron como conexiones de personalización personalizadas en la interfaz de usuario de Experience Platform.

Estos sistemas pueden ser plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecuten en las propiedades web y móviles de los clientes.

### Personalización de la misma página {#same-page}

Un usuario visita una página del sitio web. El cliente puede utilizar la información de visita de la página actual (por ejemplo, la dirección URL de referencia, el idioma del explorador, la información de producto incrustada) para seleccionar la siguiente acción/decisión (por ejemplo, personalización), utilizando la conexión de personalización personalizada para plataformas que no sean de Adobe (por ejemplo, [!DNL Pega], [!DNL Optimizely], etc.).

### Personalización de la página siguiente {#next-page}

Un usuario visita la página A del sitio web. En función de esta interacción, el usuario cumple los requisitos para un conjunto de segmentos. A continuación, el usuario hace clic en un vínculo que le lleva de la página A a la B. Los segmentos para los que el usuario estaba cualificado durante la interacción anterior en la página A, junto con las actualizaciones de perfil determinadas por la visita actual al sitio web, se utilizan para activar la siguiente acción/decisión (por ejemplo, qué banner publicitario mostrar al visitante o, en el caso de las pruebas A/B, qué versión de la página mostrar).

### Personalización de próxima sesión {#next-session}

Un usuario visita varias páginas del sitio web. En función de estas interacciones, el usuario cumple los requisitos para un conjunto de segmentos. A continuación, el usuario finaliza la sesión de exploración actual.

Al día siguiente, el usuario vuelve al mismo sitio web del cliente. Los segmentos para los que se habían clasificado durante la interacción anterior con todas las páginas del sitio web visitado, junto con las actualizaciones de perfil determinadas por la visita del sitio web actual, se utilizan para seleccionar la siguiente acción/decisión (por ejemplo, qué titular de publicidad mostrar al visitante o, en el caso de las pruebas A/B, qué versión de la página mostrar).

## Conectar con el destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Acerca de los ID de secuencia de datos"
>abstract="Esta opción determina en qué secuencia de datos de recopilación de datos se incluirán los segmentos en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Debe configurar una secuencia de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es" text="Obtenga información sobre cómo configurar una secuencia de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
* **[!UICONTROL Alias de integración]**: este valor se envía al SDK web de Experience Platform como nombre de objeto JSON.
* **[!UICONTROL ID de flujo de datos]**: Determina en qué flujo de datos de recopilación de datos se incluirán los segmentos en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Consulte [Configuración de una secuencia de datos](../../../edge/datastreams/overview.md) para obtener más información.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Si está utilizando [Etiquetas en Adobe Experience Platform](../../../tags/home.md) para implementar el SDK web de Experience Platform, utilice el [enviar evento completado](../../../edge/extension/event-types.md) y la acción de Custom Code tendrá un `event.destinations` que puede utilizar para ver los datos exportados.

Este es un valor de muestra para `event.destinations` variable:

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

Si no está utilizando [Etiquetas](../../../tags/home.md) para implementar el SDK web de Experience Platform, utilice el [gestión de respuestas de eventos](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) para ver los datos exportados.

La respuesta JSON de Adobe Experience Platform se puede analizar para encontrar el alias de integración correspondiente de la aplicación que está integrando con Adobe Experience Platform. Los ID de segmento se pueden pasar al código de la aplicación como parámetros de segmentación. A continuación se muestra un ejemplo de cómo sería esto específico de la respuesta de destino.

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Respuesta de ejemplo para [!UICONTROL Personalización personalizada con atributos]

Al utilizar **[!UICONTROL Personalización personalizada con atributos]** Sin embargo, la respuesta de la API tendrá un aspecto similar al ejemplo siguiente.

La diferencia entre **[!UICONTROL Personalización personalizada con atributos]** y **[!UICONTROL Personalización personalizada]** es la inclusión de `attributes` de la respuesta de la API.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](../../../data-governance/home.md).
