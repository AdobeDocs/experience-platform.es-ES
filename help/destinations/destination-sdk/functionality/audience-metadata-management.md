---
description: Utilice plantillas de metadatos de audiencia para crear, actualizar o eliminar audiencias en el destino mediante programación. Adobe proporciona una plantilla de metadatos de audiencia ampliable que puede configurar en función de las especificaciones de su API de marketing. Después de definir, probar y enviar la plantilla, se utilizará por Adobe para estructurar las llamadas de API a su destino.
title: Gestión de metadatos de audiencia
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: 3660c3a342af07268d2ca2c907145df8237872a1
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Gestión de metadatos de audiencia

Utilice plantillas de metadatos de audiencia para crear, actualizar o eliminar audiencias en el destino mediante programación. Adobe proporciona una plantilla de metadatos de audiencia ampliable que puede configurar en función de las especificaciones de su API de marketing. Después de definir, probar y enviar la configuración, se utilizará por Adobe para estructurar las llamadas de API a su destino.

Puede configurar la funcionalidad descrita en este documento utilizando `/authoring/audience-templates` Extremo de API. Leer [crear una plantilla de metadatos](../metadata-api/create-audience-template.md) para obtener una lista completa de las operaciones que puede realizar en el extremo.

## Cuándo usar el punto de conexión de gestión de metadatos de audiencia {#when-to-use}

Según la configuración de la API, puede que necesite o no utilizar el punto de conexión de gestión de metadatos de audiencia al configurar el destino en Experience Platform. Utilice el diagrama de árbol de decisión que aparece a continuación para comprender cuándo utilizar el extremo de metadatos de audiencia y cómo configurar una plantilla de metadatos de audiencia para su destino.

![Diagrama del árbol de decisiones](../assets/functionality/audience-metadata-decision-tree.png)

## Casos de uso admitidos por la gestión de metadatos de audiencia {#use-cases}

Con la compatibilidad con los metadatos de audiencia en Destination SDK, al configurar el destino del Experience Platform, puede proporcionar a los usuarios de Platform una de las varias opciones al asignar y activar audiencias en el destino. Puede controlar las opciones disponibles para el usuario mediante los parámetros del [Configuración de metadatos de audiencia](../functionality/destination-configuration/audience-metadata-configuration.md) de la configuración de destino.

### Caso de uso 1: Tiene una API de terceros y los usuarios no necesitan introducir ID de asignación

Si tiene un punto final de API para crear, actualizar o eliminar audiencias o audiencias, puede utilizar plantillas de metadatos de audiencia para configurar Destination SDK de modo que coincida con las especificaciones de su punto final de creación, actualización o eliminación de audiencia. El Experience Platform puede crear, actualizar o eliminar audiencias mediante programación y sincronizar los metadatos con el Experience Platform.

Al activar audiencias en el destino en la interfaz de usuario (IU) de Experience Platform, los usuarios no necesitan rellenar manualmente un campo de ID de asignación de audiencia en el flujo de trabajo de activación.

### Caso de uso 2: Los usuarios deben crear primero una audiencia en el destino y deben introducir manualmente el ID de asignación

Si los socios o usuarios deben crear audiencias y otros metadatos manualmente en el destino, los usuarios deben rellenar manualmente el campo ID de asignación de audiencia en el flujo de trabajo de activación para sincronizar los metadatos de audiencia entre el destino y el Experience Platform.

![ID de asignación de entrada](../assets/functionality/input-mapping-id.png)

### Caso de uso 3: Su destino acepta el ID de audiencia de Experience Platform, los usuarios no necesitan introducir manualmente el ID de asignación

Si el sistema de destino acepta el ID de audiencia de Experience Platform, puede configurarlo en la plantilla de metadatos de audiencia. Los usuarios no tienen que rellenar un ID de asignación de audiencia al activar un segmento.

## Plantilla de audiencia genérica y ampliable {#generic-and-extensible}

Para admitir los casos de uso enumerados anteriormente, Adobe proporciona una plantilla genérica que se puede personalizar para ajustarla a las especificaciones de la API.

Puede utilizar la plantilla genérica para lo siguiente [crear una nueva plantilla de audiencia](../metadata-api/create-audience-template.md) si la API admite:

* Los métodos HTTP: POST, GET, PUT, DELETE, PATCH
* Los tipos de autenticación: OAuth 1, OAuth 2 con token de actualización, OAuth 2 con token de portador
* Las funciones: crear una audiencia, actualizar una audiencia, obtener una audiencia, eliminar una audiencia, validar credenciales

