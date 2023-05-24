---
title: Creación de borradores de la API de entidades de Flow Service
description: Obtenga información sobre cómo crear borradores de la conexión base, la conexión de origen, la conexión de destino y el flujo de datos mediante la API de Flow Service
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: ebd650355a5a4c2a949739384bfd5c8df9577075
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 4%

---

# Crear borradores de su [!DNL Flow Service] entidades que utilizan la API

Puede usar el complemento `mode=draft` parámetro de consulta en [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) para configurar su [!DNL Flow Service] entidades como las conexiones base, las conexiones de origen, las conexiones de destino y los flujos de datos a un estado de borrador.

Los borradores se pueden actualizar más adelante con información nueva y, a continuación, publicar una vez que estén listos, utilizando `op=publish` parámetro de consulta.

Este tutorial proporciona pasos sobre cómo configurar las [!DNL Flow Service] entidades de a un estado de borrador y permiten pausar y guardar los flujos de trabajo para completarlos más adelante.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

### Compruebe la compatibilidad con el modo de borrador

También debe comprobar si el ID de especificación de conexión y el ID de especificación de flujo correspondiente del origen que está utilizando están habilitados para el modo borrador.

>[!BEGINTABS]

>[!TAB Búsqueda de detalles de especificaciones de conexión]

+++Solicitud La siguiente solicitud recupera la información de especificación de conexión para [!DNL Azure File Storage]:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve la información de especificación de conexión del origen. Para comprobar si el modo de borrador es compatible con el origen, compruebe que la variable `items[0].attributes.isDraftModeSupported` tiene un valor de `true`.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
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

>[!TAB Búsqueda de detalles de especificaciones de flujo]

+++Solicitud La siguiente solicitud recupera los detalles de especificación de flujo para una fuente de almacenamiento en la nube:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve la información de especificación de flujo del origen. Para comprobar si el modo de borrador es compatible con el origen, compruebe que la variable `items[0].attributes.isDraftModeSupported` tiene un valor de `true`.

