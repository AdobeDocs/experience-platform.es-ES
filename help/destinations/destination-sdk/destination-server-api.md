---
description: Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/destination-servers`. Las especificaciones de servidor y plantilla para su destino se pueden configurar en el SDK de destino de Adobe Experience Platform a través del punto final común "/authoring/destination-servers".
title: Operaciones de API de extremo del servidor de destino
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 5%

---

# Operaciones de API de extremo del servidor de destino

>[!IMPORTANT]
>
>**Punto final** de API:  `platform.adobe.io/data/core/activation/authoring/destination-servers`

Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/destination-servers` . Las especificaciones de servidor y plantilla para su destino se pueden configurar en el SDK de destino de Adobe Experience Platform mediante el punto final común `/authoring/destination-servers`. Para obtener una descripción de la funcionalidad proporcionada por este extremo, lea [especificaciones del servidor y la plantilla](./server-and-template-configuration.md).

## Introducción a las operaciones de API del servidor de destino {#get-started}

Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino necesario y los encabezados necesarios.

## Crear configuración para un servidor de destino {#create}

Puede crear una nueva configuración de servidor de destino realizando una solicitud de POST al extremo `/authoring/destination-servers` .

**Formato de API**


```http
POST /authoring/destination-servers
```

**Solicitud**

La siguiente solicitud crea una nueva configuración del servidor de destino, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el extremo `/authoring/destination-servers` . Tenga en cuenta que no es necesario agregar todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `name` | Cadena | Representa un nombre descriptivo del servidor, visible solo para el Adobe. Este nombre no es visible para socios o clientes. Ejemplo `Moviestar destination server`. |
| `destinationServerType` | Cadena | `URL_BASED` actualmente es la única opción disponible. |
| `urlBasedDestination.url.templatingStrategy` | Cadena | <ul><li>Utilice `PEBBLE_V1` si el Adobe necesita transformar la dirección URL en el campo `value` que aparece a continuación. Utilice esta opción si tiene un punto final como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilice `NONE` si no se necesita ninguna transformación en el lado del Adobe, por ejemplo si tiene un punto final como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Cadena | Rellene la dirección del extremo de API al que se debe conectar el Experience Platform. |
| `urlBasedDestination.maxUsersPerRequest` | Número entero | Adobe puede agregar varios perfiles exportados en una sola llamada HTTP. Especifique el número máximo de perfiles que su extremo debe recibir en una sola llamada HTTP. Tenga en cuenta que esta es una agregación de mejor esfuerzo. Por ejemplo, si especifica el valor 100, los Adobes pueden enviar cualquier número de perfiles menores que 100 en una llamada. <br> Si el servidor no acepta varios usuarios por solicitud, establezca este valor en 1. |
| `urlBasedDestination.splitUserById` | Booleano | Utilice este indicador si la llamada al destino debe dividirse por identidad. Establezca este indicador como `true` si el servidor solo acepta una identidad por llamada, para un área de nombres determinada. |
| `httpTemplate.httpMethod` | Cadena | Método que Adobe utilizará en las llamadas al servidor. Las opciones son `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Cadena | En su lugar, utilice `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Cadena | Esta cadena es la versión con caracteres de escape que transforma los datos de los clientes de Platform al formato que el servicio espera. <br> <ul><li> Para obtener información sobre cómo escribir la plantilla, lea la [sección Uso de plantillas](./message-format.md#using-templating). </li><li> Para obtener más información sobre el escape de caracteres, consulte el [estándar RFC JSON, sección siete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para ver un ejemplo de transformación sencilla, consulte la transformación [Atributos de perfil](./message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Cadena | El tipo de contenido que acepta el servidor. Es muy probable que este valor sea `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

## Enumerar configuraciones del servidor de destino {#retrieve-list}

Puede recuperar una lista de todas las configuraciones de servidor de destino para su organización IMS realizando una solicitud de GET al extremo `/authoring/destination-servers` .

**Formato de API**


```http
GET /authoring/destination-servers
```

**Solicitud**

La siguiente solicitud recuperará la lista de configuraciones de servidor de destino a las que tiene acceso, según la configuración de la organización y el simulador de pruebas de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de configuraciones de servidor de destino a las que tiene acceso, según el ID de organización de IMS y el nombre del entorno limitado que ha utilizado. Un `instanceId` corresponde a la plantilla de un servidor de destino. La respuesta se trunca para su brevedad.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## Actualizar una configuración de servidor de destino existente {#update}

Puede actualizar una configuración de servidor de destino existente realizando una solicitud de PUT al extremo `/authoring/destination-servers` y proporcionando el ID de instancia de la configuración de servidor de destino que desea actualizar. En el cuerpo de la llamada, proporcione la configuración actualizada del servidor de destino.

**Formato de API**


```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración del servidor de destino que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza una configuración de servidor de destino existente, configurada por los parámetros proporcionados en la carga útil.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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





## Recuperar una configuración específica del servidor de destino {#get}

Puede recuperar información detallada sobre una configuración específica del servidor de destino realizando una solicitud de GET al extremo `/authoring/destination-servers` y proporcionando el ID de instancia de la configuración del servidor de destino que desea actualizar.

**Formato de API**


```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración del servidor de destino que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la configuración del servidor de destino especificada.

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


## Eliminar una configuración específica del servidor de destino {#delete}

Puede eliminar la configuración del servidor de destino especificada realizando una solicitud de DELETE al extremo `/authoring/destination-servers` y proporcionando el ID de la configuración del servidor de destino que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | El `id` de la configuración del servidor de destino que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

## Gestión de errores de API

Los extremos de la API del SDK de destino siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte los [códigos de estado de API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) y [errores de encabezado de solicitud](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo configurar el servidor de destino y la plantilla mediante el extremo de API `/authoring/destination-servers`. Lea [cómo utilizar el SDK de destino para configurar su destino](./configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
