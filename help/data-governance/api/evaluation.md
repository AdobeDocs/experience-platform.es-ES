---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;aplicación basada en API;control de datos
solution: Experience Platform
title: Puntos finales de API de evaluación de políticas
topic-legacy: developer guide
description: Una vez creadas las acciones de marketing y definidas las políticas, puede utilizar la API del servicio de directivas para evaluar si determinadas acciones infringen alguna política. Las restricciones devueltas toman la forma de un conjunto de políticas que se violarían al intentar la acción de marketing en los datos especificados que contienen etiquetas de uso de datos.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# Puntos finales de la evaluación de políticas

Una vez creadas las acciones de marketing y definidas las políticas, puede utilizar la API [!DNL Policy Service] para evaluar si determinadas acciones infringen alguna política. Las restricciones devueltas toman la forma de un conjunto de políticas que se violarían al intentar la acción de marketing en los datos especificados que contienen etiquetas de uso de datos.

De forma predeterminada, solo participan en la evaluación las directivas cuyo estado está establecido en `ENABLED`. Sin embargo, puede utilizar el parámetro de consulta `?includeDraft=true` para incluir directivas `DRAFT` en la evaluación.

Las solicitudes de evaluación se pueden realizar de una de las tres maneras siguientes:

1. Dada una acción de marketing y un conjunto de etiquetas de uso de datos, ¿la acción infringe alguna política?
1. Dada una acción de marketing y uno o más conjuntos de datos, ¿la acción infringe alguna política?
1. Si se considera una acción de marketing, uno o más conjuntos de datos y un subconjunto de uno o más campos dentro de cada uno de esos conjuntos de datos, ¿la acción infringe alguna política?

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas correctamente a cualquier API [!DNL Experience Platform].

## Evaluar para infracciones de directiva usando etiquetas de uso de datos {#labels}

Puede evaluar infracciones de directivas en función de la presencia de un conjunto específico de etiquetas de uso de datos mediante el uso del parámetro de consulta `duleLabels` en una solicitud de GET.

