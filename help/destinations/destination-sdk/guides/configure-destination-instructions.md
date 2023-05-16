---
description: En esta página se enumeran y describen los pasos para configurar un destino de flujo continuo mediante el Destination SDK .
title: Usar Destination SDK para configurar un destino de flujo continuo
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Usar Destination SDK para configurar un destino de flujo continuo

## Información general {#overview}

Esta página describe cómo utilizar la información de [Opciones de configuración en el SDK de Destinations](../functionality/configuration-options.md) y en otros documentos de referencia de API y funcionalidad de Destination SDK para configurar un [destino de flujo continuo](../../destination-types.md#streaming-destinations). Los pasos se muestran en orden secuencial a continuación.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos que se ilustran a continuación, lea la [introducción al Destination SDK](../getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK. Esto supone que ha completado los requisitos previos de asociación y permisos y está listo para empezar a desarrollar su destino.

## Pasos para utilizar las opciones de configuración en Destination SDK para configurar el destino {#steps}

![Pasos ilustrados para utilizar extremos de Destination SDK](../assets/guides/destination-sdk-steps.png)

## Paso 1: Creación de un servidor y una configuración de plantilla {#create-server-template-configuration}

Comience por [creación de un servidor y una configuración de plantilla](../authoring-api/destination-server/create-destination-server.md) usando la variable `/destinations-server` punto final.

A continuación se muestra un ejemplo de configuración. Tenga en cuenta que la plantilla de transformación de mensajes de la sección `requestBody.value` se aborda en el paso 3, [Crear plantilla de transformación](#create-transformation-template).

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

## Paso 2: Crear configuración de destino {#create-destination-configuration}

A continuación se muestra un ejemplo de configuración para una plantilla de destino creada mediante el uso de la variable `/destinations` extremo de API. Consulte [crear una configuración de destino](../authoring-api/destination-configuration/create-destination-configuration.md) para obtener más información.

Para conectar el servidor y la configuración de plantilla en el paso 1 a esta configuración de destino, añada el ID de instancia del servidor y la configuración de plantilla como `destinationServerId` aquí.

>[!IMPORTANT]
>
>Para crear un destino configurado correctamente en tiempo real (flujo continuo), debe *must* agregar al menos una identidad de destino en `identityNamespaces`, como se muestra a continuación. Si no se configura ninguna identidad de destino, los usuarios no podrán continuar más allá del [Paso de asignación](../../ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación.

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

## Paso 3: Crear plantilla de transformación de mensaje: utilice el lenguaje de plantilla para especificar el formato de salida del mensaje {#create-transformation-template}

En función de las cargas útiles compatibles con el destino, debe crear una plantilla que transforme el formato de los datos exportados desde el formato XDM de Adobe a un formato compatible con el destino. Consulte ejemplos de plantillas en la sección [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos](../functionality/destination-server/message-format.md#using-templating) y utilice el [herramienta de creación de plantillas](../testing-api/streaming-destinations/create-template.md) proporcionado por Adobe.

Una vez que haya creado una plantilla de transformación de mensaje que funcione para usted, agréguela a la configuración de servidor y plantilla que ha creado en el paso 1.

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

## Paso 4: Crear configuración de metadatos de audiencia {#create-audience-metadata-configuration}

Para algunos destinos, Destination SDK requiere que configure una configuración de metadatos de audiencia para crear, actualizar o eliminar audiencias de forma programada en el destino. Consulte [Gestión de metadatos de audiencia](../functionality/audience-metadata-management.md) para obtener información sobre cuándo debe configurar esta configuración y cómo hacerlo.

Si utiliza una configuración de metadatos de audiencia, debe conectarla a la configuración de destino que creó en el paso 2. Añada el ID de instancia de la configuración de metadatos de audiencia a la configuración de destino como `audienceTemplateId`.

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

Dependiendo de si especifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` en la configuración de destino anterior, puede configurar la autenticación para el destino utilizando la variable `/destination` o `/credentials` punto final.

Si ha seleccionado `"authenticationRule": "CUSTOMER_AUTHENTICATION"` en la configuración de destino y su destino admite el método de autenticación OAuth 2, lea [Autenticación OAuth 2](../functionality/destination-configuration/oauth2-authentication.md).

Si ha seleccionado `"authenticationRule": "PLATFORM_AUTHENTICATION"`, debe crear un [configuración de credenciales](../credentials-api/create-credential-configuration.md).

## Paso 6: Probar el destino {#test-destination}

Después de configurar el destino utilizando los extremos de configuración de los pasos anteriores, puede usar la variable [herramienta de prueba de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) para probar la integración entre Adobe Experience Platform y el destino.

Como parte del proceso para probar el destino, debe utilizar la interfaz de usuario del Experience Platform para crear segmentos, que activará en el destino. Consulte los dos recursos siguientes para obtener instrucciones sobre cómo crear segmentos en Experience Platform:

* [Creación de una página de documentación de segmentos](/help/segmentation/ui/overview.md#create-segment)
* [Tutorial en vídeo sobre la creación de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Paso 7: Publicar su destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar y probar el destino, use la variable [API de publicación de destino](../publishing-api/create-publishing-request.md) para enviar la configuración a Adobe para su revisión.

## Paso 8: Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea un [integración de productos](../overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](../docs-framework/documentation-instructions.md) para crear una página de documentación de producto para su destino en el [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md).

## Paso 9: Enviar destino para revisión del Adobe {#submit-for-review}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Finalmente, antes de que el destino se pueda publicar en el catálogo del Experience Platform y sea visible para todos los clientes Experience Platform, debe enviar oficialmente el destino para su revisión por parte del Adobe. Buscar información completa sobre cómo [enviar para su revisión un destino producido creado en Destination SDK](../guides/submit-destination.md).
