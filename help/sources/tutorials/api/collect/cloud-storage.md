---
keywords: Experience Platform;inicio;temas populares;datos de almacenamiento en la nube
solution: Experience Platform
title: Crear un flujo de datos para fuentes de almacenamiento en la nube mediante la API de Flow Service
type: Tutorial
description: Este tutorial cubre los pasos para recuperar datos de un almacenamiento en la nube de terceros e incluirlos en Platform mediante conectores de origen y API.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 92f39f970402ab907f711d23a8f5f599668f0fe0
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 2%

---

# Cree un flujo de datos para fuentes de almacenamiento en la nube mediante [!DNL Flow Service] API

Este tutorial explica los pasos para recuperar datos de una fuente de almacenamiento en la nube y llevarlos a Platform mediante [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Para crear un flujo de datos, ya debe tener un ID de conexión base válido con un origen de almacenamiento en la nube. Si no tiene este ID, consulte la [información general de orígenes](../../../home.md#cloud-storage) para obtener una lista de orígenes de almacenamiento en la nube con los que puede crear una conexión base.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Guía para desarrolladores de Schema Registry](../../../../xdm/api/getting-started.md): incluye información importante que necesita conocer para realizar llamadas correctamente a la API de Registro de esquemas. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados necesarios para realizar solicitudes (con especial atención al encabezado Aceptar y sus posibles valores).
- [[!DNL Catalog Service]](../../../../catalog/home.md): el catálogo es el sistema de registro para la ubicación y el linaje de los datos dentro del Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): la API de ingesta por lotes le permite introducir datos en Experience Platform como archivos por lotes.
- [Zonas protegidas](../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../landing/api-guide.md).

## Crear una conexión de origen {#source}

Puede crear una conexión de origen realizando una solicitud de POST a `sourceConnections` punto final de [!DNL Flow Service] API al proporcionar su ID de conexión base, la ruta al archivo de origen que desea introducir y el ID de especificación de conexión correspondiente de su origen.

Al crear una conexión de origen, también debe definir un valor de enumeración para el atributo de formato de datos.

Utilice los siguientes valores de enumeración para orígenes basados en archivos:

| Formato de datos | Valor de enumeración |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todos los orígenes basados en tablas, establezca el valor en `tabular`.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `baseConnectionId` | El ID de conexión base del origen de almacenamiento en la nube. |
| `data.format` | El formato de los datos que desea llevar a Platform. Los valores admitidos son: `delimited`, `JSON`, y `parquet`. |
| `data.properties` | (Opcional) Conjunto de propiedades que se pueden aplicar a los datos al crear una conexión de origen. |
| `data.properties.columnDelimiter` | (Opcional) Un delimitador de columna de un solo carácter que puede especificar al recopilar archivos planos. Cualquier valor de carácter único es un delimitador de columna admisible. Si no se proporciona, escriba una coma (`,`) se usa como valor predeterminado. **Nota**: La `columnDelimiter` La propiedad solo se puede utilizar al ingerir archivos delimitados. |
| `data.properties.encoding` | (Opcional) Una propiedad que define el tipo de codificación que se utilizará al ingerir los datos en Platform. Los tipos de codificación admitidos son: `UTF-8` y `ISO-8859-1`. **Nota**: La `encoding` El parámetro solo está disponible al ingerir archivos CSV delimitados. Se incorporarán otros tipos de archivo con la codificación predeterminada, `UTF-8`. |
| `data.properties.compressionType` | (Opcional) Una propiedad que define el tipo de archivo comprimido para la ingesta. Los tipos de archivo comprimidos admitidos son: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, y `tar`. **Nota**: La `compressionType` La propiedad solo se puede utilizar al ingerir archivos delimitados o JSON. |
| `params.path` | La ruta del archivo de origen al que está accediendo. Este parámetro apunta a un archivo individual o a una carpeta completa.  **Nota**: Puede utilizar un asterisco en lugar del nombre del archivo para especificar la ingesta de una carpeta completa. Por ejemplo: `/acme/summerCampaign/*.csv` ingerirá la totalidad `/acme/summerCampaign/` carpeta. |
| `params.type` | El tipo de archivo del archivo de datos de origen que está ingiriendo. Tipo de uso `file` para introducir un archivo individual y tipo de uso `folder` para introducir una carpeta completa. |
| `connectionSpec.id` | El ID de especificación de conexión asociado con el origen de almacenamiento en la nube específico. Consulte la [apéndice](#appendix) para obtener una lista de los ID de especificación de conexión. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Utilice expresiones regulares para seleccionar un conjunto específico de archivos para la ingesta {#regex}

Puede utilizar expresiones regulares para introducir un conjunto concreto de archivos del origen a Platform al crear una conexión de origen.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

En el ejemplo siguiente, se utiliza una expresión regular en la ruta del archivo para especificar la ingesta de todos los archivos CSV que tienen `premium` en su nombre.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### Configurar una conexión de origen para introducir datos de forma recursiva

Al crear una conexión de origen, puede utilizar el `recursive` para introducir datos de carpetas profundamente anidadas.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

En el ejemplo siguiente, la variable `recursive: true` el parámetro informa [!DNL Flow Service] para leer todas las subcarpetas de forma recursiva durante el proceso de ingesta.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la variable [API de Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](../../../../xdm/api/schemas.md).

## Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), proporcionando el ID del esquema de destinatario dentro de la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial sobre [creación de un conjunto de datos mediante la API](../../../../catalog/api/create-dataset.md).

## Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino donde aterrizan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija asociado al lago de datos. Este ID de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino con el [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```http
POST /targetConnections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `data.schema.id` | El `$id` del esquema XDM de destino. |
| `data.schema.version` | La versión del esquema. Se debe establecer este valor `application/vnd.adobe.xed-full+json;version=1`, que devuelve la última versión secundaria del esquema. |
| `params.dataSetId` | El ID del conjunto de datos de destinatario generado en el paso anterior. **Nota**: Debe proporcionar un ID de conjunto de datos válido al crear una conexión de destino. Si la ID del conjunto de datos no es válida, se producirá un error. |
| `connectionSpec.id` | ID de especificación de conexión utilizado para conectarse al lago de datos. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único ( ) de la nueva conexión de destino`id`). Este ID es necesario en pasos posteriores.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino.

Para crear un conjunto de asignaciones, realice una solicitud de POST al `mappingSets` punto final del [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) al proporcionar el esquema XDM de destino `$id` y los detalles de los conjuntos de asignaciones que desee crear.

>[!TIP]
>
>Puede asignar tipos de datos complejos, como matrices en archivos JSON, mediante un conector de origen de almacenamiento en la nube.

**Formato de API**

```http
POST /conversion/mappingSets
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `xdmSchema` | ID del esquema XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de fuentes y llevarlos a Platform. Para crear un flujo de datos, primero debe obtener las especificaciones del flujo de datos responsables de recopilar datos de almacenamiento en la nube.

**Formato de API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>La carga útil de respuesta JSON a continuación está oculta para la brevedad. Seleccione &quot;carga útil&quot; para ver la carga útil de respuesta.

+++ Ver carga útil

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos responsable de traer datos de su origen a Platform. La respuesta incluye la especificación de flujo única `id` necesario para crear un nuevo flujo de datos.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
  "permissionsInfo": {
    "view": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "optionSpec": {
    "name": "OptionSpec",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "errorDiagnosticsEnabled": {
          "title": "Error diagnostics.",
          "description": "Flag to enable detailed and sample error diagnostics summary.",
          "type": "boolean",
          "default": false
        },
        "partialIngestionPercent": {
          "title": "Partial ingestion threshold.",
          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
          "type": "number",
          "exclusiveMinimum": 0
        }
      }
    }
  },
  "scheduleSpec": {
    "name": "PeriodicSchedule",
    "type": "Periodic",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "startTime": {
          "description": "epoch time",
          "type": "integer"
        },
        "frequency": {
          "type": "string",
          "enum": [
            "once",
            "minute",
            "hour",
            "day",
            "week"
          ]
        },
        "interval": {
          "type": "integer"
        },
        "backfill": {
          "type": "boolean",
          "default": true
        }
      },
      "required": [
        "startTime",
        "frequency"
      ],
      "if": {
        "properties": {
          "frequency": {
            "const": "once"
          }
        }
      },
      "then": {
        "allOf": [
          {
            "not": {
              "required": [
                "interval"
              ]
            }
          },
          {
            "not": {
              "required": [
                "backfill"
              ]
            }
          }
        ]
      },
      "else": {
        "required": [
          "interval"
        ],
        "if": {
          "properties": {
            "frequency": {
              "const": "minute"
            }
          }
        },
        "then": {
          "properties": {
            "interval": {
              "minimum": 15
            }
          }
        },
        "else": {
          "properties": {
            "interval": {
              "minimum": 1
            }
          }
        }
      }
    }
  },
  "transformationSpec": [
    {
      "name": "Mapping",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for different mapping from source to target",
        "properties": {
          "mappingId": {
            "type": "string"
          },
          "mappingVersion": {
            "type": "string"
          }
        }
      }
    }
  ],
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## Cree un flujo de datos

El último paso para recopilar datos de almacenamiento en la nube es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

- [ID de conexión de origen](#source)
- [ID de conexión de destino](#target)
- [ID de asignación](#mapping)
- [ID de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

>[!NOTE]
>
>Para la ingesta por lotes, cada flujo de datos posterior selecciona los archivos que se van a ingerir desde el origen en función de su **última modificación** marca de tiempo. Esto significa que los flujos de datos por lotes seleccionan archivos del origen que son nuevos o que se han modificado desde la última ejecución del flujo de datos.

Para programar una ingesta, primero debe establecer el valor de la hora de inicio en un tiempo récord en segundos. A continuación, debe establecer el valor de frecuencia en una de las cinco opciones: `once`, `minute`, `hour`, `day`, o `week`. El valor de intervalo designa el periodo entre dos ingestas consecutivas y la creación de una ingesta única no requiere que se establezca un intervalo. Para todas las demás frecuencias, el valor del intervalo debe establecerse en igual o mayor que `15`.

>[!IMPORTANT]
>
>Se recomienda programar el flujo de datos para una ingesta única al utilizar [Conector de FTP](../../../connectors/cloud-storage/ftp.md).

**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | El [ID de especificación de flujo](#specs) recuperado en el paso anterior. |
| `sourceConnectionIds` | El [ID de conexión de origen](#source) recuperado en un paso anterior. |
| `targetConnectionIds` | El [ID de conexión de destino](#target-connection) recuperado en un paso anterior. |
| `transformations.params.mappingId` | El [ID de asignación](#mapping) recuperado en un paso anterior. |
| `scheduleParams.startTime` | Hora de inicio del flujo de datos en tiempo epoch. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day`, o `week`. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. El intervalo no es obligatorio cuando la frecuencia está establecida como `once` y debe ser mayor o igual que `15` para otros valores de frecuencia. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para obtener más información sobre cómo monitorizar flujos de datos, consulte el tutorial sobre [monitorización de flujos de datos en la API](../monitor.md)

## Pasos siguientes

Al seguir este tutorial, ha creado un conector de origen para recopilar datos del almacenamiento en la nube de forma programada. Ahora, los servicios de Platform posteriores pueden utilizar los datos entrantes, como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Resumen del perfil del cliente en tiempo real](../../../../profile/home.md)
- [Resumen de Data Science Workspace](../../../../data-science-workspace/home.md)

## Apéndice {#appendix}

En la siguiente sección se enumeran los diferentes conectores de origen de almacenamiento en la nube y sus especificaciones de conexiones.

### Especificación de conexión

| Nombre del conector | Especificación de conexión |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Event Hubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
