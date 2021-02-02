---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;Aplicación basada en API;control de datos;pruebas
solution: Experience Platform
title: Aplicar directivas de uso de datos mediante la API de servicio de directivas
topic: guide
type: Tutorial
description: Una vez que haya creado etiquetas de uso de datos para los datos y haya creado políticas de uso para acciones de mercadotecnia con dichas etiquetas, puede utilizar la API de servicio de directivas para evaluar si una acción de mercadotecnia realizada en un conjunto de datos o en un grupo arbitrario de etiquetas constituye una infracción de política. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de la API.
translation-type: tm+mt
source-git-commit: acc4fa59a4808ed9a32c2aaf664039e0d12dc1d8
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 1%

---


# Aplicar políticas de uso de datos mediante la API [!DNL Policy Service]

Una vez que haya creado etiquetas de uso de datos para sus datos y haya creado políticas de uso para acciones de mercadotecnia con esas etiquetas, puede utilizar [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) para evaluar si una acción de mercadotecnia realizada en un conjunto de datos o en un grupo arbitrario de etiquetas constituye una infracción de política. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de la API.

>[!NOTE]
>
>De forma predeterminada, solo pueden participar en la evaluación las directivas cuyo estado esté establecido en `ENABLED`. Para permitir que `DRAFT` políticas participen en la evaluación, debe incluir el parámetro de consulta `includeDraft=true` en la ruta de la solicitud.

Este documento proporciona pasos sobre cómo utilizar la API [!DNL Policy Service] para verificar las infracciones de políticas en diferentes escenarios.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes conceptos clave relacionados con la aplicación de las políticas de uso de datos:

* [Administración](../home.md) de datos: Marco mediante el cual se  [!DNL Platform] aplica el cumplimiento de la normativa de uso de datos.
   * [Etiquetas](../labels/overview.md) de uso de datos: Las etiquetas de uso de datos se aplican a conjuntos de datos (y/o a campos individuales dentro de esos conjuntos de datos), especificando restricciones para el uso de los datos.
   * [Directivas](../policies/overview.md) de uso de datos: Las políticas de uso de datos son reglas que describen los tipos de acciones de mercadotecnia que están permitidas o restringidas para determinados conjuntos de etiquetas de uso de datos.
* [Simuladores](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que debe conocer a fin de realizar llamadas exitosas a la API [!DNL Policy Service], incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Evaluar mediante etiquetas y una acción de marketing

Puede evaluar una política probando una acción de marketing en comparación con un conjunto de etiquetas de uso de datos que podrían estar presentes en un conjunto de datos. Esto se realiza mediante el uso del parámetro de consulta `duleLabels`, donde las etiquetas se proporcionan como una lista de valores separados por coma, como se muestra en el ejemplo siguiente.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada con la directiva de uso de datos que está evaluando. |
| `{LABEL_1}` | Etiqueta de uso de datos para probar la acción de marketing. Se debe proporcionar al menos una etiqueta. Cuando se proporcionan varias etiquetas, deben separarse con comas. |

**Solicitud**

La siguiente solicitud prueba la acción de mercadotecnia `exportToThirdParty` con las etiquetas `C1` y `C3`. Dado que la directiva de uso de datos que creó anteriormente en este tutorial define la etiqueta `C1` como una de las condiciones `deny` de su expresión de directiva, la acción de mercadotecnia debe déclencheur una infracción de directiva.

>[!NOTE]
>
>Las etiquetas de uso de datos distinguen entre mayúsculas y minúsculas. Las infracciones de directiva solo se producen cuando las etiquetas definidas en sus expresiones de directiva coinciden exactamente. En este ejemplo, una etiqueta `C1` déclencheur una infracción, mientras que una etiqueta `c1` no.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas de uso con las que se probó y una lista de las directivas que se infringieron como resultado de probar la acción con dichas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz `violatedPolicies`, lo que indica que la acción de mercadotecnia desencadenó la infracción de directiva esperada.

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
| `violatedPolicies` | Una matriz que enumera las directivas que se infringieron al probar la acción de mercadotecnia (especificada en `marketingActionRef`) en comparación con la `duleLabels` proporcionada. |

## Evaluar mediante conjuntos de datos

Puede evaluar una directiva de uso de datos probando una acción de mercadotecnia con uno o más conjuntos de datos desde los que se pueden recopilar etiquetas. Esto se realiza haciendo una solicitud de POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` y proporcionando ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada a la directiva que está evaluando. |

**Solicitud**

La siguiente solicitud prueba la acción de mercadotecnia `exportToThirdParty` con tres conjuntos de datos diferentes. Se hace referencia a los conjuntos de datos por tipo e ID en una matriz proporcionada en la carga útil.

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
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se está definiendo. En este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityId` | Cada elemento de la matriz de carga útil debe proporcionar la ID única para un conjunto de datos. |
| `entityMeta.fields` | (Opcional) Una matriz de cadenas [Puntero JSON](../../landing/api-fundamentals.md#json-pointer), que hace referencia a campos específicos en el esquema del conjunto de datos. Si se incluye esta matriz, solo participarán en la evaluación los campos contenidos en ella. Los campos de esquema que no estén incluidos en la matriz no participarán en la evaluación.<br><br>Si no se incluye este campo, todos los campos dentro del esquema del conjunto de datos se incluirán en la evaluación. |

**Respuesta**

Una respuesta correcta devuelve la dirección URL de la acción de marketing, las etiquetas de uso recopiladas de los conjuntos de datos proporcionados y una lista de las directivas que se infringieron como resultado de probar la acción con dichas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz `violatedPolicies`, lo que indica que la acción de mercadotecnia desencadenó la infracción de directiva esperada.

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
| `duleLabels` | Una lista de las etiquetas de uso de datos que se extrajeron de los conjuntos de datos proporcionados en la carga útil de la solicitud. |
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas de nivel de conjunto de datos y de campo que se encontraron en cada una. |
| `violatedPolicies` | Una matriz que enumera las directivas que se infringieron al probar la acción de mercadotecnia (especificada en `marketingActionRef`) en comparación con la `duleLabels` proporcionada. |

## Pasos siguientes

Al leer este documento, comprobó correctamente si hay infracciones de directivas al realizar una acción de marketing en un conjunto de datos o en un conjunto de etiquetas de uso de datos. Con los datos devueltos en las respuestas de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente las infracciones de directiva cuando se produzcan.

Para obtener información sobre cómo Platform proporciona automáticamente la aplicación de políticas para segmentos activados, consulte la guía sobre [aplicación automática](./auto-enforcement.md).