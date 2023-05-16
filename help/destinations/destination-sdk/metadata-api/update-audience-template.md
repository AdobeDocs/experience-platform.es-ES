---
description: Esta página ejemplifica la llamada de API utilizada para actualizar una plantilla de audiencia a través del Adobe Experience Platform Destination SDK.
title: Actualizar una plantilla de audiencia
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 2%

---


# Actualizar una plantilla de audiencia

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para actualizar una plantilla de audiencia mediante el uso de `/authoring/audience-templates` extremo de API.

Para obtener una descripción detallada de las capacidades que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantilla de audiencia {#get-started}

Antes de continuar, revise la [guía de introducción](../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Actualizar una plantilla de audiencia {#create}

Puede actualizar una [existente](create-audience-template.md) plantilla de audiencia haciendo una `PUT` solicitud al `/authoring/audience-templates` con la carga útil actualizada.

Para obtener una plantilla de audiencia existente y su correspondiente `{INSTANCE_ID}`, consulte el artículo sobre [recuperación de una plantilla de audiencia](retrieve-audience-template.md).

**Formato de API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la plantilla de audiencia que desea actualizar. Para obtener una plantilla de audiencia existente y su correspondiente `{INSTANCE_ID}`, consulte [Recuperación de una plantilla de audiencia](retrieve-audience-template.md). |

La siguiente solicitud actualiza una plantilla de metadatos de audiencia existente, configurada por los parámetros proporcionados en la carga útil.

+++Solicitud

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
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
}'
```

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la plantilla de audiencia actualizada.

+++

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cuándo usar plantillas de audiencia y cómo actualizar una plantilla de audiencia usando la variable `/authoring/audience-templates` extremo de API. Lectura [cómo usar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
