---
description: Aprenda a configurar las opciones de formato de archivo para los destinos basados en archivos creados con Adobe Experience Platform Destination SDK, a través del punto final `/destination-servers`.
title: Configuración de formato de archivo
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# Configuración de formato de archivo

Destination SDK admite un conjunto flexible de funciones que puede configurar según sus necesidades de integración. Entre estas características está la compatibilidad con [!DNL CSV] formato de archivo.

Al crear destinos basados en archivos mediante Destination SDK, puede definir el formato que deben tener los archivos CSV exportados. Puede personalizar muchas opciones de formato, como por ejemplo:

* Si el archivo CSV debe incluir un encabezado;
* Qué carácter utilizar para citar valores;
* ¿Qué valores vacíos deberían aparecer?

Según la configuración de destino, los usuarios verán ciertas opciones en la interfaz de usuario al conectarse a un destino basado en archivos. Puede ver el aspecto de estas opciones en la [opciones de formato de archivo para destinos basados en archivos](../../../ui/batch-destinations-file-formatting-options.md) documentación.


Los ajustes de formato de archivo forman parte de la configuración del servidor de destino para destinos basados en archivos.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar las opciones de formato de archivo a través del `/authoring/destination-servers` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Actualizar la configuración del servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página describe todas las opciones de formato de archivo compatibles con las exportadas `CSV` archivos.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | No |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

Puede modificar varias propiedades de los archivos exportados para que coincidan con los requisitos del sistema de recepción de archivos de destino, a fin de leer e interpretar de forma óptima los archivos recibidos del Experience Platform.

>[!NOTE]
>
>Las opciones de CSV solo se admiten al exportar archivos CSV. La variable `fileConfigurations` no es obligatoria al configurar un nuevo servidor de destino. Si no transmite ningún valor en la llamada de API para las opciones de CSV, los predeterminados de la función [tabla de referencia más abajo](#file-formatting-reference-and-example) se utilizará.


## Opciones CSV en las que los usuarios no pueden seleccionar opciones de configuración {#file-configuration-templating-none}

En el ejemplo de configuración siguiente, todas las opciones de CSV están predefinidas. La configuración de exportación definida en cada uno de los `csvOptions` Los parámetros son finales y los usuarios no pueden modificarlos.

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

## Opciones CSV en las que los usuarios pueden seleccionar opciones de configuración {#file-configuration-templating-pebble}

En el ejemplo de configuración siguiente, ninguna de las opciones de CSV está predefinida. La variable `value` en cada una de las `csvOptions` se configura en un campo de datos de cliente correspondiente mediante la variable `/destinations` extremo (por ejemplo [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) para el `quote` formato de archivo ) y los usuarios pueden utilizar la interfaz de usuario del Experience Platform para seleccionar entre las distintas opciones que configure en el campo de datos del cliente correspondiente. Puede ver el aspecto de estas opciones en la [opciones de formato de archivo para destinos basados en archivos](../../../ui/batch-destinations-file-formatting-options.md) documentación.

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

## Referencia completa y ejemplos de opciones de formato de archivo compatibles {#file-formatting-reference-and-example}

>[!TIP]
>
>Las opciones de formato de archivo CSV que se describen a continuación también se documentan en la sección [Guía de Apache Spark para archivos CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Las descripciones utilizadas a continuación se toman de la guía Apache Spark.

A continuación se muestra una referencia completa de todas las opciones de formato de archivo disponibles en Destination SDK, junto con ejemplos de salida para cada opción.

| Campo | Obligatorio/Opcional | Descripción | Valor predeterminado | Ejemplo de salida 1 | Ejemplo de salida 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Requerido | Para cada opción de formato de archivo que configure, debe agregar el parámetro `templatingStrategy`, que puede tener dos valores: <br><ul><li>`NONE`: utilice este valor si no planea permitir que los usuarios seleccionen entre diferentes valores para una configuración. Consulte [esta configuración](#file-configuration-templating-none) por ejemplo, donde las opciones de formato de archivo son fijas.</li><li>`PEBBLE_V1`: utilice este valor si desea permitir que los usuarios seleccionen entre diferentes valores para una configuración. En este caso, también debe configurar un campo de datos de cliente correspondiente en la variable `/destination` configuración del extremo, para que aparezcan las distintas opciones para los usuarios en la interfaz de usuario. Consulte [esta configuración](#file-configuration-templating-pebble) para un ejemplo en el que los usuarios pueden seleccionar entre diferentes valores para las opciones de formato de archivo.</li></ul> | - | - | - |
| `compression.value` | Opcional | Códec de compresión que se utilizará al guardar datos en un archivo. Valores compatibles: `none`, `bzip2`, `gzip`, `lz4`y `snappy`. | `none` | - | - |
| `fileType.value` | Opcional | Especifica el formato del archivo de salida. Valores compatibles: `csv`, `parquet`y `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utiliza para escapar los valores entre comillas, donde el separador puede formar parte del valor. | `null` | - | - |
| `csvOptions.quoteAll.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si todos los valores deben estar siempre entre comillas. De forma predeterminada, solo se escapan los valores que contienen un carácter de comillas. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un separador para cada campo y valor. Este separador puede ser uno o más caracteres. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utiliza para las comillas de escape dentro de un valor ya entrecomillado. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si los valores que contienen comillas siempre se deben incluir entre comillas. El valor predeterminado es omitir todos los valores que contengan un carácter de comillas. | `true` | - | - |
| `csvOptions.header.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se deben escribir los nombres de las columnas como primera línea en el archivo exportado. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se recortan los espacios en blanco iniciales de los valores. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica si se recortarán los espacios en blanco al final de los valores. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la representación de cadena de un valor nulo. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Indica el formato de fecha. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Establece la cadena que indica un formato de marca de tiempo. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define un carácter único que se utilizará para escapar el escape del carácter de comillas. | `\` cuando los caracteres escape y comillas son diferentes. `\0` cuando el carácter escape y comillas son iguales. | - | - |
| `csvOptions.emptyValue.value` | Opcional | *Solo para`"fileType.value": "csv"`*. Define la representación de cadena de un valor vacío. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor cómo funciona el formato de archivo en la configuración del servidor de destino y cómo puede configurarlo.

Para obtener más información sobre los otros componentes del servidor de destino, consulte los siguientes artículos:

* [Especificaciones del servidor para los destinos creados con el Destination SDK](server-specs.md)
* [Plantillas de especificaciones](templating-specs.md)
* [Formato del mensaje](message-format.md)