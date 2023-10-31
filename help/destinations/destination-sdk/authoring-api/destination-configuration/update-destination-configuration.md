---
description: Esta página ejemplifica la llamada de API utilizada para actualizar una configuración de destino existente a través del Adobe Experience Platform Destination SDK.
title: Actualizar una configuración de destino
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 2%

---

# Actualizar una configuración de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para actualizar una configuración de destino existente mediante `/authoring/destinations` Extremo de API.

>[!TIP]
>
>Cualquier operación de actualización en destinos públicos o producidos solo es visible después de usar el [API de publicación](../../publishing-api/create-publishing-request.md) y enviar la actualización para su revisión por Adobes.

Para obtener una descripción detallada de las capacidades de una configuración de destino, lea los siguientes artículos:

* [Configuración de autenticación del cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autenticación OAuth2](../../functionality/destination-configuration/oauth2-authentication.md)
* [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md)
* [Atributos de IU](../../functionality/destination-configuration/ui-attributes.md)
* [Configuración del esquema](../../functionality/destination-configuration/schema-configuration.md)
* [Configuración del área de nombres de identidad](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Envío de destino](../../functionality/destination-configuration/destination-delivery.md)
* [Configuración de metadatos de audiencia](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuración de metadatos de audiencia](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Política de agregación](../../functionality/destination-configuration/aggregation-policy.md)
* [Configuración por lotes](../../functionality/destination-configuration/batch-configuration.md)
* [Cualificaciones históricas del perfil](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de la API de configuración de destino {#get-started}

Antes de continuar, consulte la [guía de introducción](../../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Actualizar una configuración de destino {#update}

Puede actualizar un [existente](create-destination-configuration.md) configuración de destino realizando una `PUT` solicitud a la `/authoring/destinations` punto final con la carga útil actualizada.

>[!TIP]
>
>Extremo de API: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obtener una configuración de destino existente y su correspondiente `{INSTANCE_ID}`, consulte el artículo sobre [recuperación de una configuración de destino](retrieve-destination-configuration.md).

**Formato de API**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de destino que desea actualizar. Para obtener una configuración de destino existente y su correspondiente `{INSTANCE_ID}`, consulte [Recuperación de una configuración de destino](retrieve-destination-configuration.md). |

+++Solicitud

La siguiente solicitud actualiza el destino que hemos creado en [este ejemplo](create-destination-configuration.md#create) con diferentes `filenameConfig` opciones.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"File type",
         "description":"Select the exported file type.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de destino actualizada.

+++

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo actualizar una configuración de destino a través del Destination SDK `/authoring/destinations` Extremo de API.

Para obtener más información acerca de lo que puede hacer con este extremo, consulte los siguientes artículos:

* [Crear una configuración de destino](create-destination-configuration.md)
* [Recuperación de una configuración de destino](retrieve-destination-configuration.md)
* [Eliminar una configuración de destino](delete-destination-configuration.md)
