---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Crear una nueva especificación de conexión mediante la API de servicio de flujo (Beta)
topic-legacy: tutorial
description: En el siguiente documento se proporcionan los pasos para crear una especificación de conexión mediante la API de servicio de flujo e integrar un nuevo origen a través del SDK de fuentes.
hide: true
hidefromtoc: true
exl-id: 0b0278f5-c64d-4802-a6b4-37557f714a97
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# Cree una nueva especificación de conexión utilizando la variable [!DNL Flow Service] API (Beta)

>[!IMPORTANT]
>
>El SDK de fuentes se encuentra en la versión beta y es posible que su organización no tenga acceso a él todavía. La funcionalidad descrita en esta documentación está sujeta a cambios.

Una especificación de conexión representa la estructura de un origen. Contiene información sobre los requisitos de autenticación de una fuente, define cómo se pueden explorar e inspeccionar los datos de origen y proporciona información sobre los atributos de una fuente determinada. La variable `/connectionSpecs` en la variable [!DNL Flow Service] La API de le permite administrar mediante programación las especificaciones de conexión dentro de su organización.

En el siguiente documento se proporcionan los pasos para crear una especificación de conexión mediante el [!DNL Flow Service] API e integrar una nueva fuente a través del SDK de fuentes.

## Primeros pasos

Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recopilar artefactos

El primer paso para crear una fuente nueva a través de [!DNL Sources SDK] se debe coordinar con el representante de Adobe e identificar los valores correspondientes de la fuente **icono**, **descripción**, **label** y **categoría**.

| Artefactos | Descripción | Ejemplo |
| --- | --- | --- |
| Etiqueta | Nombre de la fuente. | [!DNL MailChimp Members] |
| Descripción | Breve descripción de la fuente. | Cree una conexión entrante activa con su [!DNL Mailchimp Members] por ejemplo, para ingerir datos históricos y programados en Experience Platform. |
| Icono | La imagen o logotipo que representa su origen. El icono se muestra en la renderización de la interfaz de usuario de Platform de su origen. | `mailchimp-members-icon.svg` |
| Categoría | La categoría de la fuente. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Copiar plantilla de especificación de conexión

Una vez que haya recopilado los artefactos requeridos, copie y pegue la plantilla de especificación de conexión a continuación en el editor de texto de su elección y, a continuación, actualice los atributos entre corchetes `{}` con información relevante para su fuente específica.

```json
{
  "name": "generic-rest-extension",
  "type": "generic-rest",
  "description": "{DESCRIPTION}",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "uiAttributes": {
      "apiFeatures": {
        "explorePaginationSupported": false
      }
    }
  },
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "clientId": {
            "description": "Client id of user account.",
            "type": "string"
          },
          "clientSecret": {
            "description": "Client secret of user account.",
            "type": "string",
            "format": "password"
          },
          "accessToken": {
            "description": "Access Token",
            "type": "string",
            "format": "password"
          },
          "refreshToken": {
            "description": "Refresh Token",
            "type": "string",
            "format": "password"
          },
          "expirationDate": {
            "description": "Date of token expiry.",
            "type": "string",
            "format": "date",
            "uiAttributes": {
              "hidden": true
            }
          },
          "accessTokenUrl": {
            "description": "Access token url to fetch access token.",
            "type": "string"
          },
          "requestParameterOverride": {
            "type": "object",
            "description": "Specify parameter to override.",
            "properties": {
              "accessTokenField": {
                "description": "Access token field name to override.",
                "type": "string"
              },
              "refreshTokenField": {
                "description": "Refresh token field name to override.",
                "type": "string"
              },
              "expireInField": {
                "description": "ExpireIn field name to override.",
                "type": "string"
              },
              "authenticationMethod": {
                "description": "Authentication method override.",
                "type": "string",
                "enum": [
                  "GET",
                  "POST"
                ]
              },
              "clientId": {
                "description": "ClientId field name override.",
                "type": "string"
              },
              "clientSecret": {
                "description": "ClientSecret field name override.",
                "type": "string"
              }
            }
          }
        },
        "required": [
          "host",
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
          "username": {
            "description": "Username to connect rest endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect rest endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "protocols"
        },
        "icon": {
          "key": "genericRestIcon"
        },
        "description": {
          "key": "genericRestDescription"
        },
        "label": {
          "key": "genericRestLabel"
        }
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "Http method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "query parameters in json format",
              "example": "{'key':'value','key1':'value1'} in JSON format"
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "header parameters in json format",
          "example": "{'user':'c26f50c88dc035610e6753f807e28e9','x-api-key':'apiKey'}"
        },
        "contentPath": {
          "type": "object",
          "description": "Params required for main collection content.",
          "properties": {
            "path": {
              "description": "path to main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "Params required for sub-array content.",
          "properties": {
            "path": {
              "description": "path to sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "Params required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "Pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "number of records per page to fetch.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "pointer property name",
              "example": "pointer"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "Params required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
  "exploreSpec": {
    "name": "Resource",
    "type": "Resource",
    "requestSpec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object"
    },
    "responseSpec": {
      "$schema": "http: //json-schema.org/draft-07/schema#",
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
```

