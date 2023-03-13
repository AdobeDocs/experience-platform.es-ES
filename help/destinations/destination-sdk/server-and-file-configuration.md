---
description: Las especificaciones de configuración de servidor y archivo para destinos basados en archivos se pueden configurar en Adobe Experience Platform Destination SDK a través del punto de conexión /destination-servers.
title: Opciones de configuración para especificaciones del servidor de destino basadas en archivos
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 8%

---

# Configuración de servidor y archivo para especificaciones del servidor de destino basadas en archivos

## Información general {#overview}

Esta página detalla todas las opciones de configuración del servidor para los servidores de destino basados en archivos y muestra cómo configurar varias opciones de configuración de archivos para los usuarios que exportan archivos desde el Experience Platform al destino.

Las especificaciones de configuración del servidor y los archivos para los destinos basados en archivos se pueden configurar en Adobe Experience Platform Destination SDK mediante el `/destination-servers` punto final. Leer [Operaciones de extremo de API de servidor de destino](./destination-server-api.md) para obtener una lista completa de las operaciones que puede realizar en el extremo.

Las secciones siguientes incluyen especificaciones del servidor de destino específicas para cada tipo de destino de lote admitido en el Destination SDK.

## Especificaciones del servidor de destino Amazon S3 basado en archivos {#s3-example}

El siguiente ejemplo muestra una configuración de servidor de destino correcta para un destino de Amazon S3.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Amazon S3], establezca esto como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Cadena | El nombre del [!DNL Amazon S3] contenedor que utilizará este destino. |
| `fileBasedS3Destination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

{style="table-layout:auto"}

## Especificaciones del servidor de destino SFTP basado en archivos {#sftp-example}

El siguiente ejemplo muestra una configuración de servidor de destino correcta para un destino SFTP.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL SFTP] destinos, establezca esto en `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Cadena | El directorio raíz del almacenamiento de destino. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Cadena | El nombre de host del almacenamiento de destino. |
| `port` | Número entero | El puerto del servidor de archivos SFTP. |
| `encryptionMode` | Cadena | Indica si se debe utilizar el cifrado de archivos. Valores compatibles: <ul><li>PGP</li><li>Ninguna</li></ul> |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

{style="table-layout:auto"}

## Basado en archivos [!DNL Azure Data Lake Storage] ([!DNL ADLS]) especificación del servidor de destino {#adls-example}

El siguiente ejemplo muestra una configuración de servidor de destino correcta para un [!DNL Azure Data Lake Storage] destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, establezca esto en `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

{style="table-layout:auto"}

## Basado en archivos [!DNL Azure Blob Storage] especificación del servidor de destino {#blob-example}

El siguiente ejemplo muestra una configuración de servidor de destino correcta para un [!DNL Azure Blob Storage] destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Blob Storage] destinos, establezca esto en `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Cadena | El nombre del [!DNL Azure Blob Storage] contenedor que utilizará este destino. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

{style="table-layout:auto"}

## Basado en archivos [!DNL Data Landing Zone] ([!DNL DLZ]) especificación del servidor de destino {#dlz-example}

El siguiente ejemplo muestra una configuración de servidor de destino correcta para un [!DNL Data Landing Zone] ([!DNL DLZ]) destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Data Landing Zone] destinos, establezca esto en `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Cadena | *Requerido.*  En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

{style="table-layout:auto"}

## Basado en archivos [!DNL Google Cloud Storage] especificación del servidor de destino {#gcs-example}

El siguiente ejemplo muestra una configuración de servidor de destino correcta para un [!DNL Google Cloud Storage] destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Google Cloud Storage] destinos, establezca esto en `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Cadena | *Requerido.*  En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Cadena | El nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuración de formato de archivo](#file-configuration) para obtener explicaciones detalladas sobre esta sección. |

{style="table-layout:auto"}

## Configuración de formato de archivo {#file-configuration}

En esta sección se describe la configuración de formato de archivo para el archivo exportado `CSV` archivos. Puede modificar varias propiedades de los archivos exportados para que coincidan con los requisitos del sistema de recepción de archivos de su lado, a fin de leer e interpretar de forma óptima los archivos recibidos del Experience Platform.

>[!NOTE]
>
>Las opciones CSV solo se admiten al exportar archivos CSV. El `fileConfigurations` no es obligatoria al configurar un nuevo servidor de destino. Si no pasa ningún valor en la llamada de API para las opciones de CSV, los predeterminados de la [tabla de referencia más abajo](#file-formatting-reference-and-example) se utilizará.

### Las configuraciones de archivo con las opciones CSV y `templatingStrategy` establezca en `NONE` {#file-configuration-templating-none}

En el ejemplo de configuración que se muestra a continuación, todas las opciones de CSV son fijas. La configuración de exportación definida en cada una de las `csvOptions` los parámetros son finales y los usuarios no pueden modificarlos.

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
            }
        },
        "maxFileRowCount":5000000
    }
