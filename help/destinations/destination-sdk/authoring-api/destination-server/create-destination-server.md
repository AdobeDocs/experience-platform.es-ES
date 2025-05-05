---
description: Esta página ejemplifica la llamada de API utilizada para crear un servidor de destino a través de Adobe Experience Platform Destination SDK.
title: Crear una configuración de servidor de destino
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 5%

---

# Crear una configuración de servidor de destino

La creación de un servidor de destino es el primer paso para crear su propio destino con Destination SDK. El servidor de destino incluye opciones de configuración para las especificaciones [server](../../functionality/destination-server/server-specs.md) y [templating](../../functionality/destination-server/templating-specs.md), el [formato de mensaje](../../functionality/destination-server/message-format.md) y las opciones de [formato de archivo](../../functionality/destination-server/file-formatting.md) (para destinos basados en archivos).

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para crear su propio servidor de destino mediante el extremo de API `/authoring/destination-servers`.

Para obtener una descripción detallada de las capacidades que puede configurar a través de este extremo, lea los siguientes artículos:

* [Especificaciones del servidor para destinos creados con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Plantillas de especificaciones para destinos creados con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del mensaje](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuración de formato de archivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1&rbrace;.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API del servidor de destino {#get-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Crear una configuración de servidor de destino {#create}

Puede crear una nueva configuración del servidor de destino realizando una solicitud `POST` al extremo `/authoring/destination-servers`.

>[!TIP]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato de API**

```http
POST /authoring/destination-servers
```

Según el tipo de destino que cree, debe configurar un tipo ligeramente diferente de servidor de destino.

### Crear servidores de destino de esquema estático {#static-destination-servers}

Vea en las pestañas siguientes ejemplos de servidores de destino para destinos que utilizan [esquemas estáticos](../../functionality/destination-configuration/schema-configuration.md#attributes-schema).

Las siguientes cargas útiles de ejemplo incluyen todos los parámetros admitidos por cada tipo de servidor de destino. No es necesario incluir todos los parámetros en la solicitud. La carga útil se puede personalizar según sus necesidades.

Seleccione cada pestaña a continuación para ver las solicitudes de API correspondientes.

>[!BEGINTABS]

>[!TAB Tiempo real (streaming)]

**Crear un servidor de destino en tiempo real (streaming)**

Debe crear un servidor de destino en tiempo real (flujo) similar al que se muestra a continuación cuando configura una integración basada en API en tiempo real (flujo).

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `name` | Cadena | *Requerido.* representa un nombre descriptivo de su servidor, visible solamente para Adobe. Este nombre no es visible para socios o clientes. Ejemplo `Moviestar destination server`. |
| `destinationServerType` | Cadena | *Requerido.* se estableció en `URL_BASED` para destinos de tiempo real (streaming). |
| `urlBasedDestination.url.templatingStrategy` | Cadena | *Requerido.* <ul><li>Use `PEBBLE_V1` si Adobe necesita transformar la dirección URL en el campo `value` que aparece a continuación. Utilice esta opción si tiene un extremo como `https://api.moviestar.com/data/{{customerData.region}}/items`, donde la parte `region` puede diferir entre los clientes. En este caso, también debe configurar `region` como [campo de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) en la [configuración de destino]&#x200B;(../destination-configuration/create-destination-configuration.md. </li><li> Use `NONE` si no se necesita ninguna transformación en el lado de Adobe, por ejemplo, si tiene un extremo como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Cadena | *Requerido.* Rellene la dirección del extremo de API al que Experience Platform debe conectarse. |
| `httpTemplate.httpMethod` | Cadena | *Requerido.* El método que Adobe usará en las llamadas a su servidor. Las opciones son `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Cadena | *Requerido.* Esta cadena es la versión con caracteres de escape que transforma los datos de los clientes de Experience Platform al formato que espera el servicio. <br> <ul><li> Para obtener información sobre cómo escribir la plantilla, lea la sección [Uso de la plantilla](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obtener más información sobre el escape de caracteres, consulte el [estándar RFC JSON, sección siete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para ver un ejemplo de transformación simple, consulte la transformación [Atributos de perfil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Cadena | *Requerido.* El tipo de contenido que acepta su servidor. Este valor es probablemente `application/json`. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!TAB Amazon S3]

**Crear un servidor de destino Amazon S3**

Debe crear un servidor de destino [!DNL Amazon S3] similar al que se muestra a continuación al configurar un destino [!DNL Amazon S3] basado en archivos.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Amazon S3], establezca esto en `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Cadena | Nombre del contenedor [!DNL Amazon S3] que utilizará este destino. |
| `fileBasedS3Destination.path.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | N/A | Consulte [configuración de formato de archivo](../../functionality/destination-server/file-formatting.md) para obtener información detallada sobre cómo establecer esta configuración. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!TAB SFTP]

**Crear un servidor de destino [!DNL SFTP]**

Debe crear un servidor de destino [!DNL SFTP] similar al que se muestra a continuación al configurar un destino [!DNL SFTP] basado en archivos.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
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
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL SFTP] destinos, establezca esto en `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | Cadena | El directorio raíz del almacenamiento de destino. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | Cadena | El nombre de host del almacenamiento de destino. |
| `port` | Entero | El puerto del servidor de archivos SFTP. |
| `encryptionMode` | Cadena | Indica si se debe utilizar el cifrado de archivos. Valores compatibles: <ul><li>PGP</li><li>Ninguna</li></ul> |
| `fileConfigurations` | N/A | Consulte [configuración de formato de archivo](../../functionality/destination-server/file-formatting.md) para obtener información detallada sobre cómo establecer esta configuración. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!TAB Almacenamiento de Azure Data Lake]

**Crear un servidor de destino [!DNL Azure Data Lake Storage]**

Debe crear un servidor de destino [!DNL Azure Data Lake Storage] similar al que se muestra a continuación al configurar un destino [!DNL Azure Data Lake Storage] basado en archivos.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, establezca esto en `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | N/A | Consulte [configuración de formato de archivo](../../functionality/destination-server/file-formatting.md) para obtener información detallada sobre cómo establecer esta configuración. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!TAB Almacenamiento de blob de Azure]

**Crear un servidor de destino [!DNL Azure Blob Storage]**

Debe crear un servidor de destino [!DNL Azure Blob Storage] similar al que se muestra a continuación al configurar un destino [!DNL Azure Blob Storage] basado en archivos.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Blob Storage] destinos, establezca esto en `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Cadena | Nombre del contenedor [!DNL Azure Blob Storage] que utilizará este destino. |
| `fileConfigurations` | N/A | Consulte [configuración de formato de archivo](../../functionality/destination-server/file-formatting.md) para obtener información detallada sobre cómo establecer esta configuración. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!TAB Zona de aterrizaje de datos (DLZ)]

**Crear un servidor de destino [!DNL Data Landing Zone (DLZ)]**

Debe crear un servidor de destino [!DNL Data Landing Zone (DLZ)] similar al que se muestra a continuación al configurar un destino [!DNL Data Landing Zone (DLZ)] basado en archivos.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Data Landing Zone] destinos, establezca esto en `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | N/A | Consulte [configuración de formato de archivo](../../functionality/destination-server/file-formatting.md) para obtener información detallada sobre cómo establecer esta configuración. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!TAB Almacenamiento en la nube de Google]

**Crear un servidor de destino [!DNL Google Cloud Storage]**

Debe crear un servidor de destino [!DNL Google Cloud Storage] similar al que se muestra a continuación al configurar un destino [!DNL Google Cloud Storage] basado en archivos.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Google Cloud Storage] destinos, establezca esto en `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Cadena | Nombre del contenedor [!DNL Google Cloud Storage] que utilizará este destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |
| `fileConfigurations` | N/A | Consulte [configuración de formato de archivo](../../functionality/destination-server/file-formatting.md) para obtener información detallada sobre cómo establecer esta configuración. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!ENDTABS]

