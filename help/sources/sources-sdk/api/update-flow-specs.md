---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Actualización de especificaciones de flujo mediante la API de servicio de flujo (Beta)
topic-legacy: developer guide
description: El siguiente documento proporciona pasos sobre cómo recuperar y actualizar las especificaciones de flujo mediante la API de servicio de flujo para el SDK de fuentes.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 2%

---

# Actualización de las especificaciones de flujo mediante [!DNL Flow Service] API (Beta)

>[!IMPORTANT]
>
>El SDK de fuentes se encuentra en la versión beta y es posible que su organización no tenga acceso a él todavía. La funcionalidad descrita en esta documentación está sujeta a cambios.

Una vez que haya generado un nuevo ID de especificación de conexión, debe añadir este ID a una especificación de flujo para crear un flujo de datos.

Las especificaciones de flujo contienen información que define un flujo, incluidos los ID de conexión de origen y destino que admite, las especificaciones de transformación que deben aplicarse a los datos y los parámetros de programación necesarios para generar un flujo. Puede editar las especificaciones de flujo mediante el uso de `/flowSpecs` punto final.

El siguiente documento proporciona pasos sobre cómo recuperar y actualizar las especificaciones de flujo mediante el [!DNL Flow Service] API para el SDK de fuentes.

## Primeros pasos

Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Buscar una especificación de flujo {#lookup}

Fuentes creadas con `generic-rest-extension` todas utilizan la variable `RestStorageToAEP` especificación de flujo. Esta especificación de flujo se puede recuperar realizando una solicitud de GET al `/flowSpecs/` y proporcionando la variable `flowSpec.id` de `6499120c-0b15-42dc-936e-847ea3c24d72`.

**Formato de API**

```http
GET /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Solicitud**

La siguiente solicitud recupera el `6499120c-0b15-42dc-936e-847ea3c24d72` especificación de conexión.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo consultada.

```json
{
  "items": [
      {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "createdAt": 1633080822911,
          "updatedAt": 1633080822911,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "{SANDBOX_ID}",
          "sandboxName": "{SANDBOX_NAME}",
          "imsOrgId": "{IMS_ORG}",
          "name": "RestStorageToAEP",
          "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
          "version": "1.0",
          "sourceConnectionSpecIds": [
              "2d46966e-4fcc-4015-9f9e-a67594e395a3"
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
      },
  ]
}
```

## Actualización de una especificación de flujo {#update}

Puede actualizar los campos de una especificación de conexión mediante una operación de PUT. Al actualizar una especificación de conexión mediante una solicitud del PUT, el cuerpo debe incluir todos los campos necesarios al crear una nueva especificación de conexión en una solicitud del POST.

>[!IMPORTANT]
>
>Debe actualizar la lista de `sourceConnectionSpecIds` de la especificación de flujo que corresponde a un nuevo origen cada vez que se crea un nuevo origen. Esto garantiza que la nueva fuente sea compatible con una especificación de flujo existente, lo que le permite completar el proceso de creación de flujo de datos con la nueva fuente.

**Formato de API**

```http
PUT /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Solicitud**

La siguiente solicitud actualiza la especificación de flujo de `6499120c-0b15-42dc-936e-847ea3c24d72` para incluir el ID de especificación de conexión `f6c0de0c-0a42-4cd9-9139-8768bf2f1b55`.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
`     "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "name": "RestStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
      ]
    }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo consultada, incluida su lista actualizada de `sourceConnectionSpecIds`.

```json
{
    "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{IMS_ORG}",
    "name": "RestStorageToAEP",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
```

## Pasos siguientes

Con la nueva especificación de conexión agregada a la especificación de flujo adecuada, ahora puede continuar probando y enviando el nuevo origen. Consulte la guía de [prueba y envío de una nueva fuente](./overview.md#submit) para obtener más información.