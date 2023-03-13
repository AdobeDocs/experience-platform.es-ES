---
description: Obtenga información sobre cómo utilizar Destination SDK para configurar un destino de Amazon S3 con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada.
title: Configure un destino de Amazon S3 con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada.
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: 04e4b0f6b6d84d04d0a24a462383420ebd9a2daf
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Configuración de un [!DNL Amazon S3] destino con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada

## Información general {#overview}

En esta página se describe cómo utilizar Destination SDK para configurar un destino de Amazon S3 con valores predeterminados predefinidos [opciones de formato de archivo](../../server-and-file-configuration.md#file-configuration) y un personalizado [configuración de nombre de archivo](../../file-based-destination-configuration.md#file-name-configuration).

Esta página muestra todas las opciones de configuración disponibles para [!DNL Amazon S3] destinos. Puede editar las configuraciones que se muestran en los pasos siguientes o eliminar ciertas partes de las configuraciones, según sea necesario.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos descritos a continuación, lea la [Introducción al Destination SDK](../../getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Paso 1: Crear un servidor y una configuración de archivo {#create-server-file-configuration}

Comience por usar la variable `/destination-server` extremo para crear un servidor y una configuración de archivo. Para obtener descripciones detalladas de los parámetros de la solicitud HTTP, lea la [especificaciones de configuración de archivos y servidores para destinos basados en archivos](../../server-and-file-configuration.md#s3-example) y el asociado [configuraciones de formato de archivo](../../server-and-file-configuration.md#file-configuration).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitud**

La siguiente solicitud crea una nueva configuración del servidor de destino, configurada por los parámetros proporcionados en la carga útil.
La carga útil siguiente incluye un genérico [!DNL Amazon S3] configuración predeterminada, con predefinido [Formato de archivo CSV](../../server-and-file-configuration.md#file-configuration) Parámetros de configuración que los usuarios pueden definir en la interfaz de usuario de Experience Platform.

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
}'
```

Una respuesta correcta devuelve la nueva configuración del servidor de destino, incluido el identificador único (`instanceId`) de la configuración. Almacene este valor tal como se requiere en el siguiente paso.

## Paso 2: Crear la configuración de destino {#create-destination-configuration}

Después de crear el servidor de destino y la configuración de formato de archivo en el paso anterior, ahora puede utilizar el `/destinations` Punto final de API para crear una configuración de destino.

Para conectar la configuración del servidor en [paso 1](#create-server-file-configuration) a esta configuración de destino, sustituya el `destinationServerId` valor en la solicitud de API siguiente con el `instanceId` valor obtenido al crear el servidor de destino en [paso 1](#create-server-file-configuration).

Para obtener descripciones detalladas de los parámetros utilizados a continuación, consulte las siguientes páginas:

* [Configuración de autenticación](../../authentication-configuration.md#s3)
* [Configuración de destino del lote](../../file-based-destination-configuration.md#batch-configuration)
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
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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

Una respuesta correcta devuelve la nueva configuración de destino, incluido el identificador único (`instanceId`) de la configuración. Almacene este valor como es necesario si necesita realizar más solicitudes HTTP para actualizar la configuración de destino.

## Paso 3: Verificar la interfaz de usuario de Experience Platform {#verify-ui}

En función de las configuraciones anteriores, el catálogo de Experience Platform ahora mostrará una nueva tarjeta de destino privada para que la utilice.

![Grabación de pantalla que muestra la página del catálogo de destinos con una tarjeta de destino seleccionada.](../../assets/destination-card.gif)

En las imágenes y grabaciones que aparecen a continuación, observe cómo aparecen las opciones en la [flujo de trabajo de activación para destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md) coincida con las opciones seleccionadas en la configuración de destino.

Al rellenar detalles sobre el destino, observe cómo aparecen los campos como campos de datos personalizados que se configuran en la configuración.

>[!TIP]
>
>El orden en que se agregan los campos de datos personalizados a la configuración de destino no se refleja en la interfaz de usuario. Los campos de datos del cliente siempre se muestran en el orden mostrado en la grabación de pantalla a continuación.

![Grabación de pantalla que muestra los campos de datos del cliente definidos en la configuración.](../../assets/file-configuration-options.gif)

Al programar intervalos de exportación, observe cómo aparecen los campos configurados en la variable `batchConfig` configuración.
![opciones de programación de exportación](../../assets/file-export-scheduling.png)

Al ver las opciones de configuración de nombre de archivo, observe cómo los campos que aparecen representan el `filenameConfig` opciones que se configuran en la configuración.
![opciones de configuración de nombre](../../assets/file-naming-options.gif)

Si desea ajustar cualquiera de los campos mencionados anteriormente, repita lo siguiente [pasos uno](#create-server-file-configuration) y [dos](#create-destination-configuration) para modificar las configuraciones según sus necesidades.

## Paso 4: (Opcional) Publicar el destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar el destino, utilice el [API de publicación de destino](../../destination-publish-api.md) para enviar la configuración al Adobe para su revisión.

## Paso 5: (Opcional) Documente su destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o integrador de sistemas (SI) que crea un [integración de productos](../../overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](../../docs-framework/documentation-instructions.md) para crear una página de documentación del producto para el destino en [catálogo de destinos de Experience Platform](../../../catalog/overview.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora sabe cómo crear un personalizado [!DNL Amazon S3] destino mediante Destination SDK. A continuación, su equipo puede utilizar el [flujo de trabajo de activación para destinos basados en archivos](../../../ui/activate-batch-profile-destinations.md) para exportar datos al destino.
