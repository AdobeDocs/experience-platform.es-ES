---
description: Configurar las opciones de formato de archivo para destinos basados en archivos
title: Aprenda a utilizar Destination SDK para configurar las opciones de formato de archivo para los destinos basados en archivos.
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 1%

---

# Configurar las opciones de formato de archivo para destinos basados en archivos

## Información general {#overview}

El Destination SDK le permite ajustar de forma extensiva las opciones de formato y compresión de los archivos exportados, para que coincidan con los requisitos descendentes de su ubicación de almacenamiento.

En esta página se describe cómo utilizar Destination SDK para configurar las opciones de formato de archivo para los destinos basados en archivos.

## Requisitos previos {#prerequisites}

Antes de avanzar a los pasos descritos a continuación, lea la [introducción al Destination SDK](../../getting-started.md) para obtener información sobre la obtención de las credenciales de autenticación de Adobe I/O necesarias y otros requisitos previos para trabajar con las API de Destination SDK.

Adobe también recomienda leer y familiarizarse con la siguiente documentación antes de continuar:

* Todas las opciones de formato de archivo disponibles se documentan por completo en la variable [configuración de formato de archivo](../../server-and-file-configuration.md#file-configuration) para obtener más información.
* Complete los pasos para [configurar un destino basado en archivos](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) usando Destination SDK.

## Creación de una configuración de servidor y archivo {#create-server-file-configuration}

Comience por usar la variable `/destination-server` para determinar qué opciones de configuración de formato de archivo desea configurar para los archivos exportados.

A continuación se muestra un ejemplo de la configuración de un servidor de destino para un [!DNL Amazon S3] destino, con varias opciones de formato de archivo seleccionadas.

>[!TIP]
>
>Como recordatorio, todas las opciones de formato de archivo disponibles se documentan en la [configuración de formato de archivo](../../server-and-file-configuration.md#file-configuration) para obtener más información.

**Formato de API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
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
}
}'
```

## Añadir las opciones de formato de archivo a la configuración de destino {#create-destination-configuration}

>[!TIP]
>
>**Verificación de la interfaz de usuario del Experience Platform**. Al configurar las opciones de formato de archivo con las configuraciones que se muestran en las secciones siguientes, debe comprobar en la interfaz de usuario del Experience Platform cómo se representan estas opciones.

Después de agregar las opciones de formato de archivo deseadas al servidor de destino y a la configuración de formato de archivo del paso anterior, ahora puede usar la variable `/destinations` Punto final de API para agregar los campos deseados como campos de datos del cliente a la configuración de destino.

>[!IMPORTANT]
>
>Este paso es opcional y solo determina cuál de las opciones de formato de archivo debe mostrarse a los usuarios en la interfaz de usuario del Experience Platform. Si no configura las opciones de formato de archivo como campos de datos del cliente, las exportaciones de archivos continuarán con los valores predeterminados configurados en la variable [configuración de servidor y archivo](#create-server-file-configuration).

En este paso, puede agrupar las opciones mostradas en el orden que desee y crear agrupaciones personalizadas, campos desplegables y agrupaciones condicionales basadas en los tipos de archivo seleccionados. Todos estos ajustes se muestran en la grabación y en las secciones siguientes.

![La grabación de pantalla muestra varias opciones de formato de archivo para archivos por lotes.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-options.gif)

### Ordenar las opciones de formato de archivo {#ordering}

El orden en que se agregan las opciones de formato de archivo como campos de datos de cliente en la configuración de destino se refleja en la interfaz de usuario. Por ejemplo, la configuración siguiente se refleja en consecuencia en la interfaz de usuario, con las opciones que se muestran en el orden **[!UICONTROL Delimitador]**, **[!UICONTROL Carácter de comillas]**, **[!UICONTROL Carácter de escape]**, **[!UICONTROL Valor vacío]**, **[!UICONTROL Valor nulo]**.

![Imagen que muestra el orden de las opciones de formato de archivo en la interfaz de usuario del Experience Platform.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### Agrupar las opciones de formato de archivo {#grouping}

Puede agrupar varias opciones de formato de archivo en una sección. Al configurar la conexión con el destino en la interfaz de usuario, el usuario puede ver y beneficiarse de una agrupación visual de campos similares.

Para ello, utilice `"type": "object"` para crear el grupo y recopilar las opciones de formato de archivo deseadas en un `properties` , como se muestra en el ejemplo siguiente, donde la agrupación **[!UICONTROL Opciones de CSV]** está resaltado.

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },

[...]
```

