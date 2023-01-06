---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;aplicación basada en API;control de datos;prueba
solution: Experience Platform
title: Aplicar políticas de uso de datos mediante la API del servicio de directivas
type: Tutorial
description: Una vez que haya creado etiquetas de uso de datos para sus datos y haya creado políticas de uso para acciones de marketing contra esas etiquetas, puede utilizar la API del servicio de políticas para evaluar si una acción de marketing realizada en un conjunto de datos o un grupo arbitrario de etiquetas constituye una infracción de política. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Aplique las políticas de uso de datos utilizando la variable [!DNL Policy Service] API

Una vez que haya creado etiquetas de uso de datos para sus datos y haya creado políticas de uso para acciones de marketing con esas etiquetas, puede usar la variable [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) para evaluar si una acción de marketing realizada en un conjunto de datos o un grupo arbitrario de etiquetas constituye una infracción de política. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de API.

>[!NOTE]
>
>De forma predeterminada, solo las directivas cuyo estado está establecido en `ENABLED` puede participar en la evaluación. Para permitir `DRAFT` directivas para participar en la evaluación, debe incluir el parámetro de consulta `includeDraft=true` en la ruta de solicitud.

Este documento proporciona los pasos sobre cómo utilizar la variable [!DNL Policy Service] API para comprobar las infracciones de directiva en diferentes escenarios.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes conceptos clave involucrados en la aplicación de políticas de uso de datos:

* [Administración de datos](../home.md): El marco por el cual [!DNL Platform] exige el cumplimiento de las normas de uso de datos.
   * [Etiquetas de uso de datos](../labels/overview.md): Las etiquetas de uso de datos se aplican a conjuntos de datos (y/o campos individuales dentro de esos conjuntos de datos), especificando restricciones para cómo se pueden usar esos datos.
   * [Políticas de uso de datos](../policies/overview.md): Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que están permitidas o restringidas para ciertos conjuntos de etiquetas de uso de datos.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, revise la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar correctamente llamadas a la función [!DNL Policy Service] API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Evaluar mediante etiquetas y una acción de marketing

Puede evaluar una política probando una acción de marketing con un conjunto de etiquetas de uso de datos que, hipotéticamente, estarían presentes en un conjunto de datos. Esto se hace mediante el uso de la variable `duleLabels` parámetro de consulta, donde las etiquetas se proporcionan como una lista de valores separados por coma, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada a la política de uso de datos que está evaluando. |
| `{LABEL_1}` | Una etiqueta de uso de datos para probar la acción de marketing. Se debe proporcionar al menos una etiqueta. Cuando se proporcionan varias etiquetas, deben separarse con comas. |

**Solicitud**

La siguiente solicitud prueba el `exportToThirdParty` acción de marketing contra etiquetas `C1` y `C3`. Dado que la política de uso de datos que ha creado anteriormente en este tutorial define la variable `C1` como una de las etiquetas `deny` condiciones en su expresión de directiva, la acción de marketing debe déclencheur una infracción de directiva.

>[!NOTE]
>
>Las etiquetas de uso de datos distinguen entre mayúsculas y minúsculas. Las infracciones de directiva solo se producen cuando las etiquetas definidas en sus expresiones de directiva coinciden exactamente. En este ejemplo, una `C1` una etiqueta sería un déclencheur de infracción, mientras que una `c1` no.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas de uso con las que se probó y una lista de las políticas que se infringieron como resultado de probar la acción con esas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la `violatedPolicies` , indicando que la acción de marketing activó la infracción de directiva esperada.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | Una matriz que enumera las directivas que se infringieron al probar la acción de marketing (especificada en `marketingActionRef`) en relación con el `duleLabels`. |

## Evaluar mediante conjuntos de datos

Puede evaluar una política de uso de datos probando una acción de marketing con respecto a uno o más conjuntos de datos desde los cuales se pueden recopilar etiquetas. Para ello, realice una solicitud de POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` y proporcionando ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada a la política que está evaluando. |

**Solicitud**

La siguiente solicitud prueba el `exportToThirdParty` acción de marketing con tres conjuntos de datos diferentes. Se hace referencia a los conjuntos de datos por tipo e ID en una matriz proporcionada en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se está definiendo. Para este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityId` | Cada elemento de la matriz de carga útil debe proporcionar el ID único para un conjunto de datos. |
| `entityMeta.fields` | (Opcional) Una matriz de [Puntero JSON](../../landing/api-fundamentals.md#json-pointer) , haciendo referencia a campos específicos en el esquema del conjunto de datos. Si se incluye esta matriz, solo los campos contenidos en la matriz participan en la evaluación. Los campos de esquema que no estén incluidos en la matriz no participarán en la evaluación.<br><br>Si este campo no se incluye, todos los campos dentro del esquema del conjunto de datos se incluyen en la evaluación. |

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas de uso recopiladas de los conjuntos de datos proporcionados y una lista de las políticas que se infringieron como resultado de probar la acción con esas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la `violatedPolicies` , indicando que la acción de marketing activó la infracción de directiva esperada.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
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
            "imsOrg": "{ORG_ID}",
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
| `duleLabels` | Una lista de etiquetas de uso de datos extraídas de los conjuntos de datos proporcionados en la carga útil de la solicitud. |
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas de nivel de conjunto de datos y de campo que se encontraron en cada uno. |
| `violatedPolicies` | Una matriz que enumera las directivas que se infringieron al probar la acción de marketing (especificada en `marketingActionRef`) en relación con el `duleLabels`. |

## Pasos siguientes

Al leer este documento, ha comprobado correctamente las infracciones de políticas al realizar una acción de marketing en un conjunto de datos o un conjunto de etiquetas de uso de datos. Con los datos devueltos en las respuestas de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente infracciones de directiva cuando ocurran.

Para obtener información sobre cómo Platform proporciona automáticamente la aplicación de directivas para segmentos activados, consulte la guía de [aplicación automática](./auto-enforcement.md).
