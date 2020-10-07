---
keywords: Experience Platform;home;popular topics;Policy enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Políticas
topic: developer guide
description: Las políticas de uso de datos son reglas que su organización adopta que describen los tipos de acciones de marketing que puede realizar o que tiene restringido el acceso a los datos dentro de Experience Platform. El extremo /policy se utiliza para todas las llamadas de API relacionadas con la visualización, creación, actualización o eliminación de directivas de uso de datos.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 2%

---


# Extremo de directivas

Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se restringe el rendimiento de los datos dentro de [!DNL Experience Platform]. El `/policies` punto final de la [!DNL Policy Service API] le permite administrar mediante programación las directivas de uso de datos de su organización.

## Primeros pasos

El punto final de API utilizado en esta guía forma parte de la [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Recuperar una lista de directivas {#list}

Puede realizar la lista de todas `core` o `custom` las directivas mediante una solicitud de GET a `/policies/core` o `/policies/custom`, respectivamente.

**Formato API**

```http
GET /policies/core
GET /policies/custom
```

**Solicitud**

La siguiente solicitud recupera una lista de directivas personalizadas definidas por su organización.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta incluye una `children` matriz que lista los detalles de cada directiva recuperada, incluidos sus `id` valores. Puede utilizar el `id` campo de una política en particular para realizar [búsquedas](#lookup), [actualizaciones](#update)y [eliminaciones](#delete) de solicitudes para dicha directiva.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| Propiedad | Descripción |
| --- | --- |
| `_page.count` | Número total de directivas recuperadas. |
| `name` | Nombre para mostrar de una directiva. |
| `status` | Estado actual de una política. Existen tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las directivas participan en la evaluación. Consulte la información general sobre la evaluación [de](../enforcement/overview.md) políticas para obtener más información. |
| `marketingActionRefs` | Matriz que lista los URI de todas las acciones de marketing aplicables para una política. |
| `description` | Descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | Objeto que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a una política no se puede realizar. Consulte la sección sobre la [creación de una política](#create-policy) para obtener más información sobre esta propiedad. |

## Buscar una directiva {#look-up}

Puede buscar una directiva específica incluyendo la propiedad de esa `id` directiva en la ruta de una solicitud de GET.

**Formato API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` de la política que desea buscar. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre para mostrar de la directiva. |
| `status` | El estado actual de la política. Existen tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las directivas participan en la evaluación. Consulte la información general sobre la evaluación [de](../enforcement/overview.md) políticas para obtener más información. |
| `marketingActionRefs` | Una matriz que lista los URI de todas las acciones de marketing aplicables para la política. |
| `description` | Descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | Un objeto que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la política no se puede realizar. Consulte la sección sobre la [creación de una política](#create-policy) para obtener más información sobre esta propiedad. |

## Create a custom policy {#create-policy}

En la [!DNL Policy Service] API, una directiva se define de la siguiente manera:

* Referencia a una acción de mercadotecnia específica
* Una expresión que describe las etiquetas de uso de datos con las que la acción de mercadotecnia no se puede realizar

Para satisfacer este último requisito, las definiciones de políticas deben incluir una expresión booleana con respecto a la presencia de etiquetas de uso de datos. Esta expresión se denomina expresión de políticas.

Las expresiones de directiva se proporcionan en forma de `deny` propiedad dentro de cada definición de directiva. Un ejemplo de un `deny` objeto simple que solo comprueba la presencia de una única etiqueta tendría el siguiente aspecto:

```json
"deny": {
    "label": "C1"
}
```

Sin embargo, muchas políticas especifican condiciones más complejas con respecto a la presencia de etiquetas de uso de datos. Para admitir estos casos de uso, también puede incluir operaciones booleanas para describir sus expresiones de directiva. El objeto de expresión de directiva debe contener una etiqueta o un operador y operandos, pero no ambos. A su vez, cada operando es también un objeto de expresión de políticas.

Por ejemplo, para definir una directiva que prohíba que una acción de marketing se realice en los datos en los que hay `C1 OR (C3 AND C7)` `deny` etiquetas presentes, la propiedad de la política se especificaría de la siguiente manera:

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `operator` | Indica la relación condicional entre las etiquetas proporcionadas en la `operands` matriz del mismo nivel. Los valores aceptados son: <ul><li>`OR`:: La expresión se resuelve en true si hay alguna de las etiquetas de la `operands` matriz.</li><li>`AND`:: La expresión solo se resuelve en true si están presentes todas las etiquetas de la `operands` matriz.</li></ul> |
| `operands` | Matriz de objetos, en la que cada objeto representa una única etiqueta o un par de propiedades `operator` y `operands` adicional. La presencia de etiquetas y/o operaciones en una `operands` matriz se resuelve en true o false según el valor de su `operator` propiedad del mismo nivel. |
| `label` | Nombre de una única etiqueta de uso de datos que se aplica a la directiva. |

Puede crear una nueva directiva personalizada realizando una solicitud de POST al `/policies/custom` extremo.

**Formato API**

```http
POST /policies/custom
```

**Solicitud**

La siguiente solicitud crea una nueva directiva que restringe que la acción `exportToThirdParty` de marketing se realice en los datos que contienen etiquetas `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre para mostrar de la directiva. |
| `status` | El estado actual de la política. Existen tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las directivas participan en la evaluación. Consulte la información general sobre la evaluación [de](../enforcement/overview.md) políticas para obtener más información. |
| `marketingActionRefs` | Una matriz que lista los URI de todas las acciones de marketing aplicables para la política. El URI de una acción de marketing se proporciona en `_links.self.href` la respuesta para [buscar una acción](./marketing-actions.md#look-up)de marketing. |
| `description` | Descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | La expresión de directiva que describe las etiquetas de uso de datos específicas en las que se restringe la acción de marketing asociada a la política para que no se realice. |

**Respuesta**

Una respuesta exitosa devuelve los detalles de la política recién creada, incluyendo su `id`. Este valor es de sólo lectura y se asigna automáticamente cuando se crea la directiva.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Actualizar una directiva personalizada {#update}

>[!IMPORTANT]
>
>Solo puede actualizar directivas personalizadas. Si desea habilitar o deshabilitar las directivas principales, consulte la sección sobre [actualización de la lista de las directivas](#update-enabled-core)principales habilitadas.

Puede actualizar una directiva personalizada existente proporcionando su ID en la ruta de una solicitud de PUT con una carga útil que incluya el formulario actualizado de la directiva en su totalidad. En otras palabras, la solicitud del PUT esencialmente reescribe la política.

>[!NOTE]
>
>Consulte la sección sobre la [actualización de una porción de una directiva](#patch) personalizada si solo desea actualizar uno o varios campos de una directiva en lugar de sobrescribirla.

**Formato API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` de la directiva que desea actualizar. |

**Solicitud**

En este ejemplo, las condiciones para exportar datos a un tercero han cambiado y ahora se requiere la directiva que se ha creado para denegar esta acción de marketing si hay etiquetas de datos presentes `C1 AND C5` .

La siguiente solicitud actualiza la directiva existente para incluir la nueva expresión de directiva. Tenga en cuenta que, como esta solicitud esencialmente vuelve a escribir la directiva, todos los campos deben incluirse en la carga útil, incluso aunque algunos de sus valores no se estén actualizando.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre para mostrar de la directiva. |
| `status` | El estado actual de la política. Existen tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las directivas participan en la evaluación. Consulte la información general sobre la evaluación [de](../enforcement/overview.md) políticas para obtener más información. |
| `marketingActionRefs` | Una matriz que lista los URI de todas las acciones de marketing aplicables para la política. El URI de una acción de marketing se proporciona en `_links.self.href` la respuesta para [buscar una acción](./marketing-actions.md#look-up)de marketing. |
| `description` | Descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | La expresión de directiva que describe las etiquetas de uso de datos específicas en las que se restringe la acción de marketing asociada a la política para que no se realice. Consulte la sección sobre la [creación de una política](#create-policy) para obtener más información sobre esta propiedad. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva actualizada.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Actualizar una parte de una directiva personalizada {#patch}

>[!IMPORTANT]
>
>Solo puede actualizar directivas personalizadas. Si desea habilitar o deshabilitar las directivas principales, consulte la sección sobre [actualización de la lista de las directivas](#update-enabled-core)principales habilitadas.

Una porción específica de una directiva se puede actualizar mediante una solicitud de PATCH. A diferencia de las solicitudes de PUT que reescriben la directiva, las solicitudes de PATCH actualizan solo las propiedades especificadas en el cuerpo de la solicitud. Esto resulta especialmente útil cuando desea habilitar o deshabilitar una directiva, ya que solo necesita proporcionar la ruta a la propiedad (`/status`) adecuada y a su valor (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>Las cargas de las solicitudes de PATCH siguen el formato JSON Patch. Consulte la guía [de aspectos fundamentales de la](../../landing/api-fundamentals.md) API para obtener más información sobre la sintaxis aceptada.

La [!DNL Policy Service] API admite las operaciones `add`de parche JSON `remove`, y `replace`, y le permite combinar varias actualizaciones en una sola llamada, como se muestra en el ejemplo siguiente.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` de la directiva cuyas propiedades desea actualizar. |

**Solicitud**

La siguiente solicitud utiliza dos `replace` operaciones para cambiar el estado de la directiva de `DRAFT` a `ENABLED`y para actualizar el `description` campo con una nueva descripción.

>[!IMPORTANT]
>
>Al enviar varias operaciones de PATCH en una sola solicitud, se procesarán en el orden en que aparecen en la matriz. Asegúrese de enviar las solicitudes en el orden correcto cuando sea necesario.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva actualizada.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Eliminar una directiva personalizada {#delete}

Puede eliminar una directiva personalizada incluyendo su `id` en la ruta de una solicitud de DELETE.

>[!WARNING]
>
>Una vez eliminadas, las políticas no se pueden recuperar. Se recomienda [realizar primero una solicitud](#lookup) de búsqueda (GET) para vista de la directiva y confirmar que es la directiva correcta que desea eliminar.

**Formato API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | ID de la directiva que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Aceptar) con un cuerpo en blanco.

Para confirmar la eliminación, intente buscar (GET) la directiva de nuevo. Debe recibir un error HTTP 404 (no encontrado) si la directiva se ha eliminado correctamente.

## Recuperar una lista de directivas principales habilitadas {#list-enabled-core}

De forma predeterminada, solo participan en la evaluación las directivas de uso de datos habilitadas. Puede recuperar una lista de directivas principales que su organización haya habilitado actualmente haciendo una solicitud de GET al extremo del `/enabledCorePolicies` .

**Formato API**

```http
GET /enabledCorePolicies
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la lista de directivas principales habilitadas en una `policyIds` matriz.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Actualizar la lista de directivas principales habilitadas {#update-enabled-core}

De forma predeterminada, solo participan en la evaluación las directivas de uso de datos habilitadas. Al realizar una solicitud de PUT al extremo, puede actualizar la lista de directivas principales habilitadas para la organización mediante una sola llamada. `/enabledCorePolicies`

>[!NOTE]
>
>Este extremo solo puede habilitar o deshabilitar las directivas principales. Para habilitar o deshabilitar las directivas personalizadas, consulte la sección sobre la [actualización de una porción de una directiva](#patch).

**Formato API**

```http
PUT /enabledCorePolicies
```

**Solicitud**

La siguiente solicitud actualiza la lista de las directivas principales habilitadas en función de los ID proporcionados en la carga útil.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `policyIds` | Lista de ID de directivas principales que se van a habilitar. Todas las políticas básicas que no se incluyan se establecen en `DISABLED` estado y no participarán en la evaluación. |

**Respuesta**

Una respuesta correcta devuelve la lista actualizada de las directivas principales habilitadas en una `policyIds` matriz.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Pasos siguientes

Una vez definidas las nuevas directivas o actualizadas las existentes, puede utilizar la API para probar las acciones de marketing con etiquetas o conjuntos de datos específicos y ver si las políticas generan infracciones según lo esperado. [!DNL Policy Service] Para obtener más información, consulte la guía sobre los parámetros [de evaluación de](./evaluation.md) políticas.