---
description: En esta página se muestran y describen los pasos para configurar un destino basado en archivos mediante Destination SDK.
title: Usar Destination SDK para configurar un destino basado en archivos
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 04e4b0f6b6d84d04d0a24a462383420ebd9a2daf
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---

# Usar Destination SDK para configurar un destino basado en archivos

## Información general {#overview}

Esta página describe cómo utilizar la información de [Opciones de configuración en el SDK de destinos](./configuration-options.md) y en otros documentos de referencia de la API y la funcionalidad de Destination SDK para configurar un [destino basado en archivos](../../destinations/destination-types.md#file-based). Los pasos se presentan en orden secuencial a continuación.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos que se ilustran a continuación, lea la [Introducción al Destination SDK](./getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Pasos para utilizar las opciones de configuración de Destination SDK para configurar el destino {#steps}

![Pasos ilustrados del uso de extremos de Destination SDK](./assets/destination-sdk-steps-batch.png)

## Paso 1: Crear un servidor y una configuración de archivo {#create-server-file-configuration}

Comience creando un servidor y una configuración de archivo utilizando `/destinations-server` extremo (leer) [Referencia de API](./destination-server-api.md)).

A continuación se muestra un ejemplo de configuración para una [!DNL Amazon S3] destino. Para configurar otros tipos de destinos basados en archivos, consulte sus correspondientes [configuraciones del servidor](server-and-file-configuration.md).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucketName": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
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
            }
        }
    }
}
```

## Paso 2: Crear la configuración de destino {#create-destination-configuration}

A continuación se muestra un ejemplo de una configuración de destino creada con la variable `/destinations` Extremo de API. Para obtener más información sobre esta configuración, consulte [Configuración de destino](./file-based-destination-configuration.md).

Para conectar el servidor y la configuración de archivo del paso 1 a esta configuración de destino, agregue el ID de instancia del servidor y la configuración de plantilla como `destinationServerId` aquí.

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
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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

## Paso 3: Crear la configuración de metadatos de audiencia {#create-audience-metadata-configuration}

Para algunos destinos, Destination SDK requiere que configure los metadatos de audiencia para crear, actualizar o eliminar audiencias en el destino mediante programación. Consulte [Gestión de metadatos de audiencia](./audience-metadata-management.md) para obtener información sobre cuándo debe configurar esta configuración y cómo hacerlo.

Si utiliza una configuración de metadatos de audiencia, debe conectarla a la configuración de destino creada en el paso 2. Añada el ID de instancia de la configuración de metadatos de audiencia a la configuración de destino como `audienceTemplateId`.

## Paso 4: Configurar la autenticación {#set-up-authentication}

En función de si especifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` en la configuración de destino anterior, puede configurar la autenticación para su destino mediante el `/destination` o el `/credentials` punto final.

* Si ha seleccionado `"authenticationRule": "CUSTOMER_AUTHENTICATION"` en la configuración de destino, consulte las siguientes secciones sobre los tipos de autenticación admitidos por Destination SDK para destinos basados en archivos:

   * [Autenticación de Amazon S3](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Azure Data Lake Storage](authentication-configuration.md#adls)
   * [Almacenamiento de Google Cloud](authentication-configuration.md#gcs)
   * [Autenticación SFTP con clave SSH](authentication-configuration.md#sftp-ssh)
   * [Autenticación SFTP con contraseña](authentication-configuration.md#sftp-password)

* Si ha seleccionado `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte la [Configuración de autenticación](./authentication-configuration.md#when-to-use).


## Paso 5: Prueba del destino {#test-destination}

Después de configurar el destino mediante los extremos de configuración de los pasos anteriores, puede utilizar el [herramienta de prueba de destino](./file-based-destination-testing-overview.md) para probar la integración entre Adobe Experience Platform y el destino.

Como parte del proceso para probar el destino, debe utilizar la interfaz de usuario de Experience Platform para crear segmentos que activará en el destino. Consulte los dos recursos siguientes para obtener instrucciones sobre cómo crear segmentos en Experience Platform:

* [Crear una página de documentación de segmentos](/help/segmentation/ui/overview.md#create-segment)
* [Tutorial de vídeo sobre Creación de un segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Paso 6: Publicación del destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar y probar el destino, utilice el [API de publicación de destino](./destination-publish-api.md) para enviar la configuración al Adobe para su revisión.

## Paso 7: Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o integrador de sistemas (SI) que crea un [integración de productos](./overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md) para crear una página de documentación del producto para el destino en [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md).

## Paso 8: Enviar destino para su revisión por parte del Adobe {#submit-for-review}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Por último, para que el destino se pueda publicar en el catálogo de Experience Platform y sea visible para todos los clientes de Experience Platform, debe enviar oficialmente el destino para que el Adobe lo revise. Encuentre información completa acerca de cómo [enviar para su revisión un destino de productos creado en Destination SDK](/help/destinations/destination-sdk/submit-destination.md).
