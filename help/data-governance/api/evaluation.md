---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# Evaluación de políticas

Una vez creadas las acciones de marketing y definidas las políticas, puede utilizar la API de servicio de directivas para evaluar si determinadas acciones infringen alguna política. Las restricciones devueltas toman la forma de un conjunto de directivas que se violarían al intentar la acción de marketing en los datos especificados que contienen etiquetas de uso de datos.

De forma predeterminada, **solo participan en la evaluación** las directivas cuyo estado está establecido en &quot;HABILITADO&quot;; sin embargo, puede utilizar el parámetro de consulta `?includeDraft=true` para incluir las directivas &quot;BORRADOR&quot; en la evaluación.

Las solicitudes de evaluación se pueden realizar de una de las tres maneras siguientes:

1. Dado un conjunto de etiquetas de uso de datos y una acción de marketing, ¿la acción infringe alguna política?
1. Dado uno o más conjuntos de datos y una acción de marketing, ¿la acción infringe alguna política?
1. Dado uno o más conjuntos de datos y un subconjunto de uno o más campos dentro de cada uno de esos conjuntos de datos, ¿la acción infringe alguna política?

## Evaluar las directivas mediante etiquetas de uso de datos y una acción de marketing

La evaluación de las infracciones de directiva en función de la presencia de etiquetas de uso de datos requiere que especifique el conjunto de etiquetas que estarán presentes en los datos durante la solicitud. Esto se realiza mediante el uso de parámetros de consulta, donde las etiquetas de uso de datos se proporcionan como una lista de valores separados por comas, como se muestra en el siguiente ejemplo.

**Formato API**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Solicitud**

La solicitud de ejemplo siguiente evalúa una acción de mercadotecnia con las etiquetas C1 y C3. Al evaluar las políticas mediante etiquetas de uso de datos, tenga en cuenta lo siguiente:
* **Las etiquetas de uso de datos distinguen entre mayúsculas y minúsculas.** La solicitud que se muestra arriba devuelve una directiva violada, mientras que la realización de la misma solicitud con etiquetas en minúsculas (por ejemplo: `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) no.
* **Tenga en cuenta los`AND`operadores y`OR`en sus expresiones de directiva.** En este ejemplo, si alguna de las etiquetas (`C1` o `C3`) hubiera aparecido sola en la solicitud, la acción de marketing no habría violado esta política. Se necesitan ambas etiquetas (`C1 AND C3`) para devolver la directiva violada. Asegúrese de que está evaluando las políticas cuidadosamente y definiendo las expresiones de políticas con el mismo cuidado.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response incluye una `duleLabels` matriz que debe coincidir con las etiquetas enviadas en la solicitud. Si la realización de la acción de marketing especificada contra las etiquetas de uso de datos infringe una directiva, la matriz contendrá los detalles de la directiva (o las políticas) afectada. `violatedPolicies` Si no se infringe ninguna directiva, la matriz `violatedPolicies` aparecerá vacía (`[]`).

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

## Evaluar las directivas mediante conjuntos de datos y una acción de mercadotecnia

También puede evaluar las infracciones de directivas especificando el ID de uno o varios conjuntos de datos desde los que se pueden recopilar las etiquetas de uso de datos. Esto se lleva a cabo realizando una solicitud POST al extremo principal o personalizado `/constraints` de una acción de marketing y especificando los ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra a continuación.

**Formato API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Solicitud**

El cuerpo de la solicitud contiene una matriz con un objeto para cada ID de conjunto de datos. Dado que está enviando un cuerpo de solicitud, la variable &quot;Content-Type: se requiere el encabezado de solicitud &quot;application/json&quot;, como se muestra en el siguiente ejemplo.

```SHELL
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

**Respuesta**

El objeto response incluye una `duleLabels` matriz que contiene una lista consolidada de todas las etiquetas que se encuentran dentro de los conjuntos de datos especificados. Esta lista incluye rótulos a nivel de conjunto de datos y campo en todos los campos dentro del conjunto de datos.

La respuesta también incluye una `discoveredLabels` matriz que contiene objetos para cada conjunto de datos, y que `datasetLabels` se desglosan en rótulos de nivel de conjunto de datos y campo. Cada etiqueta de nivel de campo muestra la ruta al campo específico con esa etiqueta.

Si la acción de mercadotecnia especificada infringe una directiva que involucra a los `duleLabels` conjuntos de datos, la `violatedPolicies` matriz contendrá los detalles de la directiva (o políticas) afectada. Si no se infringe ninguna directiva, la matriz `violatedPolicies` aparecerá vacía (`[]`).

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

## Evaluar directivas mediante conjuntos de datos, campos y una acción de marketing

Además de proporcionar uno o más ID de conjuntos de datos, también se puede especificar un subconjunto de campos dentro de cada conjunto de datos, lo que indica que sólo se deben evaluar las etiquetas de uso de datos de esos campos. De forma similar a la solicitud POST que solo incluye conjuntos de datos, esta solicitud agrega campos específicos para cada conjunto de datos al cuerpo de la solicitud.

Cuando evalúe políticas mediante campos de conjunto de datos, tenga en cuenta lo siguiente:

* **Los nombres de los campos distinguen entre mayúsculas y minúsculas.** Al proporcionar campos, deben escribirse exactamente como aparecen en el conjunto de datos (por ejemplo, `firstName` vs `firstname`).
* **Herencia de etiquetas de conjunto de datos.** las etiquetas de uso de datos se pueden aplicar en varios niveles y se heredan hacia abajo. Si las evaluaciones de directivas no devuelven el modo que pensaba, asegúrese de comprobar las etiquetas heredadas de los conjuntos de datos a los campos además de los aplicados en el nivel de campo.

**Formato API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Solicitud**

El cuerpo de la solicitud contiene una matriz con un objeto para cada ID de conjunto de datos y el subconjunto de campos dentro de ese conjunto de datos que debe utilizarse para la evaluación. Dado que está enviando un cuerpo de solicitud, la variable &quot;Content-Type: se requiere el encabezado de solicitud &quot;application/json&quot;, como se muestra en el siguiente ejemplo.

```SHELL
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

**Respuesta**

El objeto response incluye una `duleLabels` matriz que contiene la lista consolidada de las etiquetas que se encuentran en los campos especificados. Recuerde que esto también incluye etiquetas de conjunto de datos, ya que se heredan en los campos.

Si se infringe una directiva al realizar la acción de marketing especificada en los datos de los campos proporcionados, la matriz contendrá los detalles de la directiva (o políticas) afectada. `violatedPolicies` Si no se infringe ninguna directiva, la matriz `violatedPolicies` aparecerá vacía (`[]`).

En la respuesta siguiente, se puede ver que la lista de `duleLabels` ahora es más corta, al igual que `discoveredLabels` para cada conjunto de datos, ya que solo incluye los campos especificados en el cuerpo de la solicitud. También observará que la directiva anteriormente violada, &quot;Publicidades de objetivo o contenido&quot;, requería ambas `C4 AND C6` `violatedPolicies` etiquetas, por lo que ya no se viola y la matriz parece vacía.

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

## Evaluación de políticas para [!DNL Real-time Customer Profile]

La [!DNL Policy Service] API también se puede utilizar para comprobar si hay infracciones de política que impliquen el uso de [!DNL Real-time Customer Profile] segmentos. Consulte el tutorial sobre la [aplicación de la conformidad con el uso de datos para ver los segmentos](../../segmentation/tutorials/governance.md) de audiencia para obtener más información.