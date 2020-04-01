---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# Políticas

Las políticas de uso de datos son reglas que su organización adopta que describen los tipos de acciones de marketing que puede realizar o que tiene restringido el acceso a los datos dentro de la plataforma de experiencia.

El extremo se utiliza para todas las llamadas de API relacionadas con la visualización, creación, actualización o eliminación de directivas de uso de datos. `/policies`

## Lista de todas las políticas

Para vista de una lista de políticas, se puede realizar una solicitud GET a `/policies/core` o `/policies/custom` que devuelve todas las directivas para el contenedor especificado.

**Formato API**

```http
GET /policies/core
GET /policies/custom
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye un &quot;recuento&quot; que muestra el número total de políticas dentro del contenedor especificado, así como los detalles de cada política, incluida su `id`. El `id` campo se utiliza para realizar solicitudes de búsqueda para vista de directivas específicas, así como para realizar operaciones de actualización y eliminación.

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## Buscar directiva específica

Cada directiva contiene un `id` campo que puede utilizarse para solicitar los detalles de una directiva específica. Si se desconoce el contenido `id` de una política, se puede encontrar mediante la solicitud de listado (GET) para lista de todas las directivas dentro de un contenedor específico (`core` o `custom`), como se muestra en el paso anterior.

**Formato API**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta contiene los detalles de la política, incluidos los campos clave como `id` (este campo debe coincidir con el `id` enviado en la solicitud), `name`, `status`y `description`, así como un vínculo de referencia a la acción de marketing en la que se basa la política (`marketingActionRefs`).

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Crear una directiva {#create-policy}

La creación de una directiva requiere la inclusión de una acción de marketing con una expresión de las etiquetas DULE que prohíben esa acción de marketing. Las definiciones de directiva deben incluir una `deny` propiedad, que es una expresión booleana con respecto a la presencia de etiquetas DULE.

Esta expresión se denomina `PolicyExpression` y es un objeto que contiene _una etiqueta_ o __ un operador y operandos, pero no ambos. A su vez, cada operando es también un `PolicyExpression` objeto. Por ejemplo, una política relativa a la exportación de datos a un tercero podría estar prohibida si están presentes `C1 OR (C3 AND C7)` etiquetas. Esta expresión se especificaría como:

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

**Formato API**

```http
POST /policies/custom
```

**Solicitud**

```SHELL
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
          "../marketingActions/custom/exportToThirdParty"
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

**Respuesta**

Si se crea correctamente, recibirá un estado HTTP 201 (Creado) y el cuerpo de respuesta contendrá los detalles de la directiva recién creada, incluyendo su `id`. Este valor es de sólo lectura y se asigna automáticamente cuando se crea la directiva.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Actualizar una directiva

Es posible que deba actualizar una directiva de uso de datos después de haberla creado. Esto se realiza mediante una solicitud PUT a la política `id` con una carga útil que incluye la forma actualizada de la política en su totalidad. En otras palabras, la solicitud de PUT consiste esencialmente en _reescribir_ la política, por lo que el organismo debe incluir toda la información necesaria, como se muestra en el ejemplo siguiente.

**Formato API**

```http
PUT /policies/custom/{id}
```

**Solicitud**

En este ejemplo, las condiciones para exportar datos a un tercero han cambiado y ahora se requiere la directiva que se ha creado para denegar esta acción de marketing si hay etiquetas de datos presentes `C1 AND (C3 OR C7)` . Utilizaría la siguiente llamada para actualizar la directiva existente.

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Respuesta**

Una solicitud de actualización correcta devuelve un estado HTTP 200 (Aceptar) y el cuerpo de respuesta mostrará la directiva actualizada. El `id` debe coincidir con el `id` enviado en la solicitud.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Actualizar una parte de una directiva

Una porción específica de una directiva se puede actualizar mediante una solicitud PATCH. A diferencia de las solicitudes PUT que _reescriben_ la directiva, las solicitudes PATCH actualizan solo la ruta especificada en el cuerpo de la solicitud. Esto resulta especialmente útil cuando desea habilitar o deshabilitar una directiva, ya que solo necesita enviar la ruta específica que desea actualizar (`/status`) y su valor (`ENABLE` o `DISABLE`).

Actualmente, la API de servicio de directivas admite operaciones de &quot;agregar&quot;, &quot;reemplazar&quot; y &quot;quitar&quot; PARCH, y permite combinar varias actualizaciones en una sola llamada agregando cada una como un objeto dentro de la matriz, como se muestra en los ejemplos siguientes.

**Formato API**

```http
PATCH /policies/custom/{id}
```

**Solicitud**

En este ejemplo, utilizamos la operación &quot;reemplazar&quot; para cambiar el estado de la directiva de &quot;BORRADOR&quot; a &quot;HABILITADO&quot; y para actualizar el campo de descripción con una nueva descripción. También se podría haber actualizado el campo de descripción mediante la operación &quot;eliminar&quot; para eliminar la descripción de la política y, a continuación, mediante la operación &quot;agregar&quot; para agregar una nueva vez, de este modo:

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

Al enviar varias operaciones PATCH en una sola solicitud, recuerde que se procesarán en el orden en que aparecen en la matriz, de modo que asegúrese de que envía las solicitudes en el orden correcto cuando sea necesario.

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

Una solicitud de actualización correcta devolverá un estado HTTP 200 (Aceptar) y el cuerpo de respuesta mostrará la directiva actualizada (&quot;estado&quot; ahora es &quot;HABILITADO&quot; y &quot;descripción&quot; se ha cambiado). La directiva `id` debe coincidir con la `id` enviada en la solicitud.


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Eliminar una directiva

Si necesita eliminar una directiva que haya creado, puede hacerlo enviando una solicitud DELETE al `id` de la directiva que desee eliminar. Se recomienda realizar primero una solicitud de búsqueda (GET) para vista de la directiva y confirmar que es la directiva correcta que desea eliminar. **Una vez eliminadas, las políticas no se pueden recuperar.**

**Formato API**

```http
DELETE /policies/custom/{id}
```

**Solicitud**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Si la directiva se ha eliminado correctamente, el cuerpo de la respuesta estará en blanco con un estado HTTP 200 (correcto).

Para confirmar la eliminación, intente buscar (OBTENER) la directiva de nuevo. Debe recibir un estado HTTP 404 (no encontrado) junto con un mensaje de error &quot;No encontrado&quot; porque la directiva se ha eliminado.
