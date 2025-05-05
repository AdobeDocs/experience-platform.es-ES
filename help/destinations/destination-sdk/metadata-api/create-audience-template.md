---
description: Esta página ejemplifica la llamada de API utilizada para crear una plantilla de audiencia a través de Adobe Experience Platform Destination SDK.
title: Creación de una plantilla de audiencia
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 3%

---

# Creación de una plantilla de audiencia

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Para algunos destinos creados con Destination SDK, debe crear una configuración de metadatos de audiencia para crear, actualizar o eliminar mediante programación metadatos de audiencia en el destino. Esta página muestra cómo utilizar el extremo de API `/authoring/audience-templates` para crear la configuración.

Para obtener una descripción detallada de las funcionalidades que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1&rbrace;.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantillas de audiencia {#get-started}

Antes de continuar, revisa la [guía de introducción](../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Creación de una plantilla de audiencia {#create}

Puede crear una nueva plantilla de audiencia realizando una solicitud `POST` al extremo `/authoring/audience-templates`.

**Formato de API**

```http
POST /authoring/audience-templates
```

+++Solicitud

La siguiente solicitud crea una nueva plantilla de audiencia, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el extremo `/authoring/audience-templates`. Tenga en cuenta que no tiene que añadir todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "metadataTemplate": {
    "name": "Test Webhook Audience Template",
    "create": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "update": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "PUT",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "delete": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "createDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/createDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "updateDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/updateDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "deleteDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/deleteDestination",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
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
| `name` | Cadena | Nombre de la plantilla de metadatos de audiencia del destino. Este nombre aparece en cualquier mensaje de error específico del socio en la interfaz de usuario de Experience Platform. |
| `url` | Cadena | La dirección URL y el punto final de su API, que se utiliza para crear, actualizar, eliminar o validar audiencias o flujos de datos en su plataforma. Dos ejemplos del sector son: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` y `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Cadena | Método utilizado en el extremo para crear, actualizar, eliminar o validar la audiencia en el destino mediante programación. Por ejemplo: `POST`, `PUT`, `DELETE` |
| `headers.header` | Cadena | Especifica cualquier encabezado HTTP que deba agregarse a la llamada a su API. Por ejemplo, `"Content-Type"` |
| `headers.value` | Cadena | Especifica el valor de los encabezados HTTP que deben agregarse a la llamada a la API. Por ejemplo, `"application/x-www-form-urlencoded"` |
| `requestBody` | Cadena | Especifica el contenido del cuerpo del mensaje que debe enviarse a la API. Los parámetros que se deben agregar al objeto `requestBody` dependen de los campos que acepte su API. Consulte la [documentación de macros admitidas](../functionality/audience-metadata-management.md#macros) para saber qué puede incluir en el cuerpo del mensaje. |
| `responseFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se le llama. Para ver un ejemplo, consulte [ejemplos de plantillas](../functionality/audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de Audiencia. |
| `responseFields.value` | Cadena | Especifique el valor de los campos de respuesta que devuelve la API cuando se llama a. |
| `responseErrorFields.name` | Cadena | Especifique los campos de respuesta que devuelve la API cuando se le llama. Para ver un ejemplo, consulte [ejemplos de plantillas](../functionality/audience-metadata-management.md#examples) en el documento de funcionalidad de metadatos de Audiencia. |
| `responseErrorFields.value` | Cadena | Analiza cualquier mensaje de error devuelto en las respuestas de llamadas de API desde su destino. Estos mensajes de error aparecerán a los usuarios en la interfaz de usuario de Experience Platform. |
| `validations.field` | Cadena | Indica si se deben ejecutar las validaciones para algún campo antes de realizar llamadas de API al destino. Por ejemplo, puede usar `{{validations.accountId}}` para validar el identificador de cuenta del usuario. |
| `validations.regex` | Cadena | Indica cómo se debe estructurar el campo para que se apruebe la validación. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la plantilla de audiencia recién creada.

+++

## Administración de errores de API

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes

Después de leer este documento, sabe cuándo usar plantillas de audiencia y cómo configurar una plantilla de audiencia mediante el extremo de API `/authoring/audience-templates`. Lee [cómo usar Destination SDK para configurar tu destino](../guides/configure-destination-instructions.md) para saber dónde encaja este paso en el proceso de configuración de tu destino.
