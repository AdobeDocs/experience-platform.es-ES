---
description: En esta página se muestran y describen los pasos para configurar un destino de flujo continuo mediante Destination SDK.
title: Usar Destination SDK para configurar un destino de flujo continuo
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Usar Destination SDK para configurar un destino de flujo continuo

## Información general {#overview}

Esta página describe cómo utilizar la información de [Opciones de configuración en el SDK de destinos](../functionality/configuration-options.md) y en otros documentos de referencia de la API y la funcionalidad de Destination SDK para configurar un [destino de streaming](../../destination-types.md#streaming-destinations). Los pasos se presentan en orden secuencial a continuación.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos que se ilustran a continuación, lea la [Introducción al Destination SDK](../getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK. Esto supone que ha completado la asociación y los requisitos previos de permisos y está listo para empezar a desarrollar su destino.

## Pasos para utilizar las opciones de configuración de Destination SDK para configurar el destino {#steps}

![Pasos ilustrados del uso de extremos de Destination SDK](../assets/guides/destination-sdk-steps.png)

## Paso 1: Crear una configuración de servidor y plantilla {#create-server-template-configuration}

Comenzar por [creación de una configuración de servidor y plantilla](../authoring-api/destination-server/create-destination-server.md) uso del `/destinations-server` punto final.

A continuación se muestra un ejemplo de configuración. Tenga en cuenta que la plantilla de transformación de mensajes de la variable `requestBody.value` parámetro se aborda en el paso 3, [Crear plantilla de transformación](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
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

## Paso 2: Crear la configuración de destino {#create-destination-configuration}

A continuación se muestra un ejemplo de configuración para una plantilla de destino creada con la variable `/destinations` Extremo de API. Consulte [crear una configuración de destino](../authoring-api/destination-configuration/create-destination-configuration.md) para obtener más información.

Para conectar el servidor y la configuración de plantilla del paso 1 a esta configuración de destino, agregue el ID de instancia del servidor y la configuración de plantilla como `destinationServerId` aquí.

>[!IMPORTANT]
>
>Para crear un destino en tiempo real (flujo) correctamente configurado, debe *debe* añada al menos una identidad de destino en `identityNamespaces`, como se muestra a continuación. Si no se configura ninguna identidad de destino, los usuarios no podrán continuar más allá de [Paso de asignación](../../ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## Paso 3: Crear una plantilla de transformación de mensaje: utilice el lenguaje de plantilla para especificar el formato de salida del mensaje {#create-transformation-template}

En función de las cargas útiles que admite su destino, debe crear una plantilla que transforme el formato de los datos exportados del formato XDM de Adobe a un formato compatible con su destino. Consulte los ejemplos de plantilla en la sección [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a audiencias](../functionality/destination-server/message-format.md#using-templating) y utilice el [herramienta de creación de plantillas](../testing-api/streaming-destinations/create-template.md) proporcionadas por el Adobe.

Una vez que haya creado una plantilla de transformación de mensajes que le funcione, agréguela al servidor y a la configuración de plantilla que creó en el paso 1.

```json {line-numbers="true" highlight="13-14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Paso 4: Crear la configuración de metadatos de audiencia {#create-audience-metadata-configuration}

Para algunos destinos, Destination SDK requiere que configure los metadatos de audiencia para crear, actualizar o eliminar audiencias en el destino mediante programación. Consulte [Gestión de metadatos de audiencia](../functionality/audience-metadata-management.md) para obtener información sobre cuándo debe configurar esta configuración y cómo hacerlo.

Si utiliza una configuración de metadatos de audiencia, debe conectarla a la configuración de destino creada en el paso 2. Añada el ID de instancia de la configuración de metadatos de audiencia a la configuración de destino como `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```


## Paso 5: Configuración de la autenticación {#set-up-authentication}

En función de si especifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` en la configuración de destino anterior, puede configurar la autenticación para su destino mediante el `/destination` o el `/credentials` punto final.

Si ha seleccionado `"authenticationRule": "CUSTOMER_AUTHENTICATION"` en la configuración de destino y el destino admite el método de autenticación OAuth 2, lea lo siguiente [Autenticación OAuth 2](../functionality/destination-configuration/oauth2-authentication.md).

Si ha seleccionado `"authenticationRule": "PLATFORM_AUTHENTICATION"`, debe crear un [configuración de credenciales](../credentials-api/create-credential-configuration.md).

## Paso 6: Prueba del destino {#test-destination}

Después de configurar el destino mediante los extremos de configuración de los pasos anteriores, puede utilizar el [herramienta de prueba de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) para probar la integración entre Adobe Experience Platform y el destino.

Como parte del proceso para probar el destino, debe utilizar la interfaz de usuario de Experience Platform para crear segmentos que activará en el destino. Consulte los dos recursos siguientes para obtener instrucciones sobre cómo crear audiencias en Experience Platform:

* [Creación de una página de documentación de audiencia](/help/segmentation/ui/overview.md#create-segment)
* [Tutorial de Creación de un vídeo de audiencia](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Paso 7: Publicar el destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar y probar el destino, utilice el [API de publicación de destino](../publishing-api/create-publishing-request.md) para enviar la configuración al Adobe para su revisión.

## Paso 8: Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o integrador de sistemas (SI) que crea un [integración de productos](../overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](../docs-framework/documentation-instructions.md) para crear una página de documentación del producto para el destino en [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md).

## Paso 9: Enviar destino para su revisión por parte del Adobe {#submit-for-review}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Por último, para que el destino se pueda publicar en el catálogo de Experience Platform y sea visible para todos los clientes de Experience Platform, debe enviar oficialmente el destino para que el Adobe lo revise. Encuentre información completa acerca de cómo [enviar para su revisión un destino de productos creado en Destination SDK](../guides/submit-destination.md).
