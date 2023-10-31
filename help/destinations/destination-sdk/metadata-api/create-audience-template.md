---
description: Esta página ejemplifica la llamada de API utilizada para crear una plantilla de audiencia a través del Adobe Experience Platform Destination SDK.
title: Creación de una plantilla de audiencia
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 4%

---

# Creación de una plantilla de audiencia

>[!IMPORTANT]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Para algunos destinos creados con Destination SDK, debe crear una configuración de metadatos de audiencia para crear, actualizar o eliminar mediante programación metadatos de audiencia en el destino. Esta página muestra cómo utilizar la variable `/authoring/audience-templates` Punto final de API para crear la configuración.

Para obtener una descripción detallada de las funciones que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantillas de audiencia {#get-started}

Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Creación de una plantilla de audiencia {#create}

Puede crear una nueva plantilla de audiencia creando un `POST` solicitud a la `/authoring/audience-templates` punto final.

**Formato de API**

```http
POST /authoring/audience-templates
```

+++Solicitud

La siguiente solicitud crea una nueva plantilla de audiencia, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el `/authoring/audience-templates` punto final. Tenga en cuenta que no tiene que añadir todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

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
| `name` | Cadena | Nombre de la plantilla de metadatos de audiencia del destino. Este nombre aparece en cualquier mensaje de error específico del socio en la interfaz de usuario del Experience Platform, seguido del mensaje de error analizado desde `metadataTemplate.create.errorSchemaMap`. |
| `url` | Cadena | La dirección URL y el punto final de su API, que se utiliza para crear, actualizar, eliminar o validar audiencias en su plataforma. Dos ejemplos del sector son: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` y `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Cadena | Método utilizado en el extremo para crear, actualizar, eliminar o validar la audiencia en el destino mediante programación. Por ejemplo: `POST`, `PUT`, `DELETE` |
| `headers.header` | Cadena | Especifica cualquier encabezado HTTP que deba agregarse a la llamada a su API. Por ejemplo, `"Content-Type"` |
| `headers.value` | Cadena | Especifica el valor de los encabezados HTTP que deben agregarse a la llamada a la API. Por ejemplo, `"application/x-www-form-urlencoded"` |
| `requestBody` | Cadena | Especifica el contenido del cuerpo del mensaje que debe enviarse a la API. Los parámetros que deben añadirse a `requestBody` depende de los campos que acepte su API. Por ejemplo, consulte la [primer ejemplo de plantilla](../functionality/audience-metadata-management.md#example-1) en el documento de funcionalidad de metadatos de Audiencia. |
| `responseFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se le llama. Por ejemplo, consulte la [ejemplos de plantillas](../functionality/audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de Audiencia. |
| `responseFields.value` | Cadena | Especifique el valor de los campos de respuesta que devuelve la API cuando se llama a. |
| `responseErrorFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se le llama. Por ejemplo, consulte la [ejemplos de plantillas](../functionality/audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de Audiencia. |
| `responseErrorFields.value` | Cadena | Analiza cualquier mensaje de error devuelto en las respuestas de llamadas de API desde su destino. Estos mensajes de error aparecerán a los usuarios en la interfaz de usuario del Experience Platform. |
| `validations.field` | Cadena | Indica si se deben ejecutar las validaciones para algún campo antes de realizar llamadas de API al destino. Por ejemplo, puede utilizar `{{validations.accountId}}` para validar el ID de cuenta del usuario. |
| `validations.regex` | Cadena | Indica cómo se debe estructurar el campo para que se apruebe la validación. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la plantilla de audiencia recién creada.

+++

## Administración de errores de API

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, sabe cuándo usar plantillas de audiencia y cómo configurar una plantilla de audiencia con la variable `/authoring/audience-templates` Extremo de API. Leer [cómo utilizar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración del destino.