### Crear servidores de destino de esquema dinámico {#dynamic-schema-servers}

Los esquemas dinámicos le permiten recuperar dinámicamente los atributos de destino admitidos y generar esquemas basados en su propia API. Debe configurar un servidor de destino para esquemas dinámicos antes de poder configurar el esquema.

Vea en la pestaña siguiente un ejemplo de un servidor de destino para destinos que utilizan [esquemas dinámicos](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

La carga útil de ejemplo siguiente incluye todos los parámetros necesarios para un servidor de esquema dinámico.

>[!BEGINTABS]

>[!TAB Servidor de esquema dinámico]

**Crear un servidor de esquema dinámico**

Debe crear un servidor de esquema dinámico similar al que se muestra a continuación cuando configura un destino que recupera su esquema de perfil desde su propio extremo de API. A diferencia de un esquema estático, un esquema dinámico no utiliza una matriz `profileFields`. En su lugar, los esquemas dinámicos utilizan un servidor de esquema dinámico que se conecta a su propia API desde donde recupera la configuración de esquema.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `name` | Cadena | *Requerido.* representa un nombre descriptivo del servidor de esquema dinámico, visible solamente para Adobe. |
| `destinationServerType` | Cadena | *Requerido.* se estableció en `URL_BASED` para servidores de esquema dinámico. |
| `urlBasedDestination.url.templatingStrategy` | Cadena | *Requerido.* <ul><li>Use `PEBBLE_V1` si Adobe necesita transformar la dirección URL en el campo `value` que aparece a continuación. Utilice esta opción si tiene un extremo como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Use `NONE` si no se necesita ninguna transformación en el lado de Adobe, por ejemplo, si tiene un extremo como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Cadena | *Requerido.* Rellene la dirección del extremo de la API al que Experience Platform debe conectarse y recupere los campos de esquema para rellenar como campos de destino en el paso de asignación del flujo de trabajo de activación. |
| `httpTemplate.httpMethod` | Cadena | *Requerido.* El método que Adobe usará en las llamadas a su servidor. Para servidores de esquema dinámico, use `GET`. |
| `responseFields.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `responseFields.value` | Cadena | *Requerido.* Esta cadena es la plantilla de transformación sin caracteres que transforma la respuesta recibida de la API del socio en el esquema del socio que se mostrará en la interfaz de usuario de Experience Platform. <br> <ul><li> Para obtener información sobre cómo escribir la plantilla, lea la sección [Uso de la plantilla](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obtener más información sobre el escape de caracteres, consulte el [estándar RFC JSON, sección siete](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Para ver un ejemplo de transformación simple, consulte la transformación [Atributos de perfil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++


>[!ENDTABS]


### Crear servidores de destino desplegables dinámicos {#dynamic-dropdown-servers}

Utilice [desplegables dinámicos](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) para recuperar y rellenar dinámicamente campos de datos de clientes desplegables basados en su propia API. Por ejemplo, puede recuperar una lista de cuentas de usuario existentes que desee utilizar para una conexión de destino.

Debe configurar un servidor de destino para los desplegables dinámicos antes de poder configurar el campo de datos de cliente desplegables dinámicos.

Consulte en la pestaña siguiente un ejemplo de un servidor de destino utilizado para recuperar dinámicamente los valores que se mostrarán en un selector desplegable, desde una API.

La carga útil de ejemplo siguiente incluye todos los parámetros necesarios para un servidor de esquema dinámico.

>[!BEGINTABS]

>[!TAB Servidor desplegable dinámico]

**Crear un servidor desplegable dinámico**

Debe crear un servidor desplegable dinámico similar al que se muestra a continuación cuando configura un destino que recupera los valores de un campo de datos de cliente desplegable desde su propio extremo de API.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `name` | Cadena | *Requerido.* representa un nombre descriptivo de su servidor desplegable dinámico, visible solamente para Adobe. |
| `destinationServerType` | Cadena | *Requerido.* se estableció en `URL_BASED` para servidores desplegables dinámicos. |
| `urlBasedDestination.url.templatingStrategy` | Cadena | *Requerido.* <ul><li>Use `PEBBLE_V1` si Adobe necesita transformar la dirección URL en el campo `value` que aparece a continuación. Utilice esta opción si tiene un extremo como: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Use `NONE` si no se necesita ninguna transformación en el lado de Adobe, por ejemplo, si tiene un extremo como: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Cadena | *Requerido.* Rellene la dirección del extremo de API al que Experience Platform debe conectarse y recupere los valores desplegables. |
| `httpTemplate.httpMethod` | Cadena | *Requerido.* El método que Adobe usará en las llamadas a su servidor. Para servidores desplegables dinámicos, use `GET`. |
| `httpTemplate.headers` | Objeto | *Opcional.l* Incluya los encabezados necesarios para conectarse al servidor desplegable dinámico. |
| `responseFields.templatingStrategy` | Cadena | *Requerido.*: use `PEBBLE_V1`. |
| `responseFields.value` | Cadena | *Requerido.* Esta cadena es la plantilla de transformación sin caracteres que transforma la respuesta recibida de su API en los valores que se mostrarán en la interfaz de usuario de Experience Platform. <br> <ul><li> Para obtener información sobre cómo escribir la plantilla, lea la sección [Uso de la plantilla](../../functionality/destination-server/message-format.md#using-templating). </li><li> Para obtener más información sobre el escape de caracteres, consulte el [estándar RFC JSON, sección siete](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración del servidor de destino recién creada.

+++

>[!ENDTABS]

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo crear un nuevo servidor de destino a través del extremo de la API de Destination SDK `/authoring/destination-servers`.

Para obtener más información acerca de lo que puede hacer con este extremo, consulte los siguientes artículos:

* [Recuperar una configuración de servidor de destino](retrieve-destination-server.md)
* [Actualizar la configuración de un servidor de destino](update-destination-server.md)
* [Eliminar una configuración de servidor de destino](delete-destination-server.md)

Para saber dónde encaja este extremo en el proceso de creación de destinos, consulte los siguientes artículos:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
