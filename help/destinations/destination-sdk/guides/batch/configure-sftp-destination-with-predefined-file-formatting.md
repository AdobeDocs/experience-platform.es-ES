---
description: Obtenga información sobre cómo utilizar Destination SDK para configurar un destino SFTP con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada.
title: Configure un destino SFTP con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 1%

---

# Configurar un destino SFTP con opciones de formato de archivo predefinidas y configuración de nombre de archivo personalizada

## Información general {#overview}

En esta página se describe cómo usar el Destination SDK para configurar un destino SFTP con [opciones de formato de archivo](configure-file-formatting-options.md) predeterminadas y una [configuración de nombre de archivo](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) personalizada.

Esta página muestra todas las opciones de configuración disponibles para los destinos SFTP. Puede editar las configuraciones que se muestran en los pasos siguientes o eliminar ciertas partes de las configuraciones, según sea necesario.

Para obtener descripciones detalladas de los parámetros utilizados a continuación, consulte [opciones de configuración en Destinations SDK](../../functionality/configuration-options.md).

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos descritos a continuación, lea la página de [introducción al Destination SDK](../../getting-started.md) para obtener información sobre cómo obtener las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

## Paso 1: Crear un servidor y una configuración de archivo {#create-server-file-configuration}

Comience por usar el extremo `/destination-server` para [crear un servidor y una configuración de archivo](../../authoring-api/destination-server/create-destination-server.md).

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitud**

La siguiente solicitud crea una nueva configuración del servidor de destino, configurada por los parámetros proporcionados en la carga útil.
La carga útil siguiente incluye una configuración SFTP genérica, con [formato de archivo CSV](../../functionality/destination-server/file-formatting.md) predefinido y predeterminado, parámetros de configuración que los usuarios pueden definir en la interfaz de usuario del Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "SFTP destination with predefined CSV formatting options",
    "destinationServerType": "FILE_BASED_SFTP",
    "fileBasedSFTPDestination": {
        "hostname": {
            "templatingStrategy": "NONE",
            "value": "{{customerData.hostname}}"
        },
        "rootDirectory": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.remotePath}}"
        },
        "port": 22
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
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      },
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"remotePath",
         "title":"Root directory",
         "description":"Enter root directory",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"hostname",
         "title":"Hostname",
         "description":"Enter hostname",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-sftp-en",
      "category":"SFTP",
      "connectionType":"SFTP",
      "monitoringSupported":true,
      "flowRunsSupported":true,
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
         "destinationServerId":"{{instanceID of your destination server}}"
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

![Grabación de pantalla que muestra la página del catálogo de destinos con una tarjeta de destino seleccionada.](../../assets/guides/batch/destination-card.gif)

En las imágenes y grabaciones siguientes, observe cómo las opciones del flujo de trabajo de [activación para destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md) coinciden con las opciones que seleccionó en la configuración de destino.

Al rellenar detalles sobre el destino, observe cómo aparecen los campos como campos de datos personalizados que se configuran en la configuración.

>[!TIP]
>
>El orden en que se agregan los campos de datos personalizados a la configuración de destino no se refleja en la interfaz de usuario. Los campos de datos personalizados siempre se muestran en el orden mostrado en la grabación de pantalla a continuación.

![rellenar detalles de destino](../../assets/guides/batch/file-configuration-options.gif)

Al programar intervalos de exportación, observe cómo aparecen los campos configurados en la configuración `batchConfig`.
![opciones de programación de exportación](../../assets/guides/batch/file-export-scheduling.png)

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

Al leer este artículo, ahora sabe cómo crear un destino SFTP personalizado con Destination SDK. A continuación, su equipo puede usar el flujo de trabajo de [activación para destinos basados en archivos](../../../ui/activate-batch-profile-destinations.md) para exportar datos al destino.
