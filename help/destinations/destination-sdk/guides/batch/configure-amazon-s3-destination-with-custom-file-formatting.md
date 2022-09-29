---
description: Aprenda a utilizar Destination SDK para configurar un destino de Amazon S3 con opciones de formato y nombre de archivo personalizados.
title: Configure un destino de Amazon S3 con opciones de formato y nombre de archivo personalizados.
exl-id: eed73572-5050-44fa-ba16-90729c65495e
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 1%

---

# Configuración de un destino de Amazon S3 con opciones de formato y nombre de archivo personalizados

## Información general {#overview}

En esta página se describe cómo utilizar Destination SDK para configurar un destino de Amazon S3 con [opciones de formato de archivo](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) y un [configuración de nombre de archivo](/help/destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration).

Esta página muestra todas las opciones de configuración disponibles para los destinos de Amazon S3. Puede editar las configuraciones que se muestran en los pasos siguientes o eliminar ciertas partes de las configuraciones, según sea necesario.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos descritos a continuación, lea la [introducción al Destination SDK](/help/destinations/destination-sdk/getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Paso 1: Creación de una configuración de servidor y archivo {#create-server-file-configuration}

Comience por usar la variable `/destination-server` para crear una configuración de servidor y archivo. Para obtener descripciones detalladas de los parámetros de la solicitud HTTP, lea la [especificaciones de configuración de archivos y servidores para destinos basados en archivos](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example) y el [configuraciones de formato de archivo](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitud**

La siguiente solicitud crea una nueva configuración del servidor de destino, configurada por los parámetros proporcionados en la carga útil.
La carga útil siguiente incluye una configuración genérica de Amazon S3, con [Formato del archivo CSV](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) parámetros de configuración que los usuarios pueden definir en la interfaz de usuario del Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
   "name":"Amazon S3 destination server with custom file formatting options",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.compression}}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.sep}}"
         },
         "encoding":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.encoding}}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quote}}"
         },
         "quoteAll":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quoteAll}}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escape}}"
         },
         "escapeQuotes":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escapeQuotes}}"
         },
         "header":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.header}}"
         },
         "ignoreLeadingWhiteSpace":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.ignoreLeadingWhiteSpace}}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.nullValue}}"
         },
         "dateFormat":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         },
         "charToEscapeQuoteEscaping":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.charToEscapeQuoteEscaping}}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         }
      }
   }
}'
```

Una respuesta correcta devuelve la nueva configuración del servidor de destino, incluido el identificador único (`instanceId`) de la configuración. Almacene este valor como sea necesario en el siguiente paso.

## Paso 2: Crear configuración de destino {#create-destination-configuration}

Después de crear el servidor de destino y la configuración de formato de archivo en el paso anterior, ahora puede usar la variable `/destinations` extremo de API para crear una configuración de destino.

Para conectar la configuración del servidor en [paso 1](#create-server-file-configuration) a esta configuración de destino, reemplace la variable `destinationServerId` en la solicitud de API que aparece a continuación con el valor obtenido al crear el servidor de destino en [paso 1](#create-server-file-configuration).

Para obtener descripciones detalladas de los parámetros utilizados a continuación, consulte las páginas siguientes:

* [Configuración de autenticación](/help/destinations/destination-sdk/authentication-configuration.md#s3)
* [Configuración de destino de lote](/help/destinations/destination-sdk/file-based-destination-configuration.md#batch-configuration)
* [Operaciones de API de configuración de destino basadas en archivos](/help/destinations/destination-sdk/destination-configuration-api.md#create-file-based)

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
   "name":"Amazon S3 destination with custom file formatting options and custom file name configuration",
   "description":"Amazon S3 destination with custom file formatting options and custom file name configuration",
   "releaseNotes":"Amazon S3 destination with custom file formatting options and custom file name configuration",
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
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
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
>El orden en que se agregan los campos de datos personalizados a la configuración de destino no se refleja en la interfaz de usuario. Los campos de datos personalizados siempre se muestran en el orden mostrado en la grabación de pantalla siguiente.

![rellene los detalles de destino](../../assets/file-configuration-options.gif)

Al programar intervalos de exportación, observe cómo los campos mostrados son los campos configurados en la variable `batchConfig` configuración.
![exportar opciones de programación](../../assets/file-export-scheduling.png)

Cuando vea las opciones de configuración del nombre del archivo, observe cómo los campos mostrados representan la variable `filenameConfig` que configure en la configuración.
![opciones de configuración del nombre de archivo](../../assets/file-naming-options.gif)

Si desea ajustar cualquiera de los campos mencionados anteriormente, repita [paso uno](#create-server-file-configuration) y [two](#create-destination-configuration) para modificar las configuraciones según sus necesidades.

## Paso 4: (Opcional) Publique el destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar el destino, use la variable [API de publicación de destino](/help/destinations/destination-sdk/destination-publish-api.md) para enviar la configuración a Adobe para su revisión.

## Paso 5: (Opcional) Documentar el destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea un [integración de productos](/help/destinations/destination-sdk/overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md) para crear una página de documentación de producto para su destino en el [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora sabe cómo crear una [!DNL Amazon S3] destino mediante Destination SDK. A continuación, su equipo puede usar la variable [flujo de trabajo de activación para destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md) para exportar datos al destino.
