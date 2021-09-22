---
description: Las especificaciones de servidor y plantilla se pueden configurar en el SDK de destino de Adobe Experience Platform a través del punto final común "/authoring/destination-servers".
title: Opciones de configuración para especificaciones de servidor y plantilla en el SDK de destino
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 9%

---

# Opciones de configuración para especificaciones de servidor y plantilla

## Información general {#overview}

Las especificaciones de servidor y plantilla se pueden configurar en el SDK de destino de Adobe Experience Platform a través del extremo común `/authoring/destination-servers`. Lea [Destinations API endpoint operations](./destination-server-api.md) para obtener una lista completa de las operaciones que puede realizar en el punto final.

## Ejemplo de configuración {#example-configuration}

```json
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Especificaciones del servidor {#server-specs}

![Configuración del servidor resaltada](./assets/server-configuration.png)

Los clientes podrán activar datos desde Adobe Experience Platform a su destino mediante exportaciones HTTP. La configuración del servidor contiene información sobre el servidor que recibe los mensajes (el servidor de su parte).

Este proceso envía datos de usuario como una serie de mensajes HTTP a la plataforma de destino. Los parámetros siguientes forman la plantilla de especificaciones del servidor HTTP.

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | *Requerido.* Representa un nombre descriptivo del servidor, visible solo para el Adobe. Este nombre no es visible para socios o clientes. Ejemplo `Moviestar destination server`. |
| `destinationServerType` | Cadena | *Requerido.* `URL_BASED` actualmente es la única opción disponible. |
| `templatingStrategy` | Cadena | *Requerido.* <ul><li>Utilice `PEBBLE_V1` si el Adobe necesita transformar la dirección URL en el campo `value` que aparece a continuación. Utilice esta opción si tiene un punto final como: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Utilice `NONE` si no se necesita ninguna transformación en el lado del Adobe, por ejemplo si tiene un punto final como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Cadena | *Requerido.* Rellene la dirección del extremo de API al que se debe conectar el Experience Platform. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Especificaciones de plantilla {#template-specs}

![Configuración de plantilla resaltada](./assets/template-configuration.png)

La especificación de plantilla le permite configurar cómo dar formato al mensaje exportado a su destino. Adobe utiliza un lenguaje de plantilla similar a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar los campos del esquema XDM en un formato compatible con el destino. Para obtener más información sobre la transformación, visite los vínculos siguientes:

* [Formato del mensaje](./message-format.md)
* [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe ofrece una [herramienta para desarrolladores](./create-template.md) que le ayuda a crear y probar una plantilla de transformación de mensajes.

| Parámetro | Tipo | Descripción |
|---|---|---|
| `httpMethod` | Cadena | *Requerido.* Método que Adobe utilizará en las llamadas al servidor. Las opciones son `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `value` | Cadena | *Requerido.* Esta cadena es la versión con caracteres de escape que transforma los datos de los clientes de Platform al formato que el servicio espera. <br> Para obtener información sobre cómo escribir la plantilla, lea la  [sección](./message-format.md#using-templating) Uso de plantillas . <br> Para obtener más información sobre el escape de caracteres, consulte el estándar JSON  [RFC, sección siete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para ver un ejemplo de transformación sencilla, consulte la transformación  [Atributo ](./message-format.md#attributes) de perfil. |
| `contentType` | Cadena | *Requerido.* El tipo de contenido que acepta el servidor. Es muy probable que este valor sea `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
