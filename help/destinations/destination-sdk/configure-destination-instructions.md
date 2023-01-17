---
description: En esta página se enumeran y describen los pasos para configurar un destino de flujo continuo mediante el Destination SDK .
title: Usar Destination SDK para configurar un destino de flujo continuo
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0d58d949ff24b9059d6afe81de354da0783ec8a4
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Usar Destination SDK para configurar un destino de flujo continuo

## Información general {#overview}

Esta página describe cómo utilizar la información de [Opciones de configuración en el SDK de Destinations](./configuration-options.md) y en otros documentos de referencia de API y funcionalidad de Destination SDK para configurar un [destino de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). Los pasos se muestran en orden secuencial a continuación.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos que se ilustran a continuación, lea la [introducción al Destination SDK](./getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Pasos para utilizar las opciones de configuración en Destination SDK para configurar el destino {#steps}

![Pasos ilustrados para utilizar extremos de Destination SDK](./assets/destination-sdk-steps.png)

## Paso 1: Creación de un servidor y una configuración de plantilla {#create-server-template-configuration}

Comience creando un servidor y una configuración de plantilla utilizando el `/destinations-server` punto final (leer [Referencia de API](destination-server-api.md)). Para obtener más información sobre el servidor y la configuración de plantillas, consulte [Especificaciones de servidor y plantilla](server-and-template-configuration.md) en la sección de referencia.

A continuación se muestra un ejemplo de configuración. Tenga en cuenta que la plantilla de transformación de mensajes de la sección `requestBody.value` se aborda en el paso 3, [Crear plantilla de transformación](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

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

A continuación se muestra un ejemplo de configuración para una plantilla de destino creada mediante el uso de la variable `/destinations` extremo de API. Para obtener más información sobre esta configuración, consulte [Configuración de destino](./destination-configuration.md).

Para conectar el servidor y la configuración de plantilla en el paso 1 a esta configuración de destino, añada el ID de instancia del servidor y la configuración de plantilla como `destinationServerId` aquí.

>[!IMPORTANT]
>
>Para crear un destino configurado correctamente, debe *must* agregar al menos una identidad de destino en `identityNamespaces`, como se muestra a continuación. Si no se configura ninguna identidad de destino, los usuarios no podrán continuar más allá del [Paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación.

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
   "segmentMappingConfig":{
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

En función de las cargas útiles compatibles con el destino, debe crear una plantilla que transforme el formato de los datos exportados desde el formato XDM de Adobe a un formato compatible con el destino. Consulte ejemplos de plantillas en la sección [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos](./message-format.md#using-templating) y utilice el [herramienta de creación de plantillas](./create-template.md) proporcionado por Adobe.

Una vez que haya creado una plantilla de transformación de mensaje que funcione para usted, agréguela a la configuración de servidor y plantilla que ha creado en el paso 1.

## Paso 4: Crear configuración de metadatos de audiencia {#create-audience-metadata-configuration}

Para algunos destinos, Destination SDK requiere que configure una configuración de metadatos de audiencia para crear, actualizar o eliminar audiencias de forma programada en el destino. Consulte [Gestión de metadatos de audiencia](./audience-metadata-management.md) para obtener información sobre cuándo debe configurar esta configuración y cómo hacerlo.

Si utiliza una configuración de metadatos de audiencia, debe conectarla a la configuración de destino que creó en el paso 2. Añada el ID de instancia de la configuración de metadatos de audiencia a la configuración de destino como `audienceTemplateId`.

## Paso 5: Configuración de la autenticación {#set-up-authentication}

Dependiendo de si especifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` en la configuración de destino anterior, puede configurar la autenticación para el destino utilizando la variable `/destination` o `/credentials` punto final.

* **Caso más común**: Si ha seleccionado `"authenticationRule": "CUSTOMER_AUTHENTICATION"` en la configuración de destino y su destino admite el método de autenticación OAuth 2, lea [Autenticación OAuth 2](./oauth2-authentication.md).
* Si ha seleccionado `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte [Configuración de autenticación](./authentication-configuration.md#when-to-use).

## Paso 6: Probar el destino {#test-destination}

Después de configurar el destino utilizando los extremos de configuración de los pasos anteriores, puede usar la variable [herramienta de prueba de destino](./test-destination.md) para probar la integración entre Adobe Experience Platform y el destino.

Como parte del proceso para probar el destino, debe utilizar la interfaz de usuario del Experience Platform para crear segmentos, que activará en el destino. Consulte los dos recursos siguientes para obtener instrucciones sobre cómo crear segmentos en Experience Platform:

* [Creación de una página de documentación de segmentos](/help/segmentation/ui/overview.md#create-segment)
* [Tutorial en vídeo sobre la creación de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Paso 7: Publicar su destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar y probar el destino, use la variable [API de publicación de destino](./destination-publish-api.md) para enviar la configuración a Adobe para su revisión.

## Paso 8: Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea un [integración de productos](./overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md) para crear una página de documentación de producto para su destino en el [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md).

## Paso 9: Enviar destino para revisión del Adobe {#submit-for-review}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Finalmente, antes de que el destino se pueda publicar en el catálogo del Experience Platform y sea visible para todos los clientes Experience Platform, debe enviar oficialmente el destino para su revisión por parte del Adobe. Buscar información completa sobre cómo [enviar para su revisión un destino producido creado en Destination SDK](/help/destinations/destination-sdk/submit-destination.md).