## Crear una especificación de conexión {#create}

Una vez adquirida la plantilla de especificación de conexión, ahora puede empezar a crear una nueva especificación de conexión rellenando los valores adecuados que correspondan a su origen.

Una especificación de conexión puede dividirse en tres partes diferentes: las especificaciones de autenticación, las especificaciones de origen y las especificaciones de exploración.

Consulte los siguientes documentos para obtener instrucciones sobre cómo rellenar los valores de cada parte de una especificación de conexión:

* [Configurar la especificación de autenticación](../config/authspec.md)
* [Configurar la especificación de origen](../config/sourcespec.md)
* [Configuración de la especificación de exploración](../config/explorespec.md)

Con la información de especificación actualizada, puede enviar la nueva especificación de conexión realizando una solicitud del POST a la `/connectionSpecs` punto final del [!DNL Flow Service] API.

**Formato de API**

```http
POST /connectionSpecs
```

**Solicitud**

La siguiente solicitud es un ejemplo de especificación de conexión de autoría completa para un [!DNL MailChimp] fuente:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MailChimp Members source",
      "description": "MailChimp Members source using generic-rest and SDK",
      "type": "generic-rest",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
          "uiAttributes": {
              "apiFeatures": {
                  "explorePaginationSupported": false
              }
          }
      },
      "authSpec": [
          {
              "name": "OAuth2 Refresh Code",
              "type": "OAuth2RefreshCode",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                  "properties": {
                      "host": {
                          "type": "string",
                          "description": "Enter resource url host path"
                      },
                      "authorizationTestUrl": {
                          "description": "Authorization test url to validate accessToken.",
                          "type": "string"
                      },
                      "accessToken": {
                          "description": "Access Token of mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "host",
                      "accessToken"
                  ]
              }
          },
          {
              "name": "Basic Authentication",
              "type": "BasicAuthentication",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "defines auth params required for connecting to rest service.",
                  "properties": {
                      "host": {
                          "type": "string",
                          "description": "Enter resource url host path."
                      },
                      "username": {
                          "description": "Username to connect mailChimp endpoint.",
                          "type": "string"
                      },
                      "password": {
                          "description": "Password to connect mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "host",
                      "username",
                      "password"
                  ]
              }
          }
      ],
      "sourceSpec": {
          "attributes": {
              "uiAttributes": {
                  "isSource": true,
                  "isPreview": true,
                  "isBeta": true,
                  "icon": {
                      "key": "mailchimpMembersIcon"
                  },
                  "description": {
                      "key": "mailchimpMembersDescription"
                  },
                  "label": {
                      "key": "mailchimpMembersLabel"
                  }
              },
              "urlParams": {
                  "path": "/3.0/lists/${listId}/members",
                  "method": "GET"
              },
              "contentPath": "$.members",
              "paginationParams": {
                  "type": "OFFSET",
                  "limitName": "count",
                  "limitValue": "100",
                  "offSetName": "offset"
              },
              "scheduleParams": {
                  "scheduleStartParamName": "since_last_changed",
                  "scheduleEndParamName": "before_last_changed",
                  "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                  "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
              }
          },
          "spec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object",
              "description": "Define user input parameters to fetch resource values.",
              "properties": {
                  "listId": {
                      "type": "string",
                      "description": "listId for which members need to fetch."
                  }
              }
          }
      },
      "exploreSpec": {
          "name": "Resource",
          "type": "Resource",
          "requestSpec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object"
          },
          "responseSpec": {
              "$schema": "http: //json-schema.org/draft-07/schema#",
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
  }'
