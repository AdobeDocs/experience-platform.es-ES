---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;aplicación basada en API;control de datos
solution: Experience Platform
title: Punto final de la API de políticas de administración de datos
description: Las políticas de control de datos son reglas que adopta su organización y que describen los tipos de acciones de marketing que puede realizar o de las que está restringido el cumplimiento de los datos dentro de un Experience Platform. El extremo /policy se utiliza para todas las llamadas de API relacionadas con la visualización, la creación, la actualización o la eliminación de directivas de control de datos.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 3%

---

# Punto final de las políticas de control de datos

Las políticas de control de datos son reglas que describen los tipos de acciones de marketing que puede realizar o de las que se le restringe el uso de datos dentro de [!DNL Experience Platform]. La variable `/policies` en la variable [!DNL Policy Service API] le permite administrar mediante programación las políticas de control de datos de su organización.

>[!IMPORTANT]
>
>Las políticas de administración no deben confundirse con las políticas de control de acceso, que determinan los atributos de datos específicos a los que pueden acceder ciertos usuarios de Platform de su organización. Consulte la `/policies` guía de extremo para la variable [API de control de acceso](../../access-control/abac/api/policies.md) para obtener más información sobre cómo administrar las políticas de control de acceso mediante programación.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la variable [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, revise la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier [!DNL Experience Platform] API.

## Recuperar una lista de directivas {#list}

Puede enumerar todo `core` o `custom` directivas realizando una solicitud de GET a `/policies/core` o `/policies/custom`, respectivamente.

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta incluye una `children` matriz que enumera los detalles de cada directiva recuperada, incluidas sus `id` valores. Puede usar la variable `id` campo de una directiva determinada que se va a realizar [búsqueda](#lookup), [actualizar](#update)y [delete](#delete) solicitudes de dicha directiva.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `status` | Estado actual de una directiva. Hay tres estados posibles: `DRAFT`, `ENABLED`o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la descripción general sobre [evaluación de políticas](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Matriz que enumera los URI de todas las acciones de marketing aplicables a una directiva. |
| `description` | Una descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | Un objeto que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a una directiva está restringida de realizarse. Consulte la sección sobre [creación de una directiva](#create-policy) para obtener más información sobre esta propiedad. |

## Buscar una directiva {#look-up}

Puede consultar una directiva específica incluyendo la `id` en la ruta de una solicitud de GET.

**Formato de API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | La variable `id` de la directiva que desea buscar. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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
| `status` | Estado actual de la política. Hay tres estados posibles: `DRAFT`, `ENABLED`o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la descripción general sobre [evaluación de políticas](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Matriz que enumera los URI de todas las acciones de marketing aplicables a la directiva. |
| `description` | Una descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | Un objeto que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la directiva está restringida de realizarse. Consulte la sección sobre [creación de una directiva](#create-policy) para obtener más información sobre esta propiedad. |

## Crear una directiva personalizada {#create-policy}

En el [!DNL Policy Service] , una política se define de la siguiente manera:

* Una referencia a una acción de marketing específica
* Expresión que describe las etiquetas de uso de datos con las que la acción de marketing está restringida para no realizarse

Para satisfacer este último requisito, las definiciones de políticas deben incluir una expresión booleana con respecto a la presencia de etiquetas de uso de datos. Esta expresión se denomina expresión de política.

Las expresiones de política se proporcionan en forma de `deny` dentro de cada definición de directiva. Un ejemplo de `deny` que solo comprueba la presencia de una única etiqueta tendría el siguiente aspecto:

```json
"deny": {
    "label": "C1"
}
```

Sin embargo, muchas políticas especifican condiciones más complejas con respecto a la presencia de etiquetas de uso de datos. Para admitir estos casos de uso, también puede incluir operaciones booleanas para describir sus expresiones de directiva. El objeto de expresión de directiva debe contener una etiqueta o un operador y operandos, pero no ambos. A su vez, cada operando también es un objeto de expresión de política.

Por ejemplo, para definir una directiva que prohíba que una acción de marketing se realice en datos en los que `C1 OR (C3 AND C7)` las etiquetas están presentes, el `deny` se especificaría como:

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
| `operator` | Indica la relación condicional entre las etiquetas proporcionadas en el elemento del mismo nivel `operands` matriz. Los valores aceptados son: <ul><li>`OR`: La expresión se resuelve en true si alguna de las etiquetas de la variable `operands` están presentes.</li><li>`AND`: La expresión solo se resuelve en true si todas las etiquetas de la variable `operands` están presentes.</li></ul> |
| `operands` | Matriz de objetos, cada uno de los cuales representa una única etiqueta o un par adicional de `operator` y `operands` propiedades. La presencia de etiquetas y/o operaciones en un `operands` la matriz se resuelve en true o false en función del valor de su elemento secundario `operator` propiedad. |
| `label` | Nombre de una etiqueta de uso de datos única que se aplica a la directiva. |

Puede crear una nueva directiva personalizada realizando una solicitud de POST al `/policies/custom` punto final.

**Formato de API**

```http
POST /policies/custom
```

**Solicitud**

La siguiente solicitud crea una nueva directiva que restringe la acción de marketing `exportToThirdParty` desde que se realiza en datos que contienen etiquetas `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | Estado actual de la política. Hay tres estados posibles: `DRAFT`, `ENABLED`o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la descripción general sobre [evaluación de políticas](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Matriz que enumera los URI de todas las acciones de marketing aplicables a la directiva. El URI de una acción de marketing se proporciona en `_links.self.href` en la respuesta de [búsqueda de una acción de marketing](./marketing-actions.md#look-up). |
| `description` | Una descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | La expresión de directiva que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la directiva está restringida de realizarse. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la política recién creada, incluido su `id`. Este valor es de solo lectura y se asigna automáticamente cuando se crea la directiva.

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
    "imsOrg": "{ORG_ID}",
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
>Solo puede actualizar las directivas personalizadas. Si desea habilitar o deshabilitar las directivas principales, consulte la sección de [actualización de la lista de directivas principales habilitadas](#update-enabled-core).

Puede actualizar una directiva personalizada existente proporcionando su ID en la ruta de una solicitud de PUT con una carga útil que incluya el formulario actualizado de la directiva en su totalidad. En otras palabras, la solicitud del PUT esencialmente reescribe la política.

>[!NOTE]
>
>Consulte la sección sobre [actualizar una parte de una directiva personalizada](#patch) si solo desea actualizar uno o más campos de una directiva, en lugar de sobrescribirlos.

**Formato de API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | La variable `id` de la directiva que desea actualizar. |

**Solicitud**

En este ejemplo, las condiciones para exportar datos a un tercero han cambiado y ahora necesita la política que ha creado para denegar esta acción de marketing si `C1 AND C5` están presentes las etiquetas de datos.

La siguiente solicitud actualiza la directiva existente para incluir la nueva expresión de directiva. Tenga en cuenta que, como esta solicitud esencialmente reescribe la directiva, todos los campos deben incluirse en la carga útil, incluso aunque algunos de sus valores no se estén actualizando.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | Estado actual de la política. Hay tres estados posibles: `DRAFT`, `ENABLED`o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la descripción general sobre [evaluación de políticas](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Matriz que enumera los URI de todas las acciones de marketing aplicables a la directiva. El URI de una acción de marketing se proporciona en `_links.self.href` en la respuesta de [búsqueda de una acción de marketing](./marketing-actions.md#look-up). |
| `description` | Una descripción opcional que proporciona un contexto adicional al caso de uso de la directiva. |
| `deny` | La expresión de directiva que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la directiva está restringida de realizarse. Consulte la sección sobre [creación de una directiva](#create-policy) para obtener más información sobre esta propiedad. |

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
    "imsOrg": "{ORG_ID}",
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
>Solo puede actualizar las directivas personalizadas. Si desea habilitar o deshabilitar las directivas principales, consulte la sección de [actualización de la lista de directivas principales habilitadas](#update-enabled-core).

Se puede actualizar una parte específica de una directiva mediante una solicitud del PATCH. A diferencia de las solicitudes del PUT que reescriben la directiva, el PATCH solicita actualizar solo las propiedades especificadas en el cuerpo de la solicitud. Esto resulta especialmente útil cuando desea habilitar o deshabilitar una directiva, ya que solo necesita proporcionar la ruta a la propiedad adecuada (`/status`) y su valor (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>Las cargas útiles para solicitudes de PATCH siguen el formato JSON Patch . Consulte la [Guía de fundamentos de API](../../landing/api-fundamentals.md) para obtener más información sobre la sintaxis aceptada.

La variable [!DNL Policy Service] La API admite las operaciones de parches de JSON `add`, `remove`y `replace`, y le permite combinar varias actualizaciones en una sola llamada, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | La variable `id` de la directiva cuyas propiedades desee actualizar. |

**Solicitud**

La siguiente solicitud utiliza dos `replace` operaciones para cambiar el estado de la directiva de `DRAFT` a `ENABLED`y para actualizar el `description` con una nueva descripción.

>[!IMPORTANT]
>
>Al enviar varias operaciones de PATCH en una sola solicitud, se procesan en el orden en que aparecen en la matriz. Asegúrese de que está enviando las solicitudes en el orden correcto cuando sea necesario.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Puede eliminar una directiva personalizada incluyendo su `id` en la ruta de una solicitud del DELETE.

>[!WARNING]
>
>Una vez eliminadas, las políticas no se pueden recuperar. Se recomienda [realizar una solicitud de búsqueda (GET)](#lookup) primero, vea la directiva y confirme que es la directiva correcta que desea eliminar.

**Formato de API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El ID de la directiva que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) con un cuerpo en blanco.

Puede confirmar la eliminación intentando buscar (GET) la directiva de nuevo. Debería recibir un error HTTP 404 (no encontrado) si la directiva se ha eliminado correctamente.

## Recuperar una lista de directivas principales habilitadas {#list-enabled-core}

De forma predeterminada, solo participan en la evaluación las políticas de control de datos habilitadas. Puede recuperar una lista de las directivas principales que su organización ha habilitado actualmente realizando una solicitud de GET a la `/enabledCorePolicies` punto final.

**Formato de API**

```http
GET /enabledCorePolicies
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la lista de directivas principales activadas en una `policyIds` matriz.

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
  "imsOrg": "{ORG_ID}",
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

De forma predeterminada, solo participan en la evaluación las políticas de control de datos habilitadas. Haciendo una solicitud de PUT al `/enabledCorePolicies` , puede actualizar la lista de directivas principales habilitadas para su organización mediante una sola llamada.

>[!NOTE]
>
>Este extremo solo puede habilitar o deshabilitar las directivas principales. Para habilitar o deshabilitar directivas personalizadas, consulte la sección de [actualizar una parte de una directiva](#patch).

**Formato de API**

```http
PUT /enabledCorePolicies
```

**Solicitud**

La siguiente solicitud actualiza la lista de directivas principales habilitadas en función de los ID proporcionados en la carga útil.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `policyIds` | Una lista de los ID de directivas principales que se van a habilitar. Todas las políticas principales que no estén incluidas se establecen en `DISABLED` y no participará en la evaluación. |

**Respuesta**

Una respuesta correcta devuelve la lista actualizada de directivas principales activadas en una `policyIds` matriz.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
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

Una vez definidas las nuevas directivas o actualizadas las existentes, puede usar la variable [!DNL Policy Service] API para probar acciones de marketing con etiquetas o conjuntos de datos específicos y ver si las políticas están generando infracciones como se espera. Consulte la guía de [extremos de evaluación de políticas](./evaluation.md) para obtener más información.
