---
description: Utilice plantillas de metadatos de audiencia para crear, actualizar o eliminar audiencias de forma programada en el destino. Adobe proporciona una plantilla de metadatos de audiencia extensible, que puede configurar en función de las especificaciones de su API de marketing. Después de definir, probar y enviar la plantilla, Adobe la utilizará para estructurar las llamadas de API al destino.
title: Gestión de metadatos de audiencia
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: cb4e399798a9521e6f3da89cbd88d19476ab070d
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 1%

---

# Gestión de metadatos de audiencia {#audience-metadata-management}

## Información general {#overview}

Utilice plantillas de metadatos de audiencia para crear, actualizar o eliminar audiencias de forma programada en el destino. Adobe proporciona una plantilla de metadatos de audiencia extensible, que puede configurar en función de las especificaciones de su API de marketing. Después de definir, probar y enviar la configuración, Adobe la utilizará para estructurar las llamadas de API al destino.

Puede configurar la funcionalidad descrita en este documento utilizando la variable `/authoring/audience-templates` extremo de API. Lectura [Operaciones de API de extremo de metadatos de audiencia](./audience-metadata-api.md) para obtener una lista completa de las operaciones que puede realizar en el punto final.

## Cuándo usar el extremo de gestión de metadatos de audiencia {#when-to-use}

Según la configuración de la API, puede que necesite o no utilizar el extremo de gestión de metadatos de audiencia al configurar el destino en Experience Platform. Utilice el diagrama del árbol de decisiones a continuación para comprender cuándo se debe utilizar el extremo de metadatos de audiencia y cómo configurar una plantilla de metadatos de audiencia para el destino.

![Diagrama del árbol de decisiones](./assets/audience-metadata-decision-tree.png)

## Casos de uso admitidos por la gestión de metadatos de audiencia {#use-cases}