```

**Respuesta**

Una respuesta correcta devuelve la especificación de conexión recién creada, incluyendo su `id`.

```json
{
    "id": "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55",
    "createdAt": 1633388930134,
    "updatedAt": 1633388930134,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "MailChimp Members source",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "type": "generic-rest",
    "authSpec": [
        {
            "name": "OAuth2 Refresh Code",
            "type": "OAuth2RefreshCode",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path"
                    },
                    "authorizationTestUrl": {
                        "description": "Authorization test url to validate accessToken.",
                        "type": "string"
                    },
                    "accessToken": {
                        "description": "Access Token of mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "accessToken"
                ]
            }
        },
        {
            "name": "Basic Authentication",
            "type": "BasicAuthentication",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "defines auth params required for connecting to rest service.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path."
                    },
                    "username": {
                        "description": "Username to connect mailChimp endpoint.",
                        "type": "string"
                    },
                    "password": {
                        "description": "Password to connect mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "username",
                    "password"
                ]
            }
        }
    ],
    "sourceSpec": {
        "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "Define user input parameters to fetch resource values.",
            "properties": {
                "listId": {
                    "type": "string",
                    "description": "listId for which members need to fetch."
                }
            }
        },
        "attributes": {
            "uiAttributes": {
                "isSource": true,
                "isPreview": true,
                "isBeta": true,
                "icon": {
                    "key": "mailchimpMembersIcon"
                },
                "description": {
                    "key": "mailchimpMembersDescription"
                },
                "label": {
                    "key": "mailchimpMembersLabel"
                }
            },
            "urlParams": {
                "path": "/3.0/lists/${listId}/members",
                "method": "GET"
            },
            "contentPath": {
                    "path": "$.members",
                    "skipAttributes": [
                      "_links",
                      "total_items",
                      "list_id"
                    ],
                    "overrideWrapperAttribute": "member"
                  },
            "paginationParams": {
                "type": "OFFSET",
                "limitName": "count",
                "limitValue": "100",
                "offSetName": "offset"
            },
            "scheduleParams": {
                "scheduleStartParamName": "since_last_changed",
                "scheduleEndParamName": "before_last_changed",
                "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
            }
        }
    },
    "exploreSpec": {
        "name": "Resource",
        "type": "Resource",
        "requestSpec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object"
        },
        "responseSpec": {
            "$schema": "http: //json-schema.org/draft-07/schema#",
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
    },
    "attributes": {
        "uiAttributes": {
            "apiFeatures": {
                "explorePaginationSupported": false
            }
        }
    }
}
```

## Pasos siguientes

Ahora que ha creado una nueva especificación de conexión, debe agregar su ID de especificación de conexión correspondiente a una especificación de flujo existente. Consulte el tutorial en [actualizar especificaciones de flujo](./update-flow-specs.md) para obtener más información.

Para realizar modificaciones en la especificación de conexión que ha creado, consulte el tutorial sobre [actualización de las especificaciones de conexión](./update-connection-specs.md).
