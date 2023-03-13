---
keywords: Experience Platform;inicio;temas populares;aplicación de políticas;aplicación automática;aplicación basada en API;gobernanza de datos;prueba
solution: Experience Platform
title: Aplicar directivas de uso de datos mediante la API del servicio de directivas
type: Tutorial
description: Una vez que haya creado etiquetas de uso de datos para los datos y haya creado políticas de uso para acciones de marketing contra esas etiquetas, puede utilizar la API del servicio de políticas para evaluar si una acción de marketing realizada en un conjunto de datos o en un grupo arbitrario de etiquetas constituye una infracción de política. A continuación, puede configurar sus propios protocolos internos para gestionar las infracciones de directivas en función de la respuesta de la API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Aplicar políticas de uso de datos utilizando [!DNL Policy Service] API

Una vez que haya creado etiquetas de uso de datos para los datos y haya creado políticas de uso para acciones de marketing contra esas etiquetas, puede utilizar el complemento [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) para evaluar si una acción de marketing realizada en un conjunto de datos o en un grupo arbitrario de etiquetas constituye una infracción de política. A continuación, puede configurar sus propios protocolos internos para gestionar las infracciones de directivas en función de la respuesta de la API.

>[!NOTE]
>
>De forma predeterminada, solo las directivas cuyo estado está establecido en `ENABLED` puede participar en la evaluación. Para permitir `DRAFT` directivas para participar en la evaluación, debe incluir el parámetro de consulta `includeDraft=true` en la ruta de solicitud.

Este documento proporciona pasos sobre cómo utilizar la variable [!DNL Policy Service] API para comprobar violaciones de directivas en diferentes escenarios.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes conceptos clave implicados en la aplicación de las políticas de uso de datos:

* [Gobernanza de datos](../home.md): el marco mediante el cual [!DNL Platform] aplica el cumplimiento de uso de datos.
   * [Etiquetas de uso de datos](../labels/overview.md): las etiquetas de uso de datos se aplican a conjuntos de datos (o campos individuales dentro de esos conjuntos de datos), especificando restricciones sobre cómo se pueden utilizar esos datos.
   * [Políticas de uso de datos](../policies/overview.md): las políticas de uso de datos son reglas que describen los tipos de acciones de marketing permitidas o restringidas para determinados conjuntos de etiquetas de uso de datos.
* [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para poder realizar llamadas correctamente a [!DNL Policy Service] API, incluidos los encabezados obligatorios y cómo leer las llamadas de API de ejemplo.

## Evaluar mediante etiquetas y una acción de marketing

Puede evaluar una directiva probando una acción de marketing con un conjunto de etiquetas de uso de datos que hipotéticamente estarían presentes dentro de un conjunto de datos. Esto se realiza mediante el uso de la variable `duleLabels` parámetro de consulta, donde las etiquetas se proporcionan como una lista de valores separados por comas, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | El nombre de la acción de marketing asociada con la política de uso de datos que está evaluando. |
| `{LABEL_1}` | Una etiqueta de uso de datos para probar la acción de marketing. Se debe proporcionar al menos una etiqueta. Cuando se proporcionan varias etiquetas, deben separarse con comas. |

**Solicitud**

La siguiente solicitud prueba el `exportToThirdParty` acción de marketing contra etiquetas `C1` y `C3`. Dado que la política de uso de datos creada anteriormente en este tutorial define lo siguiente `C1` etiquete como uno de los `deny` condiciones en su expresión de directiva, la acción de marketing debe almacenar en déclencheur una infracción de directiva.

>[!NOTE]
>
>Las etiquetas de uso de datos distinguen entre mayúsculas y minúsculas. Las infracciones de directivas solo se producen cuando las etiquetas definidas en sus expresiones de directiva coinciden exactamente. En este ejemplo, una `C1` déclencheur una infracción, mientras que una `c1` La etiqueta no lo haría.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas de uso con las que se probó y una lista de las políticas que se violaron como resultado de la prueba de la acción contra esas etiquetas. En este ejemplo, la política &quot;Exportar datos a terceros&quot; se muestra en la `violatedPolicies` matriz, lo que indica que la acción de marketing activó la infracción de directiva esperada.

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
| `violatedPolicies` | Una matriz que enumera cualquier política que se haya violado al probar la acción de marketing (especificada en `marketingActionRef`) con el proporcionado `duleLabels`. |

## Evaluar mediante conjuntos de datos

Puede evaluar una política de uso de datos probando una acción de marketing con uno o más conjuntos de datos de los que se pueden recopilar etiquetas. Esto se realiza realizando una solicitud de POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` y proporcionan ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | El nombre de la acción de marketing asociada con la política que está evaluando. |

**Solicitud**

La siguiente solicitud prueba el `exportToThirdParty` acción de marketing contra tres conjuntos de datos diferentes. Se hace referencia a los conjuntos de datos por tipo e ID en una matriz proporcionada en la carga útil.

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
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se define. Para este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityId` | Cada elemento de la matriz de carga útil debe proporcionar el ID único para un conjunto de datos. |
| `entityMeta.fields` | (Opcional) Una matriz de [Puntero JSON](../../landing/api-fundamentals.md#json-pointer) cadenas, que hacen referencia a campos específicos del esquema del conjunto de datos. Si se incluye esta matriz, solo los campos contenidos en la matriz participan en la evaluación. Los campos de esquema que no se incluyan en la matriz no participarán en la evaluación.<br><br>Si no se incluye este campo, todos los campos del esquema del conjunto de datos se incluirán en la evaluación. |

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas de uso recopiladas de los conjuntos de datos proporcionados y una lista de las directivas que se violaron como resultado de probar la acción contra esas etiquetas. En este ejemplo, la política &quot;Exportar datos a terceros&quot; se muestra en la `violatedPolicies` matriz, lo que indica que la acción de marketing activó la infracción de directiva esperada.

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
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas de nivel de conjunto de datos y de nivel de campo que se encontraron en cada uno. |
| `violatedPolicies` | Una matriz que enumera cualquier política que se haya violado al probar la acción de marketing (especificada en `marketingActionRef`) con el proporcionado `duleLabels`. |

## Pasos siguientes

Al leer este documento, ha comprobado correctamente las infracciones de directivas al realizar una acción de marketing en un conjunto de datos o en un conjunto de etiquetas de uso de datos. Con los datos devueltos en las respuestas de API, puede configurar protocolos dentro de su aplicación de experiencia para aplicar correctamente infracciones de directivas cuando se producen.

Para obtener información sobre cómo Platform proporciona automáticamente la aplicación de directivas para los segmentos activados, consulte la guía sobre [aplicación automática](./auto-enforcement.md).
