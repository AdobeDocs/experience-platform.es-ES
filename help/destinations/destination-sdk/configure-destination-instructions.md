---
description: En esta página se describe cómo utilizar la información de referencia de las opciones de configuración del SDK de destinos para configurar su destino mediante el SDK de destino.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Cómo utilizar el SDK de destino para configurar su destino
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Cómo utilizar el SDK de destino para configurar su destino

## Información general {#overview}

En esta página se describe cómo utilizar la información de referencia de [Configuration options in Destinations SDK](./configuration-options.md) para configurar el destino. Los pasos se muestran en orden secuencial a continuación.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos que se ilustran a continuación, lea la página [Destination SDK getting started](./getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de SDK de destino.

## Pasos para utilizar las opciones de configuración en el SDK de destino para configurar su destino {#steps}

![Pasos ilustrados para utilizar extremos del SDK de destino](./assets/destination-sdk-steps.png)

## Paso 1: Creación de un servidor y una configuración de plantilla {#create-server-template-configuration}

Comience creando un servidor y una configuración de plantilla utilizando el extremo `/destinations-server` (lea [Referencia de API](./destination-server-api.md)). Para obtener más información sobre la configuración del servidor y la plantilla, consulte [Server and template specs](./configuration-options.md#server-and-template) en la sección de referencia.

A continuación se muestra un ejemplo de configuración. Tenga en cuenta que la plantilla de transformación de mensajes del parámetro `requestBody.value` se aborda en el paso 3, [Crear plantilla de transformación](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Paso 2: Crear configuración de destino {#create-destination-configuration}

A continuación se muestra un ejemplo de configuración para una plantilla de destino creada mediante el extremo de API `/destinations` . Para obtener más información sobre esta plantilla, consulte [Configuración de destino](./destination-configuration.md).

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed"
}
```

## Paso 3: Crear plantilla de transformación de mensaje: utilice el lenguaje de plantilla para especificar el formato de salida del mensaje {#create-transformation-template}

En función de las cargas útiles compatibles con el destino, debe crear una plantilla que transforme el formato de los datos exportados desde el formato XDM de Adobe a un formato compatible con el destino. Consulte ejemplos de plantillas en la sección [Uso de un lenguaje de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos](./message-format.md#using-templating) y utilice la [herramienta de creación de plantillas](./create-template.md) proporcionada por el Adobe.

## Paso 4: Crear configuración de metadatos de audiencia {#create-audience-metadata-configuration}

Para algunos destinos, el SDK de destino requiere que configure una plantilla de metadatos de audiencia para crear, actualizar o eliminar audiencias mediante programación en el destino. Consulte [Audience metadata management](./audience-metadata-management.md) para obtener información sobre cuándo debe configurar esta configuración y cómo hacerlo.

## Paso 5: Crear configuración de credenciales / Configurar autenticación {#set-up-authentication}

Dependiendo de si especifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` en la configuración de destino anterior, puede configurar la autenticación para su destino utilizando el extremo `/destination` o `/credentials` .

* **Caso** más común: Si ha seleccionado  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` y su destino admite el método de autenticación OAuth 2, lea la autenticación  [OAuth 2](./oauth2-authentication.md).
* Si seleccionó `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte [Credentials configuration](./credentials-configuration.md) en la documentación de referencia.

## Paso 6: Probar el destino {#test-destination}

Después de configurar el destino utilizando las plantillas de los pasos anteriores, puede utilizar la [herramienta de prueba de destino](./create-template.md) para probar la integración entre Adobe Experience Platform y el destino.

Como parte del proceso para probar el destino, debe utilizar la interfaz de usuario del Experience Platform para crear segmentos, que activará en el destino. Consulte los dos recursos siguientes para obtener instrucciones sobre cómo crear segmentos en Experience Platform:

* [Creación de una página de documentación de segmentos](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Tutorial en vídeo sobre la creación de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Paso 7: Publicar su destino {#publish-destination}

Después de configurar y probar el destino, utilice la [API de publicación de destino](./destination-publish-api.md) para enviar la configuración a Adobe para su revisión.

## Paso 8: Documentar el destino {#document-destination}

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea una [integración productiva](./overview.md#productized-custom-integrations), utilice el [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md) para crear una página de documentación de producto para el destino en el [catálogo de destinos de Experience League](/help/destinations/catalog/overview.md).