```

### Las configuraciones de archivo con las opciones CSV y `templatingStrategy` establezca en `PEBBLE_V1` {#file-configuration-templating-pebble}

En el ejemplo de configuración que se muestra a continuación, ninguna de las opciones de CSV es fija. El `value` en cada una de las `csvOptions` parámetros se configura en un campo de datos del cliente correspondiente a través de la variable `/destinations` punto final (por ejemplo, `customerData.quote` para el `quote` opciones de formato de archivo ) y los usuarios pueden utilizar la interfaz de usuario de Experience Platform para seleccionar entre las distintas opciones que configure en el campo correspondiente datos de cliente.

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### Referencia completa y ejemplos de las opciones de formato de archivo compatibles {#file-formatting-reference-and-example}

>[!TIP]
>
>Las opciones de formato de archivo CSV que se describen a continuación también están documentadas en la [Guía de Apache Spark para archivos CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Las descripciones utilizadas a continuación se toman de la guía de Apache Spark.

A continuación se muestra una referencia completa de todas las opciones de formato de archivo disponibles en Destination SDK, junto con ejemplos de salida para cada opción.

| Campo | Obligatorio/Opcional | Descripción | Valor predeterminado | Ejemplo de salida 1 | Ejemplo de salida 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Requerido | Para cada opción de formato de archivo que configure, es necesario agregar el parámetro `templatingStrategy`, que puede tener dos valores: <br><ul><li>`NONE`: utilice este valor si no planea permitir que los usuarios seleccionen entre valores diferentes para una configuración. Consulte [esta configuración](#file-configuration-templating-none) por ejemplo, donde las opciones de formato de archivo son fijas.</li><li>`PEBBLE_V1`: utilice este valor si desea permitir que los usuarios seleccionen entre valores diferentes para una configuración. En este caso, también debe configurar un campo de datos del cliente correspondiente en la variable `/destination` configuración de extremo, para que aparezcan las distintas opciones a los usuarios en la interfaz de usuario. Consulte [esta configuración](#file-configuration-templating-pebble) por ejemplo, donde los usuarios pueden seleccionar entre diferentes valores para las opciones de formato de archivo.</li></ul> | - | - | - |
| `compression.value` | Opcional | Códec de compresión que se utilizará al guardar datos en un archivo. Valores compatibles: `none`, `bzip2`, `gzip`, `lz4`, y `snappy`. | `none` | - | - |
| `fileType.value` | Opcional | Especifica el formato del archivo de salida. Valores compatibles: `csv`, `parquet`, y `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece un solo carácter utilizado para aplicar secuencias de escape a valores entre comillas en los que el separador puede formar parte del valor. | `null` | - | - |
| `csvOptions.quoteAll.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si todos los valores deben ir siempre entre comillas. El valor predeterminado es aplicar secuencias de escape únicamente a los valores que contienen un carácter de comillas. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece un separador para cada campo y valor. Este separador puede tener uno o más caracteres. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece un solo carácter utilizado para las comillas de escape dentro de un valor ya citado. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si los valores que contienen comillas siempre deben incluirse entre comillas. El valor predeterminado es omitir todos los valores que contengan un carácter de comillas. | `true` | - | - |
| `csvOptions.header.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se deben escribir los nombres de las columnas como primera línea en el archivo exportado. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se deben recortar los espacios en blanco iniciales de los valores. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se deben recortar los espacios en blanco finales de los valores. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la representación de cadena de un valor nulo. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica el formato de fecha. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la cadena que indica un formato de marca de tiempo. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece un solo carácter utilizado para omitir el escape del carácter de comillas. | `\` cuando los caracteres de escape y comillas son diferentes. `\0` cuando el carácter de escape y comillas son iguales. | - | - |
| `csvOptions.emptyValue.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la representación de cadena de un valor vacío. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}