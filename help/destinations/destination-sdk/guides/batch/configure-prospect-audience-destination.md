---
description: Obtenga información sobre cómo utilizar Destination SDK para configurar un destino basado en archivos con el fin de exportar audiencias potenciales a una ubicación de almacenamiento.
title: Configurar un destino basado en archivos para exportar audiencias potenciales a una ubicación de almacenamiento
exl-id: 052fd185-294a-4c1d-8d82-12b27b661e22
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# Configurar un destino basado en archivos para exportar audiencias potenciales a una ubicación de almacenamiento

## Información general {#overview}

En esta página se describe cómo usar Destination SDK para configurar un destino basado en archivos con [opciones de formato de archivo](configure-file-formatting-options.md) personalizadas y una [configuración de nombre de archivo](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) personalizada para exportar [audiencias de clientes potenciales](/help/destinations/ui/activate-prospect-audiences.md). Los ejemplos de esta guía describen cómo exportar audiencias de perfiles de clientes potenciales a una ubicación de Amazon S3.

También puede configurar STFP u otras ubicaciones de almacenamiento para exportar audiencias de clientes potenciales. La parte importante que hay que recordar es agregar el siguiente fragmento a la configuración de destino en el [paso 2](#create-destination-configuration) para habilitar el [flujo de trabajo para exportar audiencias de clientes potenciales](/help/destinations/ui/activate-prospect-audiences.md) al destino.

```json
  "sources": [
    "UNIFIED_PROFILE_PROSPECTS"
  ],
```

Para obtener descripciones detalladas de los parámetros utilizados a continuación, consulte [opciones de configuración en Destinations SDK](../../functionality/configuration-options.md).

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos descritos a continuación, lea la página de [introducción al Destination SDK](../../getting-started.md) para obtener información sobre cómo obtener las credenciales de autenticación necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Paso 1: Crear un servidor y una configuración de archivo {#create-server-file-configuration}

Comience por usar el extremo `/destination-server` para [crear un servidor y una configuración de archivo](../../authoring-api/destination-server/create-destination-server.md).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitud**

La siguiente solicitud crea una nueva configuración del servidor de destino, configurada por los parámetros proporcionados en la carga útil.
La carga útil siguiente incluye una configuración genérica de Amazon S3, con [formato de archivo CSV](../../functionality/destination-server/file-formatting.md) personalizado que los usuarios pueden definir en la interfaz de usuario del Experience Platform.

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
         "value":"{{customerData.bucketName}}"
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

Una respuesta correcta devuelve la nueva configuración del servidor de destino, incluido el identificador único (`instanceId`) de la configuración. Almacene este valor tal como se requiere en el siguiente paso.

## Paso 2: Crear la configuración de destino {#create-destination-configuration}

Después de crear el servidor de destino y la configuración de formato de archivo en el paso anterior, puede usar el extremo de la API `/destinations` para crear una configuración de destino.

Para conectar la configuración del servidor en [paso 1](#create-server-file-configuration) a esta configuración de destino, reemplace el valor `destinationServerId` de la solicitud de API siguiente por el valor obtenido al crear el servidor de destino en [paso 1](#create-server-file-configuration).

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
   "name":"Amazon S3 destination to export prospect audiences",
   "description":"Amazon S3 destination to export prospect audiences",
   "status":"TEST",
   "sources": [
    "UNIFIED_PROFILE_PROSPECTS"
   ],
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
         "DAILY_FULL_EXPORT"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
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

![Grabación de pantalla que muestra la página del catálogo de destinos con una tarjeta de destino seleccionada.](../../assets/guides/batch/destination-card.gif)

En las imágenes y grabaciones siguientes, observe cómo las opciones del flujo de trabajo de [activación para destinos basados en archivos](../../../ui/activate-batch-profile-destinations.md) coinciden con las opciones que seleccionó en la configuración de destino.

Al rellenar detalles sobre el destino, observe cómo aparecen los campos como campos de datos personalizados que se configuran en la configuración.

>[!TIP]
>
>El orden en que se agregan los campos de datos personalizados a la configuración de destino no se refleja en la interfaz de usuario. Los campos de datos personalizados siempre se muestran en el orden mostrado en la grabación de pantalla a continuación.

![rellenar detalles de destino](../../assets/guides/batch/file-configuration-options.gif)

Al programar intervalos de exportación, observe cómo aparecen los campos configurados en la configuración `batchConfig`.
![opciones de programación de exportación](../../assets/guides/batch/ui-view-scheduling-prospect-destination.png)

Al ver las opciones de configuración del nombre de archivo, observe cómo los campos que aparecen representan las opciones de `filenameConfig` que configuró en la configuración.
![opciones de configuración de nombre de archivo](../../assets/guides/batch/file-naming-options.gif)

Si desea ajustar cualquiera de los campos mencionados anteriormente, repita los [pasos uno](#create-server-file-configuration) y [dos](#create-destination-configuration) para modificar las configuraciones según sus necesidades.

## Paso 4: (Opcional) Publish su destino {#publish-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Después de configurar el destino, usa la [API de publicación de destino](../../publishing-api/create-publishing-request.md) para enviar la configuración al Adobe y revisarla.

## Paso 5: (Opcional) Documente su destino {#document-destination}

>[!NOTE]
>
>Este paso no es necesario si está creando un destino privado para su propio uso y no desea publicarlo en el catálogo de destinos para que lo utilicen otros clientes.

Si es un proveedor de software independiente (ISV) o integrador de sistemas (SI) que crea una [integración de productos](../../overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](../../docs-framework/documentation-instructions.md) para crear una página de documentación de productos para su destino en el [catálogo de destinos de Experience Platform](../../../catalog/overview.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora sabe cómo usar Destination SDK para crear un destino [!DNL Amazon S3] personalizado con el fin de exportar audiencias de clientes potenciales.
