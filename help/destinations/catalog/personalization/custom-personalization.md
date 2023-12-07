---
keywords: personalización personalizada; destino; destino personalizado de experience platform;
title: Conexión de personalización personalizada
description: Este destino proporciona personalización externa, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en el sitio para recuperar información de audiencia de Adobe Experience Platform. Este destino proporciona personalización en tiempo real basada en la pertenencia a audiencias de perfil de usuario.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 10%

---


# Conexión de personalización personalizada {#custom-personalization-connection}

## Registro de cambios de destino {#changelog}

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Mayo de 2023 | Actualización de funcionalidad y documentación | A partir de mayo de 2023, la **[!UICONTROL Personalización personalizada]** compatibilidad de conexión [personalización basada en atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) y está disponible para todos los clientes. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, debe utilizar la variable [API del servidor de red perimetral](/help/server-api/overview.md) al configurar el **[!UICONTROL Personalización personalizada]** destino para la personalización basada en atributos. Todas las llamadas a la API de servidor deben realizarse en un [contexto autenticado](../../../server-api/authentication.md).
>
><br>Si ya utiliza el SDK web o el SDK móvil para la integración, puede recuperar atributos mediante la API del servidor añadiendo una integración del lado del servidor.
>
><br>Si no cumple los requisitos anteriores, la personalización se basará únicamente en el abono a audiencia.

## Información general {#overview}

Configure este destino para permitir que las plataformas de personalización externas, los sistemas de administración de contenido, los servidores de publicidad y otras aplicaciones que se ejecutan en los sitios web de los clientes recuperen la información de audiencia de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Esta integración funciona con el [SDK web de Adobe Experience Platform](../../../edge/home.md) o el [SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/). Debe utilizar uno de estos SDK para utilizar este destino.

>[!IMPORTANT]
>
>Antes de crear una conexión de personalización personalizada, lea la guía sobre cómo [activar datos de audiencia en destinos de personalización de edge](../../ui/activate-edge-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para los casos de uso de personalización de la misma página y de la página siguiente, en varios componentes de Experience Platform.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!DNL Profile request]** | Está solicitando todas las audiencias asignadas en el destino de personalización personalizado para un solo perfil. Se pueden configurar diferentes destinos de personalización personalizados para diferentes [Adobe de flujos de datos de recopilación](../../../datastreams/overview.md). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Conexión al destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Acerca de los ID de secuencia de datos"
>abstract="Esta opción determina en qué secuencia de datos de recopilación de datos se incluirán los públicos en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Debe configurar una secuencia de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=es" text="Obtenga información sobre cómo configurar una secuencia de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
* **[!UICONTROL Alias de integración]**: este valor se envía al SDK web de Experience Platform como nombre de objeto JSON.
* **[!UICONTROL ID de flujo de datos]**: Determina en qué flujo de datos de recopilación de datos se incluirán las audiencias en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Consulte [Configuración de una secuencia de datos](../../../datastreams/overview.md) para obtener más información.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y audiencias en destinos de personalización de Edge](../../ui/activate-edge-personalization-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados {#exported-data}

Si está utilizando [Etiquetas en Adobe Experience Platform](../../../tags/home.md) para implementar el SDK web de Experience Platform, utilice el [enviar evento completado](../../../tags/extensions/client/web-sdk/event-types.md) y la acción de Custom Code tendrá un `event.destinations` que puede utilizar para ver los datos exportados.

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

La respuesta JSON de Adobe Experience Platform se puede analizar para encontrar el alias de integración correspondiente de la aplicación que está integrando con Adobe Experience Platform. Los ID de audiencia se pueden pasar al código de la aplicación como parámetros de segmentación. A continuación se muestra un ejemplo de cómo sería esto específico de la respuesta de destino.

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
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
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