```json {line-numbers="true" start-line="1" highlight="167"}
{
  "items": [
    {
      "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
      "name": "CloudStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
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
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
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
      "attributes": {
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

>[!ENDTABS]



## Crear una conexión base de borrador {#create-a-draft-base-connection}

Para crear una conexión base de borrador, realice una solicitud de POST al `/connections` punto final del [!DNL Flow Service] API y proporcionar `mode=draft` como parámetro de consulta.

**Formato de API**

```http
POST /connections?mode=draft
```

| Parámetro | Descripción |
| --- | --- |
| `mode` | Parámetro de consulta proporcionado por el usuario que decide el estado de la conexión base. Para establecer una conexión base como borrador, establezca `mode` hasta `draft`. |

**Solicitud**

La siguiente solicitud crea una conexión base de borrador para [!DNL Azure File Storage] fuente:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**Respuesta**

Una respuesta correcta devuelve el ID de conexión base y la etiqueta correspondiente para la conexión base de borrador. Puede utilizar este ID más adelante para actualizar y publicar la conexión base.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Publicar el borrador de la conexión base {#publish-your-draft-base-connection}

Una vez que el borrador esté listo para publicarse, realice una solicitud de POST al `/connections` y proporcione el ID de la conexión base de borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `op` | Operación de acción que actualiza el estado de la conexión base consultada. Para publicar un borrador de conexión base, establezca `op` hasta `publish`. |

**Solicitud**

La siguiente solicitud publica el borrador de conexión base para [!DNL Azure File Storage] que se creó en un paso anterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el ID y la etiqueta correspondiente para la conexión base publicada.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Crear una conexión de origen de borrador {#create-a-draft-source-connection}

Para crear una conexión de origen de borrador, realice una solicitud de POST al `/sourceConnections` punto final del [!DNL Flow Service] API y proporcionar `mode=draft` como parámetro de consulta.

**Formato de API**

```http
POST /sourceConnections?mode=draft
```

| Parámetro | Descripción |
| --- | --- |
| `mode` | Parámetro de consulta proporcionado por el usuario que decide el estado de la conexión de origen. Para establecer una conexión de origen como borrador, establezca `mode` hasta `draft`. |

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de origen y la etiqueta correspondiente para la conexión de origen de borrador. Puede utilizar este ID más adelante para actualizar y publicar la conexión de origen.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Publicar la conexión de origen de borrador {#publish-your-draft-source-connection}

>[!NOTE]
>
>No puede publicar una conexión de origen si su conexión base asociada sigue en estado de borrador. Asegúrese de que la conexión base se publique primero, antes de publicar la conexión de origen.

Una vez que el borrador esté listo para publicarse, realice una solicitud de POST al `/sourceConnections` y proporcione el ID de la conexión de origen de borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `op` | Operación de acción que actualiza el estado de la conexión de origen consultada. Para publicar una conexión de origen de borrador, establezca `op` hasta `publish`. |

**Solicitud**

La siguiente solicitud publica la conexión de origen de borrador para [!DNL Azure File Storage] que se creó en un paso anterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el ID y la etiqueta correspondiente para la conexión de origen publicada.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Crear una conexión de destino de borrador {#create-a-draft-target-connection}

Para crear una conexión de destino de borrador, realice una solicitud de POST al `/targetConnections` punto final del [!DNL Flow Service] API y proporcionar `mode=draft` como parámetro de consulta.

**Formato de API**

```http
POST /targetConnections?mode=draft
```

| Parámetro | Descripción |
| --- | --- |
| `mode` | Parámetro de consulta proporcionado por el usuario que decide el estado de la conexión de destino. Para establecer una conexión de destino como borrador, establezca `mode` hasta `draft`. |

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de destino y la etiqueta correspondiente para el borrador de conexión de destino. Puede utilizar este ID más adelante para actualizar y publicar la conexión de destino.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Publicación del borrador de la conexión de destino {#publish-your-draft-target-connection}

>[!NOTE]
>
>No puede publicar una conexión de destino si su conexión base asociada sigue en estado de borrador. Asegúrese de que la conexión base se publique primero, antes de publicar la conexión de destino.

Una vez que el borrador esté listo para publicarse, realice una solicitud de POST al `/targetConnections` y proporcione el ID de la conexión de destino de borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `op` | Operación de acción que actualiza el estado de la conexión de destino consultada. Para publicar un borrador de conexión de destino, establezca `op` hasta `publish`. |

**Solicitud**

La siguiente solicitud publica el borrador de conexión de destino para [!DNL Azure File Storage] que se creó en un paso anterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el ID y la etiqueta correspondiente para la conexión de destino publicada.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Crear un flujo de datos de borrador {#create-a-draft-dataflow}

Para establecer un flujo de datos como borrador, realice una solicitud de POST a `/flows` al añadir el `mode=draft` como parámetro de consulta. Esto le permite crear un flujo de datos y guardarlo como borrador.

**Formato de API**

```http
POST /flows?mode=draft
```

| Parámetro | Descripción |
| --- | --- |
| `mode` | Parámetro de consulta proporcionado por el usuario que decide el estado del flujo de datos. Para establecer un flujo de datos como borrador, establezca `mode` hasta `draft`. |

**Solicitud**

La siguiente solicitud crea un flujo de datos de borrador.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**Respuesta**

Una respuesta correcta devuelve el ID de flujo y la etiqueta correspondiente para el flujo de datos de borrador. Puede utilizar este ID más adelante para actualizar y publicar el flujo de datos.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Publicación del flujo de datos de borrador {#publish-your-draft-dataflow}

>[!NOTE]
>
>No puede publicar un flujo de datos si sus conexiones de origen y destino asociadas siguen en estado de borrador. Asegúrese de que las conexiones de origen y destino se publiquen primero antes de publicar el flujo de datos.

Una vez que el borrador esté listo para publicarse, realice una solicitud de POST al `/flows` al proporcionar el ID del flujo de datos de borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `op` | Operación de acción que actualiza el estado del flujo de datos consultado. Para publicar un flujo de datos de borrador, establezca `op` hasta `publish`. |

**Solicitud**

La siguiente solicitud publica el flujo de datos de borrador.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el ID y el correspondiente `etag` del flujo de datos.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha aprendido a crear borradores de su [!DNL Flow Service] y publicar estos borradores. Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../home.md).