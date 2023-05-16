---
description: Esta página ejemplifica la llamada de API utilizada para crear una plantilla de audiencia a través del Adobe Experience Platform Destination SDK.
title: Creación de una plantilla de audiencia
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 4%

---


# Creación de una plantilla de audiencia

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Para algunos destinos creados con Destination SDK, debe crear una configuración de metadatos de audiencia para crear, actualizar o eliminar metadatos de segmento en el destino mediante programación. Esta página muestra cómo usar la variable `/authoring/audience-templates` extremo de API para crear la configuración.

Para obtener una descripción detallada de las capacidades que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantilla de audiencia {#get-started}

Antes de continuar, revise la [guía de introducción](../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Creación de una plantilla de audiencia {#create}

Puede crear una nueva plantilla de audiencia creando un `POST` solicitud al `/authoring/audience-templates` punto final.

**Formato de API**

```http
POST /authoring/audience-templates
```

+++Solicitud

La siguiente solicitud crea una nueva plantilla de audiencia, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por la variable `/authoring/audience-templates` punto final. Tenga en cuenta que no es necesario agregar todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

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
| `requestBody` | Cadena | Especifica el contenido del cuerpo del mensaje que se debe enviar a la API. Los parámetros que deben añadirse a la variable `requestBody` dependen de los campos que acepte la API. Para ver un ejemplo, consulte la [primer ejemplo de plantilla](../functionality/audience-metadata-management.md#example-1) en el documento de funcionalidad de metadatos de audiencia . |
| `responseFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se llama a . Para ver un ejemplo, consulte la [ejemplos de plantilla](../functionality/audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de audiencia . |
| `responseFields.value` | Cadena | Especifique el valor de los campos de respuesta que su API devuelve cuando se llama a . |
| `responseErrorFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se llama a . Para ver un ejemplo, consulte la [ ejemplos de plantilla](../functionality/audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de audiencia . |
| `responseErrorFields.value` | Cadena | Analiza los mensajes de error devueltos en las respuestas de llamadas de API desde el destino. Estos mensajes de error se enviarán a los usuarios de la interfaz de usuario del Experience Platform. |
| `validations.field` | Cadena | Indica si se deben ejecutar las validaciones para cualquier campo antes de que se realicen llamadas de API al destino. Por ejemplo, puede utilizar `{{validations.accountId}}` para validar el ID de cuenta del usuario. |
| `validations.regex` | Cadena | Indica cómo se debe estructurar el campo para que pase la validación. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la plantilla de audiencia recién creada.

+++

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cuándo usar plantillas de audiencia y cómo configurar una plantilla de audiencia usando la variable `/authoring/audience-templates` extremo de API. Lectura [cómo usar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
