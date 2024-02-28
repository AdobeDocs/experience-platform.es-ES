---
keywords: Experience Platform;inicio;temas populares;aplicación de políticas;aplicación basada en API;control de datos
solution: Experience Platform
title: Punto final de API de políticas de gobernanza de datos
description: Las políticas de gobernanza de datos son reglas que adopta su organización y que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de Experience Platform. El extremo /policies se utiliza para todas las llamadas a la API relacionadas con la visualización, creación, actualización o eliminación de directivas de control de datos.
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 3%

---

# Extremo de políticas de gobernanza de datos

Las políticas de gobernanza de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de [!DNL Experience Platform]. El `/policies` punto final en la [!DNL Policy Service API] le permite administrar mediante programación las directivas de control de datos de su organización.

>[!IMPORTANT]
>
>Las políticas de gobernanza no se deben confundir con las políticas de control de acceso, que determinan los atributos de datos específicos a los que pueden acceder determinados usuarios de Platform en su organización. Consulte la `/policies` guía de extremo para [API de control de acceso](../../access-control/abac/api/policies.md) para obtener más información sobre cómo administrar mediante programación las directivas de control de acceso.

## Introducción

El extremo de API utilizado en esta guía forma parte del [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, consulte la [guía de introducción](getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier [!DNL Experience Platform] API.

## Recuperación de una lista de directivas {#list}

Puede enumerar todos `core` o `custom` políticas realizando una solicitud de GET a `/policies/core` o `/policies/custom`, respectivamente.

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

Una respuesta correcta incluye una `children` matriz que enumera los detalles de cada directiva recuperada, incluido su `id` valores. Puede usar el complemento `id` campo de una directiva concreta que se va a realizar [búsqueda](#lookup), [actualizar](#update), y [eliminar](#delete) solicitudes de esa directiva.

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
| `name` | El nombre para mostrar de una directiva. |
| `status` | El estado actual de una directiva. Hay tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la información general sobre [evaluación política](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Matriz que enumera los URI de todas las acciones de marketing aplicables para una directiva. |
| `description` | Una descripción opcional que proporciona más contexto al caso de uso de la directiva. |
| `deny` | Un objeto que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a una directiva está restringida para que no se realice. Consulte la sección sobre [creación de una directiva](#create-policy) para obtener más información sobre esta propiedad. |

## Buscar una directiva {#look-up}

Puede buscar una directiva específica incluyendo la de `id` en la ruta de una petición GET.

**Formato de API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` de la directiva que desea buscar. |

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
| `name` | El nombre para mostrar de la directiva. |
| `status` | El estado actual de la directiva. Hay tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la información general sobre [evaluación política](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Una matriz que enumera los URI de todas las acciones de marketing aplicables para la directiva. |
| `description` | Una descripción opcional que proporciona más contexto al caso de uso de la directiva. |
| `deny` | Un objeto que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la política está restringida para que no se realicen. Consulte la sección sobre [creación de una directiva](#create-policy) para obtener más información sobre esta propiedad. |

## Crear una directiva personalizada {#create-policy}

En el [!DNL Policy Service] API, una política se define de la siguiente manera:

* Una referencia a una acción de marketing específica
* Una expresión que describe las etiquetas de uso de datos con las que está restringida la acción de marketing

Para cumplir este último requisito, las definiciones de políticas deben incluir una expresión booleana con respecto a la presencia de etiquetas de uso de datos. Esta expresión se denomina expresión de directiva.

Las expresiones de política se proporcionan en forma de `deny` dentro de cada definición de directiva. Un ejemplo de un `deny` que solo comprueba la presencia de una sola etiqueta tendría el siguiente aspecto:

```json
"deny": {
    "label": "C1"
}
```

Sin embargo, muchas políticas especifican condiciones más complejas con respecto a la presencia de etiquetas de uso de datos. Para admitir estos casos de uso, también puede incluir operaciones booleanas para describir las expresiones de directiva. El objeto de expresión de directiva debe contener una etiqueta o un operador y operandos, pero no ambos. A su vez, cada operando también es un objeto de expresión de directiva.

Por ejemplo, para definir una política que prohíba que se realice una acción de marketing en datos en los que `C1 OR (C3 AND C7)` están presentes, las etiquetas `deny` La propiedad se especificaría como:

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
| `operator` | Indica la relación condicional entre las etiquetas proporcionadas en el elemento secundario `operands` matriz. Los valores aceptados son: <ul><li>`OR`: la expresión se resuelve en true si alguna de las etiquetas de la variable `operands` están presentes.</li><li>`AND`: la expresión solo se resuelve en true si todas las etiquetas del `operands` están presentes.</li></ul> |
| `operands` | Matriz de objetos, cada uno de los cuales representa una sola etiqueta o un par adicional de `operator` y `operands` propiedades. La presencia de las etiquetas u operaciones en un `operands` la matriz se resuelve en true o false en función del valor de su elemento secundario `operator` propiedad. |
| `label` | El nombre de una sola etiqueta de uso de datos que se aplica a la directiva. |

Puede crear una nueva directiva personalizada realizando una solicitud de POST a `/policies/custom` punto final.

**Formato de API**

```http
POST /policies/custom
```

**Solicitud**

La siguiente solicitud crea una nueva directiva que restringe la acción de marketing `exportToThirdParty` de realizarse en datos que contengan etiquetas `C1 OR (C3 AND C7)`.

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
| `name` | El nombre para mostrar de la directiva. |
| `status` | El estado actual de la directiva. Hay tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la información general sobre [evaluación política](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Una matriz que enumera los URI de todas las acciones de marketing aplicables para la directiva. El URI de una acción de marketing se proporciona en `_links.self.href` en la respuesta de [búsqueda de una acción de marketing](./marketing-actions.md#look-up). |
| `description` | Una descripción opcional que proporciona más contexto al caso de uso de la directiva. |
| `deny` | La expresión de directiva que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la directiva está restringida para que no se realice. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva recién creada, incluido su `id`. Este valor es de sólo lectura y se asigna automáticamente cuando se crea la directiva.

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
>Solo puede actualizar las directivas personalizadas. Si desea habilitar o deshabilitar directivas principales, consulte la sección sobre [actualización de la lista de directivas principales habilitadas](#update-enabled-core).

Puede actualizar una directiva personalizada existente proporcionando su ID en la ruta de una solicitud de PUT con una carga útil que incluya el formulario actualizado de la directiva en su totalidad. En otras palabras, la solicitud del PUT básicamente reescribe la directiva.

>[!NOTE]
>
>Consulte la sección sobre [actualizar una parte de una directiva personalizada](#patch) si solo desea actualizar uno o más campos para una directiva, en lugar de sobrescribirlos.

**Formato de API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` de la directiva que desea actualizar. |

**Solicitud**

En este ejemplo, las condiciones para exportar datos a un tercero han cambiado y ahora necesita la directiva que ha creado para denegar esta acción de marketing si `C1 AND C5` hay etiquetas de datos.

La siguiente solicitud actualiza la directiva existente para incluir la nueva expresión de directiva. Tenga en cuenta que, como esta solicitud básicamente reescribe la directiva, todos los campos deben incluirse en la carga útil, incluso si algunos de sus valores no se actualizan.

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
| `name` | El nombre para mostrar de la directiva. |
| `status` | El estado actual de la directiva. Hay tres estados posibles: `DRAFT`, `ENABLED`, o `DISABLED`. De forma predeterminada, solo `ENABLED` las políticas participan en la evaluación. Consulte la información general sobre [evaluación política](../enforcement/overview.md) para obtener más información. |
| `marketingActionRefs` | Una matriz que enumera los URI de todas las acciones de marketing aplicables para la directiva. El URI de una acción de marketing se proporciona en `_links.self.href` en la respuesta de [búsqueda de una acción de marketing](./marketing-actions.md#look-up). |
| `description` | Una descripción opcional que proporciona más contexto al caso de uso de la directiva. |
| `deny` | La expresión de directiva que describe las etiquetas de uso de datos específicas en las que la acción de marketing asociada a la directiva está restringida para que no se realice. Consulte la sección sobre [creación de una directiva](#create-policy) para obtener más información sobre esta propiedad. |

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
>Solo puede actualizar las directivas personalizadas. Si desea habilitar o deshabilitar directivas principales, consulte la sección sobre [actualización de la lista de directivas principales habilitadas](#update-enabled-core).

Una parte específica de una directiva se puede actualizar mediante una solicitud de PATCH. A diferencia de las solicitudes de PUT que reescriben la directiva, las solicitudes de PATCH actualizan únicamente las propiedades especificadas en el cuerpo de la solicitud. Esto resulta especialmente útil cuando desea habilitar o deshabilitar una directiva, ya que solo necesita proporcionar la ruta a la propiedad adecuada (`/status`) y su valor (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>Las cargas útiles para solicitudes de PATCH siguen el formato de parche JSON. Consulte la [Guía de aspectos básicos de API](../../landing/api-fundamentals.md) para obtener más información sobre la sintaxis aceptada.

El [!DNL Policy Service] La API admite las operaciones de parches de JSON `add`, `remove`, y `replace`y le permite combinar varias actualizaciones en una sola llamada, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` de la directiva cuyas propiedades desea actualizar. |

**Solicitud**

La siguiente solicitud utiliza dos `replace` operaciones desde las que cambiar el estado de la directiva `DRAFT` hasta `ENABLED`y para actualizar el `description` con una nueva descripción.

>[!IMPORTANT]
>
>Cuando se envían varias operaciones de PATCH en una sola solicitud, se procesan en el orden en que aparecen en la matriz. Asegúrese de enviar las solicitudes en el orden correcto cuando sea necesario.

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

Puede eliminar una directiva personalizada incluyendo su `id` en la ruta de una petición de DELETE.

>[!WARNING]
>
>Una vez eliminadas, las directivas no se pueden recuperar. Se recomienda hacer lo siguiente [realizar una solicitud de búsqueda (GET)](#lookup) en primer lugar, para ver la directiva y confirmar que es la correcta que desea eliminar.

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

Para confirmar la eliminación, intente buscar (GET) la directiva de nuevo. Debería recibir un error HTTP 404 (no encontrado) si la directiva se ha eliminado correctamente.

## Recuperar una lista de directivas principales habilitadas {#list-enabled-core}

De forma predeterminada, solo las políticas de gobernanza de datos habilitadas participan en la evaluación. Puede recuperar una lista de las directivas principales actualmente habilitadas por su organización realizando una solicitud de GET a `/enabledCorePolicies` punto final.

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

De forma predeterminada, solo las políticas de gobernanza de datos habilitadas participan en la evaluación. Realizando una solicitud de PUT a `/enabledCorePolicies` punto final, puede actualizar la lista de directivas principales habilitadas para su organización mediante una sola llamada.

>[!NOTE]
>
>Este extremo solo puede habilitar o deshabilitar las directivas principales. Para habilitar o deshabilitar directivas personalizadas, consulte la sección sobre [actualizar una parte de una directiva](#patch).

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
| `policyIds` | Lista de ID de directivas principales que se van a habilitar. Las políticas principales que no se incluyan se establecen en `DISABLED` estado y no participarán en la evaluación. |

**Respuesta**

Una respuesta correcta devuelve la lista actualizada de directivas principales habilitadas en un `policyIds` matriz.

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

Una vez que haya definido nuevas directivas o actualizado las existentes, puede utilizar el [!DNL Policy Service] API para probar acciones de marketing con etiquetas o conjuntos de datos específicos y ver si las políticas están generando infracciones según lo esperado. Consulte la guía en la [extremos de evaluación de directivas](./evaluation.md) para obtener más información.
