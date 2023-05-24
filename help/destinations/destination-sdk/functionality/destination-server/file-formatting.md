---
description: Obtenga información sobre cómo configurar las opciones de formato de archivo para destinos basados en archivos creados con Adobe Experience Platform Destination SDK a través del punto de conexión /destination-servers.
title: Configuración de formato de archivo
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# Configuración de formato de archivo

Destination SDK admite un conjunto flexible de funciones que puede configurar según sus necesidades de integración. Entre estas características se encuentra la compatibilidad con [!DNL CSV] formato de archivo.

Al crear destinos basados en archivos mediante Destination SDK, puede definir el formato de los archivos CSV exportados. Puede personalizar muchas opciones de formato, como, entre otras:

* Si el archivo CSV debe incluir un encabezado;
* Qué carácter utilizar para citar valores;
* Aspecto que deben tener los valores vacíos.

Según la configuración de destino, los usuarios verán ciertas opciones en la interfaz de usuario al conectarse a un destino basado en archivos. Puede ver el aspecto de estas opciones en la sección [opciones de formato de archivo para destinos basados en archivos](../../../ui/batch-destinations-file-formatting-options.md) documentación.


La configuración de formato de archivo forma parte de la configuración del servidor de destino para destinos basados en archivos.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar las opciones de formato de archivo mediante la variable `/authoring/destination-servers` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Actualizar la configuración de un servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página describe todos los ajustes de formato de archivo admitidos para los archivos exportados `CSV` archivos.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | No |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

Puede modificar varias propiedades de los archivos exportados para que coincidan con los requisitos del sistema de recepción de archivos del destino, de modo que se lean e interpreten de forma óptima los archivos recibidos del Experience Platform.

>[!NOTE]
>
>Las opciones CSV solo se admiten al exportar archivos CSV. El `fileConfigurations` no es obligatoria al configurar un nuevo servidor de destino. Si no pasa ningún valor en la llamada de API para las opciones de CSV, los predeterminados de la [tabla de referencia más abajo](#file-formatting-reference-and-example) se utilizará.


## Opciones de CSV donde los usuarios no pueden seleccionar opciones de configuración {#file-configuration-templating-none}

En el siguiente ejemplo de configuración, todas las opciones de CSV están predefinidas. La configuración de exportación definida en cada una de las `csvOptions` los parámetros son finales y los usuarios no pueden modificarlos.

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

## Opciones de CSV donde los usuarios pueden seleccionar opciones de configuración {#file-configuration-templating-pebble}

En el ejemplo de configuración que se muestra a continuación, ninguna de las opciones de CSV está predefinida. El `value` en cada una de las `csvOptions` parámetros se configura en un campo de datos del cliente correspondiente a través de la variable `/destinations` punto final (por ejemplo, [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) para el `quote` opciones de formato de archivo ) y los usuarios pueden utilizar la interfaz de usuario de Experience Platform para seleccionar entre las distintas opciones que configure en el campo correspondiente datos de cliente. Puede ver el aspecto de estas opciones en la sección [opciones de formato de archivo para destinos basados en archivos](../../../ui/batch-destinations-file-formatting-options.md) documentación.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      }
   }
}
```

## Referencia completa y ejemplos de las opciones de formato de archivo compatibles {#file-formatting-reference-and-example}

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
| `csvOptions.escape.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utiliza para las comillas de escape dentro de un valor ya entrecomillado. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
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

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo funciona el formato de archivos en una configuración de servidor de destino y cómo puede configurarlo.

Para obtener más información acerca de los demás componentes del servidor de destino, consulte los siguientes artículos:

* [Especificaciones del servidor para destinos creados con Destination SDK](server-specs.md)
* [Especificaciones de plantilla](templating-specs.md)
* [Formato del mensaje](message-format.md)