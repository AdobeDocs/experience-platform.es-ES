---
keywords: Experience Platform;inicio;temas populares;crm;CRM
solution: Experience Platform
title: Creación de un flujo de datos para fuentes CRM mediante la API del servicio de flujo
type: Tutorial
description: Este tutorial cubre los pasos para recuperar datos de un sistema CRM de terceros e incluirlos en Experience Platform mediante conectores de origen y API.
exl-id: b07dd640-bce6-4699-9d2b-b7096746934a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 3%

---

# Crear un flujo de datos para orígenes CRM mediante la API [!DNL Flow Service]

Este tutorial trata los pasos para recuperar datos de un origen CRM y llevarlos a Experience Platform mediante [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>* Para crear un flujo de datos, ya debe tener un ID de conexión base válido con un origen CRM. Si no tiene este identificador, consulte la [descripción general de orígenes](../../../home.md#customer-relationship-management) para obtener una lista de orígenes de CRM con los que puede crear una conexión base.
>* Para que Experience Platform pueda introducir datos, las zonas horarias de todos los orígenes de lotes basados en tablas deben configurarse en UTC.

## Introducción

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): el marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Guía para desarrolladores de Schema Registry](../../../../xdm/api/getting-started.md): Incluye información importante que necesita conocer para realizar correctamente llamadas a la API de Schema Registry. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados necesarios para realizar solicitudes (con especial atención al encabezado Aceptar y sus posibles valores).
* [[!DNL Catalog Service]](../../../../catalog/home.md): el catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): la API de ingesta por lotes le permite ingerir datos en Experience Platform como archivos por lotes.
* [Zonas protegidas](../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../landing/api-guide.md).

## Crear una conexión de origen {#source}

Puede crear una conexión de origen realizando una petición POST a la API [!DNL Flow Service]. Una conexión de origen consta de un identificador de conexión, una ruta de acceso al archivo de datos de origen y un identificador de especificación de conexión.

Para crear una conexión de origen, también debe definir un valor de enumeración para el atributo de formato de datos.

Utilice los siguientes valores de enumeración para los conectores basados en archivos:

| Formato de datos | Valor de enumeración |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todos los conectores basados en tablas, establezca el valor en `tabular`.

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
        "name": "Salesforce source connection",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "description": "Salesforce source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "tableName": "Accounts",
            "columns": [
                {
                    "name": "first_name",
                    "type": "string",
                    "xdm": {
                        "type": "String"
                    }
                },
                {
                    "name": "last_name",
                    "type": "string",
                    "xdm": {
                        "type": "String"
                    }
                },
                {
                    "name": "email",
                    "type": "string",
                    "xdm": {
                        "type": "String"
                    }
                }
            ]
        },
        "connectionSpec": {
            "id": "ccfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `baseConnectionId` | El ID de conexión único del sistema CRM de terceros al que está accediendo. |
| `params.path` | Ruta del archivo de origen. |
| `connectionSpec.id` | El ID de especificación de conexión asociado con el sistema CRM de terceros específico. Consulte el [apéndice](#appendix) para obtener una lista de los ID de especificación de conexión. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "9a603322-19d2-4de9-89c6-c98bd54eb184"
    "etag": "\"4a00038b-0000-0200-0000-5ebc47fd0000\""
}
```

## Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Experience Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Experience Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una petición POST a la [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](../../../../xdm/api/schemas.md).

## Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una petición POST en la [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), que proporcione el ID del esquema de destino en la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](../../../../catalog/api/create-dataset.md).

## Creación de una conexión de destino

Una conexión de destino representa la conexión con el destino donde aterrizan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija asociado al lago de datos. Este id. de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con la API [!DNL Flow Service], puede crear una conexión de destino especificando estos identificadores junto con el conjunto de datos que contendrá los datos de origen entrantes.

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
        "name": "Salesforce target connection",
        "description": "Salesforce target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5c8c3c555033b814b69f947f"
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
| `data.schema.version` | La versión del esquema. Este valor debe establecerse `application/vnd.adobe.xed-full+json;version=1`, que devuelve la última versión secundaria del esquema. |
| `params.dataSetId` | El ID del conjunto de datos de destinatario generado en el paso anterior. **Nota**: debe proporcionar un identificador de conjunto de datos válido al crear una conexión de destino. Si la ID del conjunto de datos no es válida, se producirá un error. |
| `connectionSpec.id` | ID de especificación de conexión utilizado para conectarse al lago de datos. Este identificador es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

```json
{
    "id": "4ee890c7-519c-4291-bd20-d64186b62da8",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino.

Para crear un conjunto de asignaciones, realice una petición POST al extremo `mappingSets` de la [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/) y proporcione el esquema XDM de destino `$id` y los detalles de los conjuntos de asignaciones que desee crear.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "first_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "last_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
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
    "id": "500a9b747fcf4908a21917d49bd61780",
    "version": 0,
    "createdDate": 1591043336298,
    "modifiedDate": 1591043336298,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de fuentes y llevarlos a Experience Platform. Para crear un flujo de datos, primero debe obtener las especificaciones del flujo de datos responsables de recopilar datos CRM.

**Formato de API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos responsable de importar datos de su origen a Experience Platform. La respuesta incluye la especificación de flujo única `id` necesaria para crear un nuevo flujo de datos.

>[!NOTE]
>
>La carga útil de respuesta JSON a continuación está oculta para la brevedad. Seleccione &quot;carga útil&quot; para ver la carga útil de respuesta.

+++ Ver carga útil

```json
{
  "id": "14518937-270c-4525-bdec-c2ba7cce3860",
  "name": "CRMToAEP",
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
    "3416976c-a9ca-4bba-901a-1f08f66978ff",
    "38ad80fe-8b06-4938-94f4-d4ee80266b07",
    "d771e9c1-4f26-40dc-8617-ce58c4b53702",
    "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
    "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
    "3000eb99-cd47-43f3-827c-43caf170f015",
    "26d738e0-8963-47ea-aadf-c60de735468a",
    "74a1c565-4e59-48d7-9d67-7c03b8a13137",
    "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
    "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
    "cb66ab34-8619-49cb-96d1-39b37ede86ea",
    "eb13cb25-47ab-407f-ba89-c0125281c563",
    "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
    "37b6bf40-d318-4655-90be-5cd6f65d334b",
    "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
    "221c7626-58f6-4eec-8ee2-042b0226f03b",
    "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
    "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
    "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
    "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
    "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
    "102706fb-a5cd-42ee-afe0-bc42f017ff43",
    "09182899-b429-40c9-a15a-bf3ddbc8ced7",
    "0479cc14-7651-4354-b233-7480606c2ac3",
    "d6b52d86-f0f8-475f-89d4-ce54c8527328",
    "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
    "1fe283f6-9bec-11ea-bb37-0242ac130002",
    "fcad62f3-09b0-41d3-be11-449d5a621b69",
    "ea1c2a08-b722-11eb-8529-0242ac130003",
    "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
    "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
    "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
    "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
    "929e4450-0237-4ed2-9404-b7e1e0a00309",
    "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
    "2fa8af9c-2d1a-43ea-a253-f00a00c74412"
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
      "name": "Copy",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "properties": {
          "deltaColumn": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "dateFormat": {
                "type": "string"
              },
              "timezone": {
                "type": "string"
              }
            },
            "required": [
              "name"
            ]
          }
        },
        "required": [
          "deltaColumn"
        ]
      }
    },
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
            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "deltaColumn": {
            "type": "object",
            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
            "properties": {
              "name": {
                "type": "string"
              },
              "dateFormat": {
                "type": "string"
              },
              "timezone": {
                "type": "string"
              }
            },
            "required": [
              "name"
            ]
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime",
          "deltaColumn"
        ]
      }
    }
}
```

+++

## Creación de un flujo de datos

El último paso para recopilar datos CRM es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

* [ID de conexión de Source](#source)
* [ID de conexión de destino](#target)
* [ID de asignación](#mapping)
* [ID de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una petición POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

Para programar una ingesta, primero debe establecer el valor de la hora de inicio en un tiempo récord en segundos. A continuación, debe establecer el valor de frecuencia en una de las cinco opciones: `once`, `minute`, `hour`, `day` o `week`. El valor de intervalo designa el periodo entre dos ingestas consecutivas y la creación de una ingesta única no requiere que se establezca un intervalo. Para todas las demás frecuencias, el valor del intervalo debe establecerse en igual o mayor que `15`.

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
        "name": "Salesforce dataflow",
        "description": "Salesforce dataflow",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "9a603322-19d2-4de9-89c6-c98bd54eb184"
        ],
        "targetConnectionIds": [
            "4ee890c7-519c-4291-bd20-d64186b62da8"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "500a9b747fcf4908a21917d49bd61780",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `flowSpec.id` | [ID de especificación de flujo](#specs) recuperado en el paso anterior. |
| `sourceConnectionIds` | [Id. de conexión de origen](#source) recuperado en un paso anterior. |
| `targetConnectionIds` | [Id. de conexión de destino](#target-connection) recuperado en un paso anterior. |
| `transformations.params.mappingId` | [ID de asignación](#mapping) recuperado en un paso anterior. |
| `transformations.params.deltaColum` | La columna designada se utiliza para diferenciar entre datos nuevos y existentes. Los datos incrementales se incorporarán en función de la marca de tiempo de la columna seleccionada. El formato admitido para `deltaColumn` es `yyyy-MM-dd HH:mm:ss`. Si usa Microsoft Dynamics, el formato admitido para `deltaColumn` es `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | ID de asignación asociado con la base de datos. |
| `scheduleParams.startTime` | Hora de inicio del flujo de datos en tiempo epoch. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. El valor mínimo del intervalo aceptado para cada frecuencia es el siguiente:<ul><li>**Una vez**: n/a</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Día**: 1</li><li>**Semana**: 1</li></ul> |

**Respuesta**

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""

}
```

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para obtener más información sobre cómo supervisar flujos de datos, consulte el tutorial sobre [supervisión de flujos de datos en la API](../monitor.md)

## Pasos siguientes

Al seguir este tutorial, ha creado un conector de origen para recopilar datos de un sistema CRM de forma programada. Ahora los servicios de Experience Platform descendentes como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace] pueden usar los datos entrantes. Consulte los siguientes documentos para obtener más información:

* [Información general del perfil del cliente en tiempo real](../../../../profile/home.md)
* [Información general del espacio de trabajo de ciencia de datos](../../../../data-science-workspace/home.md)

## Apéndice

En la siguiente sección se enumeran los diferentes conectores de origen CRM y sus especificaciones de conexiones.

### Especificación de conexión

| Nombre del conector | Especificación de conexión |
| -------------- | --------------- |
| [!DNL Microsoft Dynamics] | `38ad80fe-8b06-4938-94f4-d4ee80266b07` |
| [!DNL Salesforce] | `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` |