Con la compatibilidad con los metadatos de audiencia en Destination SDK, al configurar el destino de Experience Platform, puede dar a los usuarios de Platform una de las varias opciones cuando asignen y activen segmentos al destino. Puede controlar las opciones disponibles para el usuario mediante los parámetros de la sección de asignación de segmentos del [configuración de destino](./destination-configuration.md#segment-mapping).

### Caso de uso 1: Tiene una API de terceros y los usuarios no necesitan introducir ID de asignación

Si tiene un punto final de API para crear, actualizar o eliminar segmentos o audiencias, puede usar plantillas de metadatos de audiencia para configurar Destination SDK de modo que coincida con las especificaciones del punto final de creación, actualización o eliminación del segmento. El Experience Platform puede crear, actualizar o eliminar segmentos mediante programación y sincronizar los metadatos de nuevo con el Experience Platform.

Al activar segmentos en el destino en la interfaz de usuario (IU) del Experience Platform, los usuarios no necesitan rellenar manualmente un campo ID de asignación de segmentos en el flujo de trabajo de activación.

### Caso de uso 2: Los usuarios deben crear primero un segmento en el destino y se les requiere introducir manualmente el ID de asignación

Si los socios o usuarios necesitan crear manualmente segmentos y otros metadatos en el destino, los usuarios deben rellenar manualmente el campo ID de asignación de segmentos en el flujo de trabajo de activación para sincronizar los metadatos de segmentos entre el destino y el Experience Platform.

![ID de asignación de entrada](./assets/input-mapping-id.png)

### Caso de uso 3: Su destino acepta el ID de segmento del Experience Platform, los usuarios no necesitan introducir manualmente el ID de asignación

Si el sistema de destino acepta el ID de segmento del Experience Platform, puede configurarlo en la plantilla de metadatos de audiencia. Los usuarios no tienen que rellenar un ID de asignación de segmentos al activar un segmento.

## Plantilla de audiencia genérica y extensible {#generic-and-extensible}

Para admitir los casos de uso enumerados anteriormente, Adobe le proporciona una plantilla genérica que puede personalizarse para ajustarse a las especificaciones de su API.

Puede utilizar la plantilla genérica para [crear una plantilla de audiencia nueva](./audience-metadata-api.md#create) si su API admite:

* Los métodos HTTP: POST, GET, PUT, DELETE, PATCH
* Los tipos de autenticación: OAuth 1, OAuth 2 con token de actualización, OAuth 2 con token de portador
* Las funciones: crear una audiencia, actualizar una audiencia, obtener una audiencia, eliminar una audiencia, validar credenciales

El equipo de ingeniería de Adobes puede trabajar con usted para expandir la plantilla genérica con campos personalizados si sus casos de uso lo requieren.

## Ejemplos de configuración {#configuration-examples}

Esta sección incluye tres ejemplos de configuraciones de metadatos de audiencia genéricas, para su referencia, junto con descripciones de las secciones principales de la configuración. Observe cómo la dirección URL, los encabezados, la solicitud y el cuerpo de respuesta difieren entre las tres configuraciones de ejemplo. Esto se debe a las diferentes especificaciones de la API de marketing de las tres plataformas de muestra.

Tenga en cuenta que en algunos ejemplos, los campos de macro como `{{authData.accessToken}}` o `{{segment.name}}` se utilizan en la dirección URL y en otros ejemplos se utilizan en los encabezados o en el cuerpo de la solicitud. Realmente depende de las especificaciones de la API de marketing.

| Sección Plantilla | Descripción |
|--- |--- |
| `create` | Incluye todos los componentes necesarios (URL, método HTTP, encabezados, solicitud y cuerpo de respuesta) para realizar una llamada HTTP a la API, para crear segmentos o audiencias mediante programación en la plataforma y sincronizar la información de nuevo con Adobe Experience Platform. |
| `update` | Incluye todos los componentes necesarios (URL, método HTTP, encabezados, solicitud y cuerpo de respuesta) para realizar una llamada HTTP a la API, actualizar mediante programación segmentos o audiencias en la plataforma y volver a sincronizar la información con Adobe Experience Platform. |
| `delete` | Incluye todos los componentes necesarios (URL, método HTTP, encabezados, solicitud y cuerpo de respuesta) para realizar una llamada HTTP a la API y eliminar segmentos o audiencias de forma programada en la plataforma. |
| `validate` | Ejecuta validaciones para cualquier campo de la configuración de la plantilla antes de realizar una llamada a la API del socio. Por ejemplo, puede validar que el ID de cuenta del usuario se introduce correctamente. |

{style=&quot;table-layout:auto&quot;}

### Primer ejemplo {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

### Segundo ejemplo {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

### Tercer ejemplo {#example-3}

```json
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
```

Buscar descripciones de todos los parámetros de la plantilla en la documentación de referencia [Operaciones de API de extremo de metadatos de audiencia](./audience-metadata-api.md).

## Macros utilizados en plantillas de metadatos de audiencia

Para pasar información como ID de segmento, tokens de acceso, mensajes de error, etc. entre Experience Platform y su API, las plantillas de audiencia incluyen macros que puede utilizar. A continuación se muestra una descripción de las macros que se utilizan en los tres ejemplos de configuración de esta página:

| Macro | Descripción |
|--- |--- |
| `{{segment.alias}}` | Permite acceder al alias del segmento en el Experience Platform. |
| `{{segment.name}}` | Permite acceder al nombre del segmento en Experience Platform. |
| `{{segment.id}}` | Permite acceder al ID de segmento en Experience Platform. |
| `{{customerData.accountId}}` | Permite acceder al campo Id de cuenta que configuró en la configuración de destino. |
| `{{oauth2ServiceAccessToken}}` | Permite generar dinámicamente un token de acceso basado en la configuración de OAuth 2. |
| `{{authData.accessToken}}` | Permite pasar el token de acceso a su extremo de API. Uso `{{authData.accessToken}}` si el Experience Platform debe utilizar tokens que no caduquen para conectarse al destino, de lo contrario, utilice `{{oauth2ServiceAccessToken}}` para generar un token de acceso. |
| `{{body.segments[0].segment.id}}` | Devuelve el identificador único de la audiencia creada, como el valor de la clave `externalAudienceId`. |
| `{{error.message}}` | Devuelve un mensaje de error que se mostrará a los usuarios en la interfaz de usuario del Experience Platform. |

{style=&quot;table-layout:auto&quot;}