El equipo de ingeniería de Adobes puede trabajar con usted para expandir la plantilla genérica con campos personalizados si sus casos de uso lo requieren.

## Ejemplos de configuración {#configuration-examples}

Esta sección incluye tres ejemplos de configuraciones de metadatos de audiencia genéricas, para su referencia, junto con descripciones de las secciones principales de la configuración. Observe cómo la dirección URL, los encabezados, la solicitud y el cuerpo de respuesta difieren entre las tres configuraciones de ejemplo. Esto se debe a las diferentes especificaciones de la API de marketing de las tres plataformas de ejemplo.

Tenga en cuenta que, en algunos ejemplos, los campos de macro como `{{authData.accessToken}}` o `{{segment.name}}` se utilizan en la dirección URL y, en otros ejemplos, en los encabezados o en el cuerpo de la solicitud. Realmente depende de las especificaciones de su API de marketing.

| Sección de plantilla | Descripción |
|--- |--- |
| `create` | Incluye todos los componentes necesarios (URL, método HTTP, encabezados, cuerpo de solicitud y respuesta) para realizar una llamada HTTP a la API, crear mediante programación segmentos/audiencias en la plataforma y sincronizar la información de nuevo con Adobe Experience Platform. |
| `update` | Incluye todos los componentes necesarios (URL, método HTTP, encabezados, cuerpo de solicitud y respuesta) para realizar una llamada HTTP a la API, para actualizar mediante programación segmentos/audiencias en la plataforma y sincronizar la información de nuevo con Adobe Experience Platform. |
| `delete` | Incluye todos los componentes necesarios (URL, método HTTP, encabezados, cuerpo de solicitud y respuesta) para realizar una llamada HTTP a la API y eliminar segmentos/audiencias en la plataforma mediante programación. |
| `validate` | Ejecuta las validaciones de cualquier campo en la configuración de la plantilla antes de realizar una llamada a la API del socio. Por ejemplo, puede validar que el ID de cuenta del usuario se introduzca correctamente. |
| `notify` | Solo se aplica a destinos basados en archivos. Incluye todos los componentes necesarios (URL, método HTTP, encabezados, cuerpo de solicitud y respuesta) para realizar una llamada HTTP a la API y notificarle las exportaciones de archivos correctas. |

{style="table-layout:auto"}

### Ejemplo 1 de transmisión {#example-1}

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

### Ejemplo 2 de streaming {#example-2}

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

### Ejemplo 3 de transmisión {#example-3}

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


### Ejemplo basado en archivos {#example-file-based}

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
      "notify":{
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

Busque descripciones de todos los parámetros en la plantilla en la [Creación de una plantilla de audiencia](../metadata-api/create-audience-template.md) Referencia de API.

## Macros utilizadas en plantillas de metadatos de audiencia {#macros}

Para pasar información como ID de audiencia, tokens de acceso, mensajes de error y mucho más entre Experience Platform y la API, las plantillas de audiencia incluyen macros que puede utilizar. Lea a continuación una descripción de las macros que se utilizan en los tres ejemplos de configuración de esta página:

| Macro | Descripción |
|--- |--- |
| `{{segment.alias}}` | Permite acceder al alias de audiencia en Experience Platform. |
| `{{segment.name}}` | Permite acceder al nombre de la audiencia en Experience Platform. |
| `{{segment.id}}` | Permite acceder al ID de audiencia en Experience Platform. |
| `{{customerData.accountId}}` | Permite acceder al campo ID de cuenta que configuró en la configuración de destino. |
| `{{oauth2ServiceAccessToken}}` | Permite generar dinámicamente un token de acceso basado en la configuración de OAuth 2. |
| `{{authData.accessToken}}` | Permite pasar el token de acceso a su extremo de API. Uso `{{authData.accessToken}}` si el Experience Platform debe utilizar tokens que no caduquen para conectarse a su destino, de lo contrario, utilice `{{oauth2ServiceAccessToken}}` para generar un token de acceso. |
| `{{body.segments[0].segment.id}}` | Devuelve el identificador único de la audiencia creada, como valor de la clave `externalAudienceId`. |
| `{{error.message}}` | Devuelve un mensaje de error que se mostrará a los usuarios en la interfaz de usuario de Experience Platform. |

{style="table-layout:auto"}
