---
description: Aprenda a utilizar Destination SDK para configurar un destino de Amazon S3 con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada.
title: (Beta) Configure un destino de Amazon S3 con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada.
source-git-commit: 1e6515bf4fe34258194f56d341e477a02a1c31be
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# (Beta) Configure un [!DNL Amazon S3] destino con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada

## Información general {#overview}

>[!IMPORTANT]
>
>Actualmente, la funcionalidad para configurar destinos basados en archivos mediante Adobe Experience Platform Destination SDK está en versión beta. La documentación y la funcionalidad están sujetas a cambios.

En esta página se describe cómo utilizar Destination SDK para configurar un destino de Amazon S3 con un destino predefinido y predeterminado [opciones de formato de archivo](../../server-and-file-configuration.md#file-configuration) y un [configuración de nombre de archivo](../../file-based-destination-configuration.md#file-name-configuration).

Esta página muestra todas las opciones de configuración disponibles para [!DNL Amazon S3] destinos. Puede editar las configuraciones que se muestran en los pasos siguientes o eliminar ciertas partes de las configuraciones, según sea necesario.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos descritos a continuación, lea la [introducción al Destination SDK](../../getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Paso 1: Creación de una configuración de servidor y archivo {#create-server-file-configuration}

Comience por usar la variable `/destination-server` para crear una configuración de servidor y archivo. Para obtener descripciones detalladas de los parámetros de la solicitud HTTP, lea la [especificaciones de configuración de archivos y servidores para destinos basados en archivos](../../server-and-file-configuration.md#s3-example) y el [configuraciones de formato de archivo](../../server-and-file-configuration.md#file-configuration).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitud**

La siguiente solicitud crea una nueva configuración del servidor de destino, configurada por los parámetros proporcionados en la carga útil.
La carga útil siguiente incluye un [!DNL Amazon S3] configuración, con predefinido, predeterminado [Formato del archivo CSV](../../server-and-file-configuration.md#file-configuration) parámetros de configuración que los usuarios pueden definir en la interfaz de usuario del Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
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
}'
```

Una respuesta correcta devuelve la nueva configuración del servidor de destino, incluido el identificador único (`instanceId`) de la configuración. Almacene este valor como sea necesario en el siguiente paso.

## Paso 2: Crear configuración de destino {#create-destination-configuration}

Después de crear el servidor de destino y la configuración de formato de archivo en el paso anterior, ahora puede usar la variable `/destinations` extremo de API para crear una configuración de destino.

Para conectar la configuración del servidor en [paso 1](#create-server-file-configuration) a esta configuración de destino, reemplace la variable `destinationServerId` en la solicitud de API que aparece a continuación con la variable `instanceId` valor obtenido al crear el servidor de destino en [paso 1](#create-server-file-configuration).

Para obtener descripciones detalladas de los parámetros utilizados a continuación, consulte las páginas siguientes:

* [Configuración de autenticación](../../authentication-configuration.md#s3)
* [Configuración de destino de lote](../../file-based-destination-configuration.md#batch-configuration)
* [Operaciones de API de configuración de destino basadas en archivos](../../destination-configuration-api.md#create-file-based)

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "releaseNotes":"Amazon S3 destination with predefined CSV formatting options",
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
      "flowRunsSupported":true,
      "monitoringSupported":true,
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
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

Una respuesta correcta devuelve la nueva configuración de destino, incluido el identificador único (`instanceId`) de la configuración. Almacene este valor tal como es necesario si necesita realizar más solicitudes HTTP para actualizar la configuración de destino.

## Paso 3: Verificación de la interfaz de usuario del Experience Platform {#verify-ui}

En función de las configuraciones anteriores, el catálogo de Experience Platform ahora mostrará una nueva tarjeta de destino privada que puede usar.

![Grabación de pantalla que muestra la página del catálogo de destinos con una tarjeta de destino seleccionada.](../../assets/destination-card.gif)

En las imágenes y grabaciones siguientes, observe cómo las opciones de la sección [flujo de trabajo de activación para destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md) coincida con las opciones que ha seleccionado en la configuración de destino.

Cuando rellene los detalles sobre el destino, observe cómo los campos mostrados son los campos de datos personalizados que configuró en la configuración.

>[!TIP]
>
>El orden en que se agregan los campos de datos personalizados a la configuración de destino no se refleja en la interfaz de usuario. Los campos de datos del cliente siempre se muestran en el orden mostrado en la grabación de pantalla siguiente.

![Registro de pantalla que muestra los campos de datos del cliente definidos en la configuración.](../../assets/file-configuration-options.gif)

Al programar intervalos de exportación, observe cómo los campos mostrados son los campos configurados en la variable `batchConfig` configuración.
![exportar opciones de programación](../../assets/file-export-scheduling.png)

Cuando vea las opciones de configuración del nombre del archivo, observe cómo los campos mostrados representan la variable `filenameConfig` que configure en la configuración.
![opciones de configuración del nombre de archivo](../../assets/file-naming-options.gif)

Si desea ajustar cualquiera de los campos mencionados anteriormente, repita [paso uno](#create-server-file-configuration) y [two](#create-destination-configuration) para modificar las configuraciones según sus necesidades.

## Paso 4: (Opcional) Publique el destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar el destino, use la variable [API de publicación de destino](../../destination-publish-api.md) para enviar la configuración a Adobe para su revisión.

## Paso 5: (Opcional) Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea un [integración de productos](../../overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](../../docs-framework/documentation-instructions.md) para crear una página de documentación de producto para su destino en el [catálogo de destinos de Experience Platform](../../../catalog/overview.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora sabe cómo crear una [!DNL Amazon S3] destino mediante Destination SDK. A continuación, su equipo puede usar la variable [flujo de trabajo de activación para destinos basados en archivos](../../../ui/activate-batch-profile-destinations.md) para exportar datos al destino.