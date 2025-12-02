---
keywords: personalización personalizada; destino; destino personalizado de experience platform;
title: Conexión de personalización personalizada
description: Este destino proporciona personalización externa, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en el sitio para recuperar información de audiencia de Adobe Experience Platform. Este destino proporciona personalización en tiempo real basada en la pertenencia a audiencias de perfil de usuario.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: d252fc30d93fa4440c6ef47146830d0423e1839a
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 9%

---


# Conexión de personalización personalizada {#custom-personalization-connection}

## Registro de cambios de destino {#changelog}

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Mayo de 2023 | Actualización de funcionalidad y documentación | A partir de mayo de 2023, la conexión **[!UICONTROL Custom personalization]** admite la [personalización basada en atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) y está disponible para todos los clientes. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, debe usar la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/) al configurar el destino **[!UICONTROL Custom Personalization]** para la personalización basada en atributos. Todas las llamadas a la API de Edge Network deben realizarse en un [contexto autenticado](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication).
>
><br>Puede recuperar atributos de perfil a través de la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/) agregando una integración del lado del servidor que utiliza la misma secuencia de datos que ya está utilizando para su implementación de SDK web o móvil.
>
><br>Si no cumple los requisitos anteriores, la personalización se basará únicamente en el abono a audiencias.

## Información general {#overview}

Configure este destino para permitir que las plataformas de personalización externas, los sistemas de administración de contenido, los servidores de publicidad y otras aplicaciones que se ejecutan en los sitios web de los clientes recuperen la información de audiencia de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Este destino requiere el uso de uno de los siguientes métodos de recopilación de datos, según la implementación:

* Use [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) si desea recopilar datos de su sitio web.
* Use [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) si desea recopilar datos de su aplicación móvil.
* Utilice la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/) si no utiliza Web SDK o Mobile SDK, o si desea personalizar la experiencia del usuario en función de los atributos del perfil.

>[!IMPORTANT]
>
>**Requisitos de personalización basados en atributos:** Si desea realizar personalizaciones basadas en atributos de perfil (no solo en la pertenencia a audiencias), **debe** utilizar la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/) con integración autenticada del lado del servidor, independientemente de si también utiliza Web SDK o Mobile SDK para la recopilación de datos.
>
>Web SDK y Mobile SDK solo admiten la personalización basada en la pertenencia a audiencias. La API de Edge Network es **necesaria** para recuperar de forma segura los atributos de perfil para la personalización.

>[!IMPORTANT]
>
>Antes de crear una conexión de personalización personalizada, lee la guía sobre cómo [activar datos de audiencia en destinos de personalización Edge](../../ui/activate-edge-personalization-destinations.md). Esta guía le explica los pasos de configuración necesarios para los casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!DNL Profile request]** | Está solicitando todas las audiencias asignadas en el destino de personalización personalizado para un solo perfil. Se pueden configurar diferentes destinos de personalización personalizados para diferentes [flujos de datos de recopilación de datos de Adobe](../../../datastreams/overview.md). |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Conectar con el destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Acerca de las secuencias de datos"
>abstract="Esta opción determina en qué secuencia de datos de recopilación de datos se incluirán los públicos en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Debe configurar una secuencia de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=es" text="Obtenga información sobre cómo configurar una secuencia de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Name]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Description]**: escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
* **[!UICONTROL Integration alias]**: este valor se envía a Experience Platform Web SDK como nombre de objeto JSON.
* **[!UICONTROL Datastream]**: esto determina en qué secuencia de datos de recopilación de datos se incluirán las audiencias en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Consulte [Configuración de una secuencia de datos](../../../datastreams/overview.md) para obtener más información.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea [Activar perfiles y audiencias para destinos personalizados Edge](../../ui/activate-edge-personalization-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados {#exported-data}

Si usa [etiquetas en Adobe Experience Platform](/help/tags/home.md) para implementar Experience Platform Web SDK, use la funcionalidad [enviar evento completado](/help/tags/extensions/client/web-sdk/event-types.md) y la acción de código personalizado tendrá una variable `event.destinations` que puede usar para ver los datos exportados.

Este es un valor de muestra para la variable `event.destinations`:

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

Si no usa [Tags](/help/tags/home.md) para implementar Experience Platform Web SDK, use [respuestas de comandos](/help/collection/js/commands/command-responses.md) para ver los datos exportados.

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

### Respuesta de ejemplo para [!UICONTROL Custom Personalization With Attributes]

Al usar **[!UICONTROL Custom Personalization With Attributes]**, la respuesta de la API será similar al ejemplo siguiente.

La diferencia entre **[!UICONTROL Custom Personalization With Attributes]** y **[!UICONTROL Custom Personalization]** es la inclusión de la sección `attributes` en la respuesta de la API.

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

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](../../../data-governance/home.md).