**Formato de API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a probar con un conjunto de etiquetas de uso de datos. Puede recuperar una lista de las acciones de marketing disponibles realizando una solicitud de [GET al extremo](./marketing-actions.md#list) de las acciones de marketing. |
| `{LABELS_LIST}` | Lista de nombres de etiquetas de uso de datos separados por coma para probar la acción de marketing. Por ejemplo: `duleLabels=C1,C2,C3`<br><br>Tenga en cuenta que los nombres de las etiquetas distinguen entre mayúsculas y minúsculas. Asegúrese de que está utilizando las mayúsculas y minúsculas correctas al enumerarlas en el parámetro `duleLabels`. |

**Solicitud**

La solicitud de ejemplo siguiente evalúa una acción de marketing en relación con las etiquetas C1 y C3.

>[!IMPORTANT]
>
>Tenga en cuenta los operadores `AND` y `OR` en las expresiones de directiva. En el ejemplo siguiente, si alguna de las etiquetas (`C1` o `C3`) hubiera aparecido sola en la solicitud, la acción de marketing no habría infringido esta directiva. Se necesitan ambas etiquetas (`C1` y `C3`) para devolver la directiva violada. Asegúrese de que está evaluando las políticas cuidadosamente y definiendo las expresiones de políticas con el mismo cuidado.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta incluye una matriz `violatedPolicies`, que contiene los detalles de las políticas que se infringieron como resultado de realizar la acción de marketing con las etiquetas proporcionadas. Si no se infringe ninguna directiva, la matriz `violatedPolicies` estará vacía.

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

## Evaluar para infracciones de directiva usando conjuntos de datos {#datasets}

Puede evaluar las infracciones de políticas en función de un conjunto de uno o más conjuntos de datos desde los que se pueden recopilar las etiquetas de uso de datos. Esto se realiza realizando una solicitud de POST al extremo `/constraints` para una acción de marketing específica y proporcionando una lista de ID de conjuntos de datos dentro del cuerpo de la solicitud.

**Formato de API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a probar con uno o más conjuntos de datos. Puede recuperar una lista de las acciones de marketing disponibles realizando una solicitud de [GET al extremo](./marketing-actions.md#list) de las acciones de marketing. |

**Solicitud**

La siguiente solicitud realiza la acción de marketing `crossSiteTargeting` frente a un conjunto de tres conjuntos de datos para evaluar si hay alguna infracción de directiva.

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
| `entityType` | Tipo de entidad cuyo ID se indica en la propiedad `entityId` del mismo nivel. Actualmente, el único valor aceptado es `dataSet`. |
| `entityId` | El ID de un conjunto de datos con el que probar la acción de marketing. Se puede obtener una lista de conjuntos de datos y sus ID correspondientes realizando una solicitud de GET al extremo `/dataSets` en la API [!DNL Catalog Service]. Consulte la guía sobre [listado [!DNL Catalog] objetos](../../catalog/api/list-objects.md) para obtener más información. |

**Respuesta**

Una respuesta correcta incluye una matriz `violatedPolicies`, que contiene los detalles de las políticas que se infringieron como resultado de realizar la acción de marketing con los conjuntos de datos proporcionados. Si no se infringe ninguna directiva, la matriz `violatedPolicies` estará vacía.

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
| `duleLabels` | El objeto response incluye una matriz `duleLabels` que contiene una lista consolidada de todas las etiquetas encontradas dentro de los conjuntos de datos especificados. Esta lista incluye etiquetas de nivel de conjunto de datos y campo en todos los campos dentro del conjunto de datos. |
| `discoveredLabels` | La respuesta también incluye una matriz `discoveredLabels` que contiene objetos para cada conjunto de datos, que muestra `datasetLabels` desglosada en etiquetas de nivel de conjunto de datos y campo. Cada etiqueta de nivel de campo muestra la ruta al campo específico con esa etiqueta. |

## Evaluar para infracciones de directiva usando campos específicos del conjunto de datos {#fields}

Puede evaluar infracciones de directiva basadas en un subconjunto de campos desde uno o varios conjuntos de datos, de modo que solo se evalúen las etiquetas de uso de datos aplicadas a esos campos.

Al evaluar políticas mediante campos de conjuntos de datos, tenga en cuenta lo siguiente:

* **Los nombres de campo distinguen entre mayúsculas y minúsculas**: Al proporcionar campos, deben escribirse exactamente como aparecen en el conjunto de datos (por ejemplo,  `firstName` frente a  `firstname`).
* **Herencia** de etiquetas de conjunto de datos: Los campos individuales de un conjunto de datos heredan cualquier etiqueta que se haya aplicado en el nivel del conjunto de datos. Si las evaluaciones de políticas no regresan según lo esperado, asegúrese de comprobar si hay etiquetas que puedan haberse heredado del nivel de conjunto de datos hasta los campos, además de las aplicadas en el nivel de campo.

**Formato de API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a probar con un subconjunto de campos de conjuntos de datos. Puede recuperar una lista de las acciones de marketing disponibles realizando una solicitud de [GET al extremo](./marketing-actions.md#list) de las acciones de marketing. |

**Solicitud**

La siguiente solicitud prueba la acción de marketing `crossSiteTargeting` en un conjunto específico de campos que pertenecen a tres conjuntos de datos. La carga útil es similar a una [solicitud de evaluación que involucra solo conjuntos de datos](#datasets), agregando campos específicos para cada conjunto de datos desde el que recopilar etiquetas.

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
| `entityType` | Tipo de entidad cuyo ID se indica en la propiedad `entityId` del mismo nivel. Actualmente, el único valor aceptado es `dataSet`. |
| `entityId` | ID de un conjunto de datos cuyos campos se van a evaluar con la acción de marketing. Se puede obtener una lista de conjuntos de datos y sus ID correspondientes realizando una solicitud de GET al extremo `/dataSets` en la API [!DNL Catalog Service]. Consulte la guía sobre [listado [!DNL Catalog] objetos](../../catalog/api/list-objects.md) para obtener más información. |
| `entityMeta.fields` | Matriz de rutas a campos específicos dentro del esquema del conjunto de datos, proporcionada en forma de cadenas de puntero JSON. Consulte la sección sobre [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) en la guía de fundamentos de API para obtener más información sobre la sintaxis aceptada para estas cadenas. |

**Respuesta**

Una respuesta correcta incluye una matriz `violatedPolicies`, que contiene los detalles de las políticas que se infringieron como resultado de realizar la acción de marketing en los campos del conjunto de datos proporcionados. Si no se infringe ninguna directiva, la matriz `violatedPolicies` estará vacía.

Al comparar la respuesta de ejemplo siguiente con la respuesta [que solo incluye conjuntos de datos](#datasets), tenga en cuenta que la lista de etiquetas recopiladas es más corta. También se ha reducido el `discoveredLabels` de cada conjunto de datos, ya que solo incluyen los campos especificados en el cuerpo de la solicitud. Además, la directiva `Targeting Ads or Content` previamente violada requiere que estén presentes ambas etiquetas `C4 AND C6` y, por lo tanto, ya no se viola como indica la matriz `violatedPolicies` vacía.

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

El extremo `/bulk-eval` le permite ejecutar varios trabajos de evaluación en una sola llamada de API.

**Formato de API**

```http
POST /bulk-eval
```

**Solicitud**

La carga útil de una solicitud de evaluación masiva debe ser una matriz de objetos; uno para cada trabajo de evaluación que se va a realizar. Para los trabajos que se evalúan en función de conjuntos de datos y campos, se debe proporcionar una matriz `entityList` . Para los trabajos que se evalúan en función de etiquetas de uso de datos, se debe proporcionar una matriz `labels`.

>[!WARNING]
>
>Si algún trabajo de evaluación enumerado contiene una matriz `entityList` y una matriz `labels`, se producirá un error. Si desea evaluar la misma acción de marketing basada en conjuntos de datos y etiquetas, debe incluir trabajos de evaluación independientes para esa acción de marketing.

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
| `evalRef` | El URI de la acción de marketing que se va a probar con etiquetas o conjuntos de datos para detectar infracciones de directivas. |
| `includeDraft` | De forma predeterminada, solo participan en la evaluación las directivas habilitadas. Si `includeDraft` se configura como `true`, también participarán las políticas que estén en estado `DRAFT`. |
| `labels` | Matriz de etiquetas de uso de datos con las que probar la acción de marketing.<br><br>**IMPORTANTE**: Al utilizar esta propiedad, NO se debe incluir una  `entityList` propiedad en el mismo objeto. Para evaluar la misma acción de marketing mediante conjuntos de datos o campos, debe incluir un objeto independiente en la carga útil de la solicitud que contenga una matriz `entityList`. |
| `entityList` | Una matriz de conjuntos de datos y campos (opcionalmente) específicos dentro de esos conjuntos de datos para probar la acción de marketing.<br><br>**IMPORTANTE**: Al utilizar esta propiedad, NO se debe incluir una  `labels` propiedad en el mismo objeto. Para evaluar la misma acción de marketing mediante etiquetas de uso de datos específicas, debe incluir un objeto independiente en la carga útil de la solicitud que contenga una matriz `labels`. |
| `entityType` | Tipo de entidad con la que probar la acción de marketing. Actualmente, solo se admite `dataSet`. |
| `entityId` | El ID de un conjunto de datos con el que probar la acción de marketing. |
| `entityMeta.fields` | (Opcional) Una lista de campos específicos dentro del conjunto de datos para probar la acción de marketing. |

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

La API [!DNL Policy Service] también se puede utilizar para comprobar si hay infracciones de directiva que impliquen el uso de segmentos [!DNL Real-time Customer Profile]. Consulte el tutorial sobre la [aplicación del cumplimiento de uso de datos para los segmentos de audiencia](../../segmentation/tutorials/governance.md) para obtener más información.
