---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aplicar directivas de uso de datos mediante la API de servicio de directivas
topic: enforcement
translation-type: tm+mt
source-git-commit: 3e5245a718295cc5318c277a5cf9ee71da2a911b

---


# Aplicar directivas de uso de datos mediante la API de servicio de directivas

Una vez que haya creado etiquetas de uso de datos para los datos y haya creado políticas de uso para acciones de mercadotecnia con esas etiquetas, puede utilizar la API [de servicio de directivas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE para evaluar si una acción de mercadotecnia realizada en un conjunto de datos o un grupo arbitrario de etiquetas constituye una infracción de la política. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de la API.

>[!NOTE] De forma predeterminada, solo pueden participar en la evaluación las directivas cuyo estado está configurado para `ENABLED` participar. Para permitir que `DRAFT` las directivas participen en la evaluación, debe incluir el parámetro de consulta `includeDraft=true` en la ruta de la solicitud.

Este documento proporciona pasos sobre cómo utilizar la API de servicio de directivas para comprobar si hay infracciones de políticas en diferentes escenarios.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes conceptos clave involucrados en la aplicación de las políticas DULE:

* [Administración](../home.md)de datos: El marco por el cual la Plataforma impone el cumplimiento del uso de datos.
   * [Etiquetas](../labels/overview.md)de uso de datos: Las etiquetas de uso de datos se aplican a conjuntos de datos (y/o a campos individuales dentro de esos conjuntos de datos), especificando restricciones para el uso de los datos.
   * [Directivas](../policies/overview.md)de uso de datos: Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que están permitidas o restringidas para determinados conjuntos de etiquetas DULE.
* [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la guía [para](../api/getting-started.md) desarrolladores para obtener información importante que necesita conocer a fin de realizar llamadas exitosas a la API del servicio de directivas DULE, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Evaluar mediante etiquetas DULE y una acción de mercadotecnia

Puede evaluar una política probando una acción de mercadotecnia con un conjunto de etiquetas DULE que podrían estar presentes en un conjunto de datos. Esto se realiza mediante el uso del parámetro de `duleLabels` consulta, donde las etiquetas DULE se proporcionan como una lista de valores separados por comas, como se muestra en el ejemplo siguiente.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada con la directiva DULE que está evaluando. |
| `{LABEL_1}` | Etiqueta de uso de datos para probar la acción de marketing. Se debe proporcionar al menos una etiqueta. Cuando se proporcionan varias etiquetas, deben separarse con comas. |

**Solicitud**

La siguiente solicitud prueba la acción de mercadotecnia con las etiquetas `exportToThirdParty` y `C1` `C3`. Dado que la directiva de uso de datos que creó anteriormente en este tutorial define la `C1` etiqueta como una de las `deny` condiciones de su expresión de directiva, la acción de marketing debe desencadenar una infracción de directiva.

>[!NOTE] Las etiquetas de uso de datos distinguen entre mayúsculas y minúsculas. Las infracciones de directiva solo se producen cuando las etiquetas definidas en sus expresiones de directiva coinciden exactamente. En este ejemplo, una `C1` etiqueta activaría una infracción, mientras que una `c1` etiqueta no.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas DULE con las que se probó y una lista de cualquier directiva DULE que se infringiera como resultado de probar la acción con dichas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz, lo que indica que la acción de marketing desencadenó la infracción de directiva esperada. `violatedPolicies`

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `violatedPolicies` | Una matriz que enumera las directivas DULE que se infringieron al probar la acción de mercadotecnia (especificada en `marketingActionRef`) en comparación con la proporcionada `duleLabels`. |

## Evaluar mediante conjuntos de datos

Puede evaluar una directiva DULE probando una acción de mercadotecnia con uno o más conjuntos de datos desde los que se pueden recopilar etiquetas DULE. Esto se realiza realizando una solicitud POST `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` y proporcionando ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada con la directiva DULE que está evaluando. |

**Solicitud**

La siguiente solicitud prueba la acción de mercadotecnia con tres conjuntos de datos diferentes. `exportToThirdParty` Se hace referencia a los conjuntos de datos por tipo e ID en una matriz proporcionada en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se está definiendo. En este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityId` | Cada elemento de la matriz de carga útil debe proporcionar la ID única para un conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas DULE recopiladas de los conjuntos de datos proporcionados y una lista de cualquier directiva DULE que se haya infringido como resultado de probar la acción con dichas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz, lo que indica que la acción de marketing desencadenó la infracción de directiva esperada. `violatedPolicies`

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `duleLabels` | Una lista de las etiquetas DULE que se han extraído de los conjuntos de datos proporcionados en la carga útil de la solicitud. |
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas DULE de nivel de conjunto de datos y de nivel de campo que se encontraron en cada una. |
| `violatedPolicies` | Una matriz que enumera las directivas DULE que se infringieron al probar la acción de mercadotecnia (especificada en `marketingActionRef`) en comparación con la proporcionada `duleLabels`. |

## Pasos siguientes

Al leer este documento, comprobó correctamente si hay infracciones de directivas al realizar una acción de marketing en un conjunto de datos o en un conjunto de etiquetas DULE. Con los datos devueltos en las respuestas de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente las infracciones de directiva cuando se produzcan.

Para ver los pasos sobre cómo aplicar políticas de uso de datos para segmentos de audiencia en Perfil de clientes en tiempo real, consulte el siguiente [tutorial](../../segmentation/tutorials/governance.md).