---
title: Crear Un Flujo De Datos Para Introducir Datos De Un CRM En Experience Platform
description: Aprenda a utilizar la API de Flow Service para crear un flujo de datos e introducir datos de origen en Experience Platform.
exl-id: b07dd640-bce6-4699-9d2b-b7096746934a
source-git-commit: b4f8d44c3ce9507ff158cf051b7a4b524b293c64
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 2%

---

# Crear un flujo de datos para introducir datos de un CRM a Experience Platform

Lea esta guía para aprender a crear un flujo de datos e ingerir datos en Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Ingesta por lotes](../../../../ingestion/batch-ingestion/overview.md): Descubra cómo cargar grandes volúmenes de datos por lotes de forma rápida y eficaz.
* [Servicio de catálogo](../../../../catalog/datasets/overview.md): organice y realice un seguimiento de sus conjuntos de datos en Experience Platform.
* [Preparación de datos](../../../../data-prep/home.md): transforme y asigne los datos entrantes para que coincidan con los requisitos de esquema.
* [Flujos de datos](../../../../dataflows/home.md): configure y administre las canalizaciones que mueven sus datos de orígenes a destinos.
* [Esquemas del modelo de datos de experiencia (XDM)](../../../../xdm/home.md): Estructure los datos con esquemas XDM para que estén listos para su uso en Experience Platform.
* [Zonas protegidas](../../../../sandboxes/home.md): Realice pruebas y desarrolle de forma segura en entornos aislados sin afectar a los datos de producción.
* [Fuentes](../../../home.md): Aprenda a conectar las fuentes de datos externas a Experience Platform.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, lea la guía sobre [introducción a las API de Experience Platform](../../../../landing/api-guide.md).

### Crear conexión base {#base}

Para crear un flujo de datos para su origen, necesitará una cuenta de origen totalmente autenticada y su ID de conexión base correspondiente. Si no tiene este identificador, visite el [catálogo de orígenes](../../../home.md) para encontrar una lista de orígenes para los que puede crear una conexión base.

### Creación de un esquema XDM de destino {#target-schema}

Un esquema del Modelo de datos de experiencia (XDM) proporciona una forma estandarizada de organizar y describir los datos de experiencia del cliente dentro de Experience Platform. Para introducir los datos de origen en Experience Platform, primero debe crear un esquema XDM de destino que defina la estructura y los tipos de datos que desea introducir. Este esquema sirve como modelo para el conjunto de datos de Experience Platform donde residirán los datos ingeridos.

Se puede crear un esquema XDM de destino realizando una petición POST a la [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, lea las siguientes guías:

* [Cree un esquema con la API](../../../../xdm/api/schemas.md).
* [Crear un esquema con la interfaz de usuario](../../../../xdm/tutorials/create-schema-ui.md).

Una vez creado, el esquema XDM de destino `$id` se requerirá más adelante para el conjunto de datos de destino y la asignación.

### Crear un conjunto de datos de destinatario {#target-dataset}

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente estructurada como una tabla con columnas (esquema) y filas (campos). Los datos que se incorporan correctamente a Experience Platform se almacenan dentro del lago de datos como conjuntos de datos. Durante este paso, puede crear un nuevo conjunto de datos o utilizar uno existente.

Puede crear un conjunto de datos de destino realizando una petición POST a la [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), al mismo tiempo que proporciona el ID del esquema de destino en la carga útil. Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, lea la guía sobre [crear un conjunto de datos mediante la API](../../../../catalog/api/create-dataset.md).

>[!TIP]
>
>Si desea introducir los datos en el perfil del cliente en tiempo real, debe asegurarse de que tanto los esquemas XDM de destino como el conjunto de datos de destino estén habilitados para el perfil.

+++Seleccione esta opción para ver el ejemplo

**Formato de API**

```HTTP
POST /dataSets
```

**Solicitud**

El siguiente ejemplo muestra cómo crear un conjunto de datos de destinatario habilitado para la ingesta de Perfil del cliente en tiempo real. En esta solicitud, la propiedad `unifiedProfile` se establece en `true` (en el objeto `tags`), lo que indica a Experience Platform que incluya el conjunto de datos en el perfil del cliente en tiempo real.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Un nombre descriptivo para el conjunto de datos de destinatario. Utilice un nombre claro y único para que sea más fácil identificar y administrar su conjunto de datos en futuras operaciones. |
| `schemaRef.id` | El ID del esquema XDM de destino. |
| `tags.unifiedProfile` | Un valor booleano que informa a Experience Platform si los datos deben ingerirse en el Perfil del cliente en tiempo real. |

**Respuesta**

Una respuesta correcta devuelve el ID del conjunto de datos de destinatario. Este ID se necesita más adelante para crear una conexión de destino.

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## Crear una conexión de origen {#source}

Una conexión de origen define cómo se introducen los datos en Experience Platform desde un origen externo. Especifica el sistema de origen y el formato de los datos entrantes, y hace referencia a una conexión base que contiene detalles de autenticación. Cada conexión de origen es única para su organización.

* En el caso de los orígenes basados en archivos (como el almacenamiento en la nube), una conexión de origen puede incluir configuraciones como delimitador de columna, tipo de codificación, tipo de compresión, expresiones regulares para la selección de archivos y si se deben introducir archivos de forma recursiva.
* Para los orígenes basados en tablas (como bases de datos, CRM y proveedores de automatización de marketing), una conexión de origen puede especificar detalles como el nombre de la tabla y las asignaciones de columnas.

Para crear una conexión de origen, realice una petición POST al extremo `/sourceConnections` de la API [!DNL Flow Service] y proporcione el identificador de conexión base, el identificador de especificación de conexión y la ruta al archivo de datos de origen.

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
    "name": "ACME source connection",
    "description": "A source connection for ACME contact data",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
      "columns": [
        {
          "name": "TestID",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Name",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Datefield",
          "type": "string",
          "meta:xdmType": "date-time",
          "xdm": {
            "type": "string",
            "format": "date-time"
          }
        }
      ]
    },
    "connectionSpec": {
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Un nombre descriptivo para la conexión de origen. Utilice un nombre claro y único para que sea más fácil identificar y administrar la conexión en futuras operaciones. |
| `description` | Descripción opcional que puede agregar para proporcionar información adicional sobre la conexión de origen. |
| `baseConnectionId` | El `id` de su conexión base. Puede recuperar este ID autenticando su origen en Experience Platform mediante la API [!DNL Flow Service]. |
| `data.format` | El formato de los datos. Establezca este valor en `tabular` para orígenes basados en tablas (como bases de datos, CRM y proveedores de automatización de marketing). |
| `params.tableName` | El nombre de la tabla de la cuenta de origen que desea introducir en Experience Platform. |
| `params.columns` | Las columnas de tabla específicas de datos que desea introducir en Experience Platform. |
| `connectionSpec.id` | Id. de especificación de conexión del origen que está utilizando. |

**Respuesta**

Una respuesta correcta devuelve el ID de la conexión de origen. Este ID es necesario para crear un flujo de datos e introducir los datos.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Creación de una conexión de destino {#target}

Una conexión de destino representa la conexión con el destino donde aterrizan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija asociado al lago de datos. Este id. de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Un nombre descriptivo para la conexión de destino. Utilice un nombre claro y único para que sea más fácil identificar y administrar la conexión en futuras operaciones. |
| `description` | Una descripción opcional que puede agregar para proporcionar información adicional sobre la conexión de destino. |
| `data.schema.id` | El ID del esquema XDM de destino. |
| `params.dataSetId` | El ID del conjunto de datos de destinatario. |
| `connectionSpec.id` | ID de especificación de conexión del lago de datos. Este identificador se corrigió: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

## Asignación {#mapping}

A continuación, asigne los datos de origen al esquema de destino al que se adhiere el conjunto de datos de destino. Para crear una asignación, realice una petición POST al extremo `mappingSets` de la [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Incluya el ID del esquema XDM de destino y los detalles de los conjuntos de asignaciones que desee crear.

**Formato de API**

```http
POST /mappingSets
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
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [
          {
              "destinationXdmPath": "_id",
              "sourceAttribute": "TestID",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.fullName",
              "sourceAttribute": "Name",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.birthDate",
              "sourceAttribute": "Datefield",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          }
      ]
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `xdmSchema` | El `$id` del esquema XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificaciones de flujo de datos {#flow-specs}

Para poder crear un flujo de datos, primero debe recuperar las especificaciones del flujo de datos que se correspondan con su origen. Para recuperar esta información, realice una petición GET al extremo `/flowSpecs` de la API [!DNL Flow Service].

**Formato de API**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| Parámetro de consulta | Descripción |
| --- | --- |
| `property=name=="{NAME}"` | El nombre de la especificación del flujo de datos. <ul><li>Para orígenes basados en archivos (como el almacenamiento en la nube), establezca este valor en `CloudStorageToAEP`.</li><li>Para orígenes basados en tablas (como bases de datos, CRM y proveedores de automatización de marketing), establezca este valor en `CRMToAEP`.</li></ul> |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos responsable de importar datos de su origen a Experience Platform. La respuesta incluye la especificación de flujo única `id` necesaria para crear un nuevo flujo de datos.

Para asegurarse de que está utilizando la especificación de flujo de datos correcta, compruebe la matriz `items.sourceConnectionSpecIds` en la respuesta. Confirme que el ID de especificación de conexión del origen se incluye en esta lista.

+++Seleccionar para ver

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
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
            "transformationSpecs": [
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
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## Creación de un flujo de datos {#dataflow}

Un flujo de datos es una canalización configurada que transfiere datos entre servicios de Experience Platform. Define cómo se incorporan los datos desde fuentes externas (como bases de datos, almacenamiento en la nube o API), se procesan y se enrutan a conjuntos de datos de destino. Estos conjuntos de datos los utilizan servicios como Identity Service, Real-Time Customer Profile y Destinations para la activación y el análisis.

Para crear un flujo de datos, deberá proporcionar valores para los siguientes elementos:

* [ID de conexión de Source](#source)
* [ID de conexión de destino](#target)
* [ID de asignación](#mapping)
* [ID de especificación de flujo de datos](#flow-specs)

Durante este paso, puede utilizar los siguientes parámetros en `scheduleParams` para configurar una programación de ingesta para el flujo de datos:

| Parámetro de programación | Descripción |
| --- | --- |
| `startTime` | Tiempo de epoch (en segundos) en que debe iniciarse el flujo de datos. |
| `frequency` | La frecuencia de la ingesta. Configure la frecuencia para indicar con qué frecuencia debe ejecutarse el flujo de datos. Puede establecer su frecuencia en: <ul><li>`once`: establezca su frecuencia en `once` para crear una ingesta única. La configuración de intervalo y relleno no está disponible para trabajos de ingesta únicos. De forma predeterminada, la frecuencia de programación se establece en una vez.</li><li>`minute`: establezca su frecuencia en `minute` para programar el flujo de datos e ingerir datos por minuto.</li><li>`hour`: establezca su frecuencia en `hour` para programar el flujo de datos e ingerir datos por hora.</li><li>`day`: establezca su frecuencia en `day` para programar el flujo de datos e ingerir datos todos los días.</li><li>`week`: establezca su frecuencia en `week` para programar el flujo de datos e ingerir datos por semana.</li></ul> |
| `interval` | Intervalo entre ingestas consecutivas (requerido para todas las frecuencias excepto `once`). Configure el intervalo para establecer el lapso de tiempo entre cada ingesta. Por ejemplo, si la frecuencia se establece en día y el intervalo es 15, el flujo de datos se ejecutará cada 15 días. No puede establecer el intervalo en cero. El valor mínimo del intervalo aceptado para cada frecuencia es el siguiente:<ul><li>`once`: n/a</li><li>`minute`: 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | Indica si se deben introducir datos históricos anteriores a `startTime`. |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
      "flowSpec": {
          "id": "14518937-270c-4525-bdec-c2ba7cce3860",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "b7581b59-c603-4df1-a689-d23d7ac440f3"
      ],
      "targetConnectionIds": [
          "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
      ],
      "transformations": [
          {
              "name": "Copy",
              "params": {
                  "deltaColumn": {
                      "name": "Datefield",
                      "dateFormat": "YYYY-MM-DD",
                      "timezone": "UTC"
                  }
              }
          },
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1612310466",
          "frequency":"minute",
          "interval":"15",
          "backfill": "true"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Un nombre descriptivo para el flujo de datos. Utilice un nombre claro y único para que sea más fácil identificar y administrar el flujo de datos en futuras operaciones. |
| `description` | Una descripción opcional que puede agregar para proporcionar información adicional sobre el flujo de datos. |
| `flowSpec.id` | El ID de la especificación de flujo que corresponde a su origen. |
| `sourceConnectionIds` | Identificador de conexión de origen que se generó en un paso anterior. |
| `targetConnectionIds` | El ID de conexión de destino generado en un paso anterior. |
| `transformations.params.deltaColum` | La columna designada se utiliza para diferenciar entre datos nuevos y existentes. Los datos incrementales se incorporarán en función de la marca de tiempo de la columna seleccionada. El formato admitido para `deltaColumn` es `yyyy-MM-dd HH:mm:ss`. Para [!DNL Microsoft Dynamics], el formato admitido para `deltaColumn` es `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.deltaColumn.dateFormat` | Formato de fecha que se debe seguir para la columna delta. |
| `transformations.params.deltaColumn.timeZone` | Zona horaria que se utiliza al interpretar los valores de la columna delta. |
| `transformations.params.mappingId` | ID de asignación generado en un paso anterior. |
| `scheduleParams.startTime` | Hora de inicio del flujo de datos en tiempo epoch (segundos desde Unix epoch). Determina cuándo comenzará la primera ejecución del flujo de datos. |
| `scheduleParams.frequency` | Frecuencia con la que se ejecutará el flujo de datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | El intervalo entre ejecuciones de flujo de datos consecutivas, en función de la frecuencia seleccionada. Debe ser un entero distinto de cero. Por ejemplo, si la frecuencia se establece en minutos y el intervalo es 15, el flujo de datos se ejecutará cada 15 minutos. |
| `scheduleParams.backfill` | Un valor booleano (`true` o `false`) que determina si se deben introducir datos históricos (relleno) cuando se crea el flujo de datos por primera vez. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado.

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### Utilice la interfaz de usuario para validar el flujo de trabajo de API {#validate-in-ui}

Puede utilizar la interfaz de usuario de Experience Platform para validar la creación del flujo de datos. Vaya al catálogo *[!UICONTROL Sources]* en la interfaz de usuario de Experience Platform y, a continuación, seleccione **[!UICONTROL Dataflows]** de las pestañas del encabezado. A continuación, use la columna [!UICONTROL Nombre de flujo de datos] y busque el flujo de datos que creó con la API [!DNL Flow Service].

![Interfaz de flujos de datos del área de trabajo de orígenes en la interfaz de usuario de Experience Platform](../../../images/tutorials/validations/dataflows-interface.png)

Puede validar aún más su flujo de datos a través de la interfaz [!UICONTROL actividad de flujo de datos]. Utilice el carril derecho para ver la información de [!UICONTROL uso de API] de su flujo de datos. Esta sección muestra el mismo ID de flujo de datos, ID de conjunto de datos e ID de asignación que se generó durante el proceso de creación de flujo de datos en [!DNL Flow Service].

![Página de vista de flujo de datos del área de trabajo de orígenes.](../../../images/tutorials/validations/api-usage.png)

## Próximos pasos

Este tutorial lo guió a través del proceso de creación de un flujo de datos en Experience Platform mediante la API [!DNL Flow Service]. Ha aprendido a crear y configurar los componentes necesarios, incluido el esquema XDM de destino, el conjunto de datos, la conexión de origen, la conexión de destino y el propio flujo de datos. Al seguir estos pasos, puede automatizar la ingesta de datos de fuentes externas a Experience Platform, lo que permite servicios descendentes como Perfil del cliente en tiempo real y Destinos para aprovechar los datos ingeridos para casos de uso avanzados.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar su rendimiento directamente en la interfaz de usuario de Experience Platform. Esto incluye el seguimiento de las tasas de ingesta, las métricas de éxito y cualquier error que se produzca. Para obtener más información sobre cómo supervisar el flujo de datos, visite el tutorial sobre [supervisar cuentas y flujos de datos](../../../../dataflows/ui/monitor-sources.md).

### Actualizar el flujo de datos

Para actualizar configuraciones para la programación, asignación o información general de sus flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen](../../api/update-dataflows.md).

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos](../../api/delete.md).
