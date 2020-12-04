---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Políticas
topic: developer guide
description: Una vez creadas las acciones de marketing y definidas las políticas, puede utilizar la API de servicio de directivas para evaluar si determinadas acciones infringen alguna política. Las restricciones devueltas toman la forma de un conjunto de directivas que se violarían al intentar la acción de marketing en los datos especificados que contienen etiquetas de uso de datos.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---


# Objetivos de la evaluación de políticas

Una vez creadas las acciones de marketing y definidas las políticas, puede utilizar la [!DNL Policy Service] API para evaluar si determinadas acciones infringen alguna política. Las restricciones devueltas toman la forma de un conjunto de directivas que se violarían al intentar la acción de marketing en los datos especificados que contienen etiquetas de uso de datos.

De forma predeterminada, solo las directivas cuyo estado está configurado para `ENABLED` participar en la evaluación. Sin embargo, puede utilizar el parámetro de consulta `?includeDraft=true` para incluir `DRAFT` directivas en la evaluación.

Las solicitudes de evaluación se pueden realizar de una de las tres maneras siguientes:

1. Dada una acción de marketing y un conjunto de etiquetas de uso de datos, ¿la acción infringe alguna política?
1. Dado que se trata de una acción de marketing y uno o más conjuntos de datos, ¿la acción infringe alguna política?
1. Dada una acción de marketing, uno o más conjuntos de datos y un subconjunto de uno o más campos dentro de cada uno de esos conjuntos de datos, ¿la acción infringe alguna política?

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte la guía [de](./getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Evaluar las infracciones de directivas mediante etiquetas de uso de datos {#labels}

Puede evaluar las infracciones de directiva en función de la presencia de un conjunto específico de etiquetas de uso de datos mediante el uso del parámetro de `duleLabels` consulta en una solicitud de GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a probar con un conjunto de etiquetas de uso de datos. Puede recuperar una lista de acciones de marketing disponibles realizando una solicitud de [GET al extremo](./marketing-actions.md#list)de acciones de marketing. |
| `{LABELS_LIST}` | Una lista separada por comas de los nombres de las etiquetas de uso de datos para probar la acción de mercadotecnia. Por ejemplo: `duleLabels=C1,C2,C3`<br><br>Tenga en cuenta que los nombres de las etiquetas distinguen entre mayúsculas y minúsculas. Asegúrese de que está utilizando las mayúsculas y minúsculas correctas al enumerarlas en el `duleLabels` parámetro. |

**Solicitud**

La solicitud de ejemplo siguiente evalúa una acción de mercadotecnia con las etiquetas C1 y C3.

>[!IMPORTANT]
>
>Tenga en cuenta los `AND` operadores y `OR` en sus expresiones de directiva. En el ejemplo siguiente, si alguna de las etiquetas (`C1` o `C3`) hubiera aparecido sola en la solicitud, la acción de marketing no habría violado esta política. Se necesitan ambas etiquetas (`C1` y `C3`) para devolver la directiva violada. Asegúrese de que está evaluando las políticas cuidadosamente y definiendo las expresiones de políticas con el mismo cuidado.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta incluye una `violatedPolicies` matriz que contiene los detalles de las directivas que se infringieron como resultado de realizar la acción de mercadotecnia con las etiquetas proporcionadas. Si no se infringe ninguna directiva, la matriz `violatedPolicies` estará vacía.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Evaluar para violaciones de políticas usando conjuntos de datos {#datasets}

Puede evaluar las infracciones de política en base a un conjunto de uno o más conjuntos de datos desde los que se pueden recopilar las etiquetas de uso de datos. Esto se realiza realizando una solicitud de POST al extremo para una acción de marketing específica y proporcionando una lista de ID de conjuntos de datos dentro del cuerpo de la solicitud. `/constraints`

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a probar con uno o varios conjuntos de datos. Puede recuperar una lista de acciones de marketing disponibles realizando una solicitud de [GET al extremo](./marketing-actions.md#list)de acciones de marketing. |

**Solicitud**

La siguiente solicitud realiza la acción de mercadotecnia con un conjunto de tres conjuntos de datos para evaluar cualquier infracción de directiva. `crossSiteTargeting`

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| Propiedad | Descripción |
| --- | --- |
| `entityType` | El tipo de entidad cuyo ID se indica en la `entityId` propiedad del mismo nivel. Actualmente, el único valor aceptado es `dataSet`. |
| `entityId` | ID de un conjunto de datos para probar la acción de marketing. Se puede obtener una lista de conjuntos de datos y sus ID correspondientes mediante una solicitud de GET al `/dataSets` extremo en la [!DNL Catalog Service] API. See the guide on [listing [!DNL Catalog] objects](../../catalog/api/list-objects.md) for more information. |

**Respuesta**

Una respuesta correcta incluye una `violatedPolicies` matriz que contiene los detalles de las directivas que se violaron como resultado de realizar la acción de mercadotecnia con los conjuntos de datos proporcionados. Si no se infringe ninguna directiva, la matriz `violatedPolicies` estará vacía.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `duleLabels` | El objeto response incluye una `duleLabels` matriz que contiene una lista consolidada de todas las etiquetas que se encuentran dentro de los conjuntos de datos especificados. Esta lista incluye rótulos a nivel de conjunto de datos y campo en todos los campos dentro del conjunto de datos. |
| `discoveredLabels` | La respuesta también incluye una `discoveredLabels` matriz que contiene objetos para cada conjunto de datos, y que `datasetLabels` se desglosan en rótulos de nivel de conjunto de datos y campo. Cada etiqueta de nivel de campo muestra la ruta al campo específico con esa etiqueta. |

## Evaluar para infracciones de directivas usando campos de conjunto de datos específicos {#fields}

Puede evaluar las infracciones de política en función de un subconjunto de campos dentro de uno o más conjuntos de datos, de modo que solo se evalúen las etiquetas de uso de datos aplicadas a esos campos.

Cuando evalúe políticas mediante campos de conjunto de datos, tenga en cuenta lo siguiente:

* **Los nombres de los campos distinguen entre mayúsculas y minúsculas**: Al proporcionar campos, deben escribirse exactamente como aparecen en el conjunto de datos (por ejemplo, `firstName` vs `firstname`).
* **Herencia** de etiquetas de conjunto de datos: Los campos individuales de un conjunto de datos heredan cualquier etiqueta que se haya aplicado en el nivel de conjunto de datos. Si las evaluaciones de directivas no se devuelven como se espera, asegúrese de comprobar si hay etiquetas que se hayan heredado del nivel de conjunto de datos hasta los campos, además de las aplicadas en el nivel de campo.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a probar con un subconjunto de campos de conjunto de datos. Puede recuperar una lista de acciones de marketing disponibles realizando una solicitud de [GET al extremo](./marketing-actions.md#list)de acciones de marketing. |

**Solicitud**

La siguiente solicitud prueba la acción de mercadotecnia `crossSiteTargeting` en un conjunto específico de campos que pertenecen a tres conjuntos de datos. La carga útil es similar a una solicitud de [evaluación que solo involucra conjuntos](#datasets)de datos, agregando campos específicos para cada conjunto de datos desde los que recopilar etiquetas.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Propiedad | Descripción |
| --- | --- |
| `entityType` | El tipo de entidad cuyo ID se indica en la `entityId` propiedad del mismo nivel. Actualmente, el único valor aceptado es `dataSet`. |
| `entityId` | ID de un conjunto de datos cuyos campos se van a evaluar en relación con la acción de marketing. Se puede obtener una lista de conjuntos de datos y sus ID correspondientes mediante una solicitud de GET al `/dataSets` extremo en la [!DNL Catalog Service] API. See the guide on [listing [!DNL Catalog] objects](../../catalog/api/list-objects.md) for more information. |
| `entityMeta.fields` | Matriz de rutas a campos específicos dentro del esquema del conjunto de datos, proporcionada en forma de cadenas de puntero JSON. Consulte la sección sobre el puntero [JSON](../../landing/api-fundamentals.md#json-pointer) en la guía de fundamentos de API para obtener detalles sobre la sintaxis aceptada para estas cadenas. |

**Respuesta**

Una respuesta correcta incluye una `violatedPolicies` matriz que contiene los detalles de las directivas que se infringieron como resultado de realizar la acción de mercadotecnia con los campos del conjunto de datos proporcionados. Si no se infringe ninguna directiva, la matriz `violatedPolicies` estará vacía.

Al comparar la respuesta de ejemplo siguiente con la [respuesta que solo involucra conjuntos](#datasets)de datos, tenga en cuenta que la lista de las etiquetas recopiladas es más corta. También se han reducido `discoveredLabels` los campos de cada conjunto de datos, ya que solo incluyen los campos especificados en el cuerpo de la solicitud. Además, la política anteriormente violada `Targeting Ads or Content` requiere que ambas `C4 AND C6` etiquetas estén presentes y, por lo tanto, ya no se viola como indica la matriz vacía `violatedPolicies` .

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Evaluar directivas de forma masiva {#bulk}

El punto final le permite ejecutar varios trabajos de evaluación en una sola llamada de API. `/bulk-eval`

**Formato API**

```http
POST /bulk-eval
```

**Solicitud**

La carga útil de una solicitud de evaluación masiva debe ser una matriz de objetos; uno para cada trabajo de evaluación que se va a realizar. Para los trabajos que se evalúan en función de conjuntos de datos y campos, se debe proporcionar una `entityList` matriz. Para los trabajos que se evalúan en función de etiquetas de uso de datos, se debe proporcionar una `labels` matriz.

>[!WARNING]
>
>Si algún trabajo de evaluación de la lista contiene una matriz `entityList` y una `labels` matriz, se producirá un error. Si desea evaluar la misma acción de mercadotecnia en base a conjuntos de datos y etiquetas, debe incluir trabajos de evaluación independientes para esa acción de mercadotecnia.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Propiedad | Descripción |
| --- | --- |
| `evalRef` | URI de la acción de marketing que se va a probar con etiquetas o conjuntos de datos para detectar infracciones de directivas. |
| `includeDraft` | De forma predeterminada, solo las directivas habilitadas participan en la evaluación. Si `includeDraft` se establece en `true`, también participarán las políticas que están en `DRAFT` estado. |
| `labels` | Matriz de etiquetas de uso de datos para probar la acción de mercadotecnia.<br><br>**IMPORTANTE**: Al utilizar esta propiedad, NO se debe incluir una `entityList` propiedad en el mismo objeto. Para evaluar la misma acción de marketing mediante conjuntos de datos o campos, debe incluir un objeto independiente en la carga útil de la solicitud que contenga una `entityList` matriz. |
| `entityList` | Matriz de conjuntos de datos y campos (opcionalmente) específicos dentro de esos conjuntos de datos para probar la acción de mercadotecnia.<br><br>**IMPORTANTE**: Al utilizar esta propiedad, NO se debe incluir una `labels` propiedad en el mismo objeto. Para evaluar la misma acción de marketing mediante etiquetas de uso de datos específicas, debe incluir un objeto independiente en la carga útil de la solicitud que contenga una `labels` matriz. |
| `entityType` | El tipo de entidad con el que se va a probar la acción de marketing. Actualmente, solo `dataSet` se admite. |
| `entityId` | ID de un conjunto de datos para probar la acción de marketing. |
| `entityMeta.fields` | (Opcional) Una lista de campos específicos dentro del conjunto de datos para probar la acción de mercadotecnia. |

**Respuesta**

Una respuesta satisfactoria devuelve una serie de resultados de evaluación; uno para cada trabajo de evaluación de directivas enviado en la solicitud.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{IMS_ORG}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Evaluación de políticas para [!DNL Real-time Customer Profile]

La [!DNL Policy Service] API también se puede utilizar para comprobar si hay infracciones de política que impliquen el uso de [!DNL Real-time Customer Profile] segmentos. Consulte el tutorial sobre la [aplicación de la conformidad con el uso de datos para ver los segmentos](../../segmentation/tutorials/governance.md) de audiencia para obtener más información.