---
description: Esta página ejemplifica la llamada de API utilizada para recuperar una configuración de servidor de destino mediante Adobe Experience Platform Destination SDK.
title: Recuperar una configuración de servidor de destino
exl-id: 1b375343-e793-4c91-856f-af66fe71822e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Recuperar una configuración de servidor de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para recuperar información sobre una configuración de servidor de destino existente mediante el extremo de API `/authoring/destination-servers`.

Para obtener una descripción detallada de las funciones utilizadas por los servidores de destino, lea los siguientes artículos:

* [Especificaciones del servidor para destinos creados con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Plantillas de especificaciones para destinos creados con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del mensaje](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuración de formato de archivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1&rbrace;.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API del servidor de destino {#get-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Recuperar una configuración de servidor de destino {#retrieve}

Puede recuperar una configuración de servidor de destino existente realizando una solicitud `GET` al extremo `/authoring/destination-servers`.

>[!TIP]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato de API**

Utilice el siguiente formato de API para recuperar todas las configuraciones del servidor de destino para su cuenta.

```http
GET /authoring/destination-servers
```

Utilice el siguiente formato de API para recuperar una configuración específica del servidor de destino, definida por el parámetro `{INSTANCE_ID}`.

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

Las dos solicitudes siguientes recuperan todas las configuraciones del servidor de destino para su organización de IMS o una configuración específica del servidor de destino, en función de si pasa el parámetro `INSTANCE_ID` en la solicitud.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente y sus respuestas.

>[!BEGINTABS]

>[!TAB Recuperar todas las configuraciones del servidor de destino]

La siguiente solicitud recuperará la lista de configuraciones del servidor de destino a las que tiene acceso, según la configuración de [!DNL IMS Org ID] y la zona protegida.

+++Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con una lista de configuraciones de servidor de destino a las que tiene acceso, en función del [!DNL IMS Org ID] y el nombre de zona protegida que ha utilizado. Un `instanceId` corresponde a un servidor de destino. La respuesta de ejemplo siguiente incluye dos configuraciones de servidor de destino.

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

+++

>[!TAB Recuperar una configuración específica del servidor de destino]

La siguiente solicitud recuperará una configuración específica del servidor de destino definida por el parámetro `{INSTANCE_ID}`.

+++Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración del servidor de destino que desea recuperar. |

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con la configuración del servidor de destino correspondiente al `{INSTANCE_ID}` proporcionado.

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
      }
   ]
}
```

+++

>[!ENDTABS]

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo recuperar una configuración de servidor de destino a través del extremo de API de Destination SDK `/authoring/destination-servers`.

Para obtener más información acerca de lo que puede hacer con este extremo, consulte los siguientes artículos:

* [Crear una configuración de servidor de destino](create-destination-server.md)
* [Actualizar la configuración de un servidor de destino](update-destination-server.md)
* [Eliminar una configuración de servidor de destino](delete-destination-server.md)