![Imagen que muestra la agrupación de opciones de CSV en la interfaz de usuario.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-grouping.png)

### Creación de selectores desplegables para las opciones de formato de archivo {#dropdown-selectors}

En los casos en los que desee permitir que los usuarios seleccionen entre varias opciones, por ejemplo, qué carácter debe utilizarse para delimitar los campos de los archivos CSV, puede agregar campos desplegables a la interfaz de usuario.

Para ello, utilice el `namedEnum` como se muestra a continuación y configure un `default` para las opciones que el usuario puede seleccionar.

```json
{
   "name": "delimiter",
   "type": "string",
   "title": "Delimiter",
   "description": "Select your Delimiter",
   "namedEnum": [
   {
      "name": "Comma (,)",
      "value": ","
   },
   {
      "name": "Tab (\\t)",
      "value": "\t"
   }
   ],
   "default": ","
},
```

![La grabación de pantalla muestra un ejemplo de selectores desplegables creados con la configuración que se muestra arriba.](/help/destinations/destination-sdk/assets/guides/batch/dropdown-options-file-formatting.gif)

### Crear opciones de formato de archivo condicional {#conditional-options}

Puede crear opciones de formato de archivo condicionales, que se muestran en el flujo de trabajo de activación solo cuando el usuario selecciona un determinado tipo de archivo para la exportación. Por ejemplo, la configuración siguiente crea una agrupación condicional para las opciones de archivo CSV. Las opciones del archivo CSV solo se muestran cuando el usuario selecciona el CSV como tipo de archivo deseado para la exportación.

Para definir un campo como condicional, utilice la variable `conditional` como se muestra a continuación:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

En un contexto más amplio, puede ver la variable `conditional` campo que se utiliza en la configuración de destino a continuación, junto con la variable `fileType` y `csvOptions` objeto en el que está definido.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

A continuación, puede ver la pantalla de IU resultante, según la configuración anterior. Cuando el usuario selecciona el CSV de tipo de archivo, en la interfaz de usuario se muestran opciones adicionales de formato de archivo que hacen referencia al tipo de archivo CSV.

![La grabación de pantalla muestra la opción de formato de archivo condicional para archivos CSV.](/help/destinations/destination-sdk/assets/guides/batch/conditional-file-formatting.gif)

### Solicitud de API completa que incluye todas las opciones que se muestran arriba

La siguiente solicitud de API combina en una configuración todas las opciones descritas en las secciones anteriores.

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
  "name": "My S3 Destination",
  "description": "Test destination",
  "releaseNotes": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
  },
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
    "defaultStartTime": "00:00",
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
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
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

Una respuesta correcta devuelve la configuración de destino, incluido el identificador único (`instanceId`) de la configuración.

## Limitaciones conocidas {#known-limitations}

Una cierta combinación de opciones de formato de archivo puede dar lugar a resultados de exportación de archivos no deseados.
Adobe recomienda no seleccionar la siguiente combinación de opciones de CSV:

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Para ejemplificar la limitación, considere la exportación de un archivo con los valores siguientes:

| firstname | lastname | country | estado |
|---------|----------|---------|--------|
| Michael | Rose | EE. UU. | NY |
| James | Smith |  | null |

{style=&quot;table-layout:auto&quot;}

Esto resultaría en un resultado como se muestra a continuación. Observe que el valor nulo de la tabla se exporta incorrectamente como una comilla con escape.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora sabe cómo configurar las opciones de formato de archivo personalizadas para los archivos exportados mediante el uso de Destination SDK. A continuación, su equipo puede usar la variable [flujo de trabajo de activación para destinos basados en archivos](../../../ui/activate-batch-profile-destinations.md) para exportar datos al destino.
