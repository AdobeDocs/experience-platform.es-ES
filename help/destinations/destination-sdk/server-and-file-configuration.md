---
description: Las especificaciones de configuración de servidor y archivo para destinos basados en archivos se pueden configurar en Adobe Experience Platform Destination SDK a través del extremo /destination-servers .
title: (Beta) Opciones de configuración para especificaciones de servidor de destino basadas en archivos
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 3c8ad296ab9f0ce62743466ca8823b13c4545a9d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 10%

---

# (Beta) Configuración de servidor y archivo para especificaciones de servidor de destino basadas en archivos

## Información general {#overview}

>[!IMPORTANT]
>
>La funcionalidad para configurar y enviar destinos basados en archivos mediante Adobe Experience Platform Destination SDK está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.

Esta página detalla todas las opciones de configuración del servidor para los servidores de destino basados en archivos y le indica cómo configurar varias opciones de configuración de archivos para los usuarios que exportan archivos desde el Experience Platform al destino.

Las especificaciones de configuración del servidor y del archivo para los destinos basados en archivos se pueden configurar en Adobe Experience Platform Destination SDK mediante la variable `/destination-servers` punto final. Lectura [Operaciones de extremo de API del servidor de destino](./destination-server-api.md) para obtener una lista completa de las operaciones que puede realizar en el punto final.

## Especificación de servidor de destino Amazon S3 basado en archivos {#s3-example}

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
       // See the file formatting configuration section further below on this page
    }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Amazon S3], configure esto como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Cadena | El nombre del [!DNL Amazon S3] contenedor que utilizará este destino. |
| `fileBasedS3Destination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

## Especificación de servidor de destino SFTP basado en archivos {#sftp-example}

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL SFTP] destinos, configúrelo en `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Cadena | El directorio raíz del almacenamiento de destino. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Cadena | El nombre de host del almacenamiento de destino. |
| `port` | Número entero | Puerto del servidor de archivos SFTP. |
| `encryptionMode` | Cadena | Indica si se utiliza el cifrado de archivos. Valores compatibles: <ul><li>PGP</li><li>Ninguna</li></ul> |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

## Basado en archivos [!DNL Azure Data Lake Storage] ([!DNL ADLS]) especificación del servidor de destino {#adls-example}

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, configúrelo en `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

## Basado en archivos [!DNL Azure Blob Storage] especificación del servidor de destino {#blob-example}

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Blob Storage] destinos, configúrelo en `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Cadena | El nombre del [!DNL Azure Blob Storage] contenedor que utilizará este destino. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

## Basado en archivos [!DNL Data Landing Zone] ([!DNL DLZ]) especificación del servidor de destino {#dlz-example}

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Data Landing Zone] destinos, configúrelo en `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Cadena | *Requerido.*  En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

## Basado en archivos [!DNL Google Cloud Storage] especificación del servidor de destino {#gcs-example}

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
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
      // See the file formatting configuration section further below on this page
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Google Cloud Storage] destinos, configúrelo en `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Cadena | *Requerido.*  En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Cadena | El nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

## Configuración de formato de archivo {#file-configuration}

En esta sección se describe la configuración de formato de archivo para la exportación `CSV` archivos. Puede modificar varias propiedades de los archivos exportados para que coincidan con los requisitos del sistema de recepción de archivos de su lado, a fin de leer e interpretar de forma óptima los archivos recibidos del Experience Platform.

>[!NOTE]
>
>Las opciones de CSV solo se admiten al exportar archivos CSV. La variable `fileConfigurations` no es obligatoria al configurar un nuevo servidor de destino. Si no pasa ningún valor en la llamada de API para las opciones de CSV, se utilizarán los predeterminados de la siguiente tabla.

```json
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
        },
        "maxFileRowCount":5000000
    }
```

| Campo | Obligatorio/Opcional | Descripción | Valor predeterminado |
|---|---|---|---|
| `compression.value` | Opcional | Códec de compresión que se utilizará al guardar datos en un archivo. Valores compatibles: `none`, `bzip2`, `gzip`, `lz4`y `snappy`. | `none` |
| `fileType.value` | Opcional | Especifica el formato del archivo de salida. Valores compatibles: `csv`, `parquet`y `json`. | `csv` |
| `csvOptions.quote.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utiliza para escapar los valores entre comillas, donde el separador puede formar parte del valor. | `null` |
| `csvOptions.quoteAll.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si todos los valores deben estar siempre entre comillas. De forma predeterminada, solo se escapan los valores que contienen un carácter de comillas. | `false` |
| `csvOptions.escape.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utiliza para las comillas de escape dentro de un valor ya citado. | `\` |
| `csvOptions.escapeQuotes.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si los valores que contienen comillas siempre se deben incluir entre comillas. El valor predeterminado es omitir todos los valores que contengan un carácter de comillas. | `true` |
| `csvOptions.header.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se deben escribir los nombres de las columnas como primera línea. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se recortan los espacios en blanco iniciales de los valores. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se recortarán los espacios en blanco al final de los valores. | `true` |
| `csvOptions.nullValue.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la representación de cadena de un valor nulo. | `""` |
| `csvOptions.dateFormat.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica el formato de fecha. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la cadena que indica un formato de marca de tiempo. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utilizará para escapar el escape del carácter de comillas. | `\` cuando los caracteres escape y comillas son diferentes. `\0` cuando el carácter escape y comillas son iguales. |
| `csvOptions.emptyValue.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define la representación de cadena de un valor vacío. | `""` |
| `csvOptions.lineSep.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define el separador de líneas que debe utilizarse para escribir. La longitud máxima es 1 carácter. | `\n` |
| `maxFileRowCount` | Opcional | Número máximo de filas que puede contener el archivo exportado. Configúrelo según los requisitos de tamaño de archivo de la plataforma de destino. | N/A |
