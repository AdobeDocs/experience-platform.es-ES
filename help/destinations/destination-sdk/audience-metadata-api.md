---
description: En esta página se describen todas las operaciones de API que se pueden realizar con el extremo de la API `/authoring/audience-templates`.
title: Operaciones de API de extremo de metadatos de audiencia
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 5%

---

# Operaciones de API de extremo de metadatos de audiencia

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

En esta página se enumeran y describen todas las operaciones de API que puede realizar mediante la `/authoring/audience-templates` extremo de API. Para obtener una descripción de cuándo usar este extremo, lea [gestión de metadatos de audiencia](./audience-metadata-management.md).

## Introducción a las operaciones de API de plantillas de audiencia {#get-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Creación de una nueva plantilla de audiencia {#create}

Puede crear una nueva plantilla de audiencia realizando una solicitud de POST al `/authoring/audience-templates` punto final.

**Formato de API**

```http
POST /authoring/audience-templates
```

**Solicitud**

La siguiente solicitud crea una nueva plantilla de metadatos de audiencia, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por la variable `/authoring/audience-templates` punto final. Tenga en cuenta que no es necesario agregar todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Propiedad | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `name` | Cadena | Nombre de la plantilla de metadatos de audiencia para el destino. Este nombre aparece en cualquier mensaje de error específico del socio en la interfaz de usuario del Experience Platform, seguido del mensaje de error analizado desde `metadataTemplate.create.errorSchemaMap`. |
| `url` | Cadena | La URL y el punto final de su API, que se utilizan para crear, actualizar, eliminar o validar audiencias o segmentos en su plataforma. Dos ejemplos del sector son: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` y `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Cadena | Método utilizado en el punto final para crear, actualizar, eliminar o validar mediante programación el segmento o la audiencia en el destino. Por ejemplo: `POST`, `PUT`, `DELETE` |
| `headers.header` | Cadena | Especifica los encabezados HTTP que deben agregarse a la llamada a la API. Por ejemplo, `"Content-Type"` |
| `headers.value` | Cadena | Especifica el valor de los encabezados HTTP que deben agregarse a la llamada a la API. Por ejemplo, `"application/x-www-form-urlencoded"` |
| `requestBody` | Cadena | Especifica el contenido del cuerpo del mensaje que se debe enviar a la API. Los parámetros que deben añadirse a la variable `requestBody` dependen de los campos que acepte la API. Para ver un ejemplo, consulte la [primer ejemplo de plantilla](./audience-metadata-management.md#example-1) en el documento de funcionalidad de metadatos de audiencia . |
| `responseFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se llama a . Para ver un ejemplo, consulte la [ejemplos de plantilla](./audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de audiencia . |
| `responseFields.value` | Cadena | Especifique el valor de los campos de respuesta que su API devuelve cuando se llama a . |
| `responseErrorFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se llama a . Para ver un ejemplo, consulte la [ ejemplos de plantilla](./audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de audiencia . |
| `responseErrorFields.value` | Cadena | Analiza los mensajes de error devueltos en las respuestas de llamadas de API desde el destino. Estos mensajes de error se enviarán a los usuarios de la interfaz de usuario del Experience Platform. |
| `validations.field` | Cadena | Indica si se deben ejecutar las validaciones para cualquier campo antes de que se realicen llamadas de API al destino. Por ejemplo, puede utilizar `{{validations.accountId}}` para validar el ID de cuenta del usuario. |
| `validations.regex` | Cadena | Indica cómo se debe estructurar el campo para que pase la validación. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la plantilla de audiencia recién creada.

## Actualizar plantilla de audiencia {#update}

Puede actualizar una plantilla de audiencia existente realizando una solicitud de PUT al `/authoring/audience-templates` y proporcionando el ID de instancia de la plantilla de audiencia que desea actualizar. En el cuerpo de la llamada a , proporcione la plantilla actualizada.

**Formato de API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la plantilla de metadatos de audiencia que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza una plantilla de metadatos de audiencia existente, configurada por los parámetros proporcionados en la carga útil.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

## Recuperar una lista de plantillas de audiencia {#retrieve-list}

Puede recuperar una lista de todas las plantillas de audiencia de su organización realizando una solicitud de GET al `/authoring/audience-templates` punto final.

**Formato de API**


```http
GET /authoring/audience-templates
```

**Solicitud**

La siguiente solicitud recuperará la lista de plantillas de audiencia a las que tiene acceso, según la organización y la configuración del entorno limitado.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de plantillas de metadatos de audiencia a las que tiene acceso, según el ID de organización y el nombre de entorno limitado que haya utilizado. One `instanceId` corresponde a la plantilla de un destino. La respuesta se trunca para su brevedad.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Recuperar una plantilla de audiencia específica {#get}

Puede recuperar información detallada sobre una plantilla de audiencia específica realizando una solicitud de GET al `/authoring/audience-templates` y proporcionando el ID de instancia de la plantilla de audiencia que desea recuperar.

**Formato de API**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la plantilla de metadatos de audiencia que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la plantilla de audiencia especificada.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## Eliminar una plantilla de audiencia específica {#delete}

Puede eliminar la plantilla de audiencia especificada realizando una solicitud de DELETE al `/authoring/audience-templates` y proporcionando el ID de la plantilla de audiencia que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | La variable `id` de la plantilla de audiencia que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cuándo usar plantillas de metadatos de audiencia y cómo configurar una plantilla de metadatos de audiencia usando la variable `/authoring/audience-templates` extremo de API. Lectura [cómo usar Destination SDK para configurar el destino](./configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
