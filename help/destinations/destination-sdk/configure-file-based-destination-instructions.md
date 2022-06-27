---
description: En esta página se enumeran y describen los pasos para configurar un destino basado en archivos mediante Destination SDK.
title: (Beta) Usar el Destination SDK para configurar un destino basado en archivos
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: abc9b9857e4a93a334440e855ca0ae562c695df1
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---

# (Beta) Usar el Destination SDK para configurar un destino basado en archivos

## Información general {#overview}

>[!IMPORTANT]
>
>La funcionalidad para configurar y enviar destinos basados en archivos mediante Adobe Experience Platform Destination SDK está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.

Esta página describe cómo utilizar la información de [Opciones de configuración en el SDK de Destinations](./configuration-options.md) y en otros documentos de referencia de API y funcionalidad de Destination SDK para configurar un [destino basado en archivos](../../destinations/destination-types.md#file-based). Los pasos se muestran en orden secuencial a continuación.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos que se ilustran a continuación, lea la [introducción al Destination SDK](./getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Pasos para utilizar las opciones de configuración en Destination SDK para configurar el destino {#steps}

![Pasos ilustrados para utilizar extremos de Destination SDK](./assets/destination-sdk-steps-batch.png)

## Paso 1: Creación de una configuración de servidor y archivo {#create-server-file-configuration}

Comience creando un servidor y una configuración de archivo utilizando `/destinations-server` punto final (leer [Referencia de API](./destination-server-api.md)).

A continuación se muestra un ejemplo de configuración para un [!DNL Amazon S3] destino. Para configurar otros tipos de destinos basados en archivos, consulte sus [configuraciones del servidor](server-and-file-configuration.md).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

## Paso 2: Crear configuración de destino {#create-destination-configuration}

A continuación se muestra un ejemplo de una configuración de destino creada mediante el uso de la variable `/destinations` extremo de API. Para obtener más información sobre esta configuración, consulte [Configuración de destino](./file-based-destination-configuration.md).

Para conectar el servidor y la configuración de archivo en el paso 1 a esta configuración de destino, añada el ID de instancia del servidor y la configuración de plantilla como `destinationServerId` aquí.

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
        "category": "S3",
        "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Paso 3: Crear configuración de metadatos de audiencia {#create-audience-metadata-configuration}

Para algunos destinos, Destination SDK requiere que configure una configuración de metadatos de audiencia para crear, actualizar o eliminar audiencias de forma programada en el destino. Consulte [Gestión de metadatos de audiencia](./audience-metadata-management.md) para obtener información sobre cuándo debe configurar esta configuración y cómo hacerlo.

Si utiliza una configuración de metadatos de audiencia, debe conectarla a la configuración de destino que creó en el paso 2. Añada el ID de instancia de la configuración de metadatos de audiencia a la configuración de destino como `audienceTemplateId`.

## Paso 4: Configuración de la autenticación {#set-up-authentication}

Dependiendo de si especifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` en la configuración de destino anterior, puede configurar la autenticación para el destino utilizando la variable `/destination` o `/credentials` punto final.

* Si ha seleccionado `"authenticationRule": "CUSTOMER_AUTHENTICATION"` en la configuración de destino, consulte las secciones siguientes para ver los tipos de autenticación admitidos por el Destination SDK para destinos basados en archivos:

   * [Autenticación de Amazon S3](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Almacenamiento de Azure Data Lake](authentication-configuration.md#adls)
   * [Almacenamiento en la nube de Google](authentication-configuration.md#gcs)
   * [Autenticación SFTP con clave SSH](authentication-configuration.md#sftp-ssh)
   * [Autenticación SFTP con contraseña](authentication-configuration.md#sftp-password)

* Si ha seleccionado `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte [Configuración de autenticación](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## Paso 5: Publicar su destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar y probar el destino, use la variable [API de publicación de destino](./destination-publish-api.md) para enviar la configuración a Adobe para su revisión.

## Paso 6: Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea un [integración de productos](./overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md) para crear una página de documentación de producto para su destino en el [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md).
