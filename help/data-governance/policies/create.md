---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear una directiva de uso de datos
topic: policies
translation-type: tm+mt
source-git-commit: ba9d4b31cfc3b7924879a91bd125f72159e55fc4
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 2%

---


# Crear una directiva de uso de datos en la API

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo central del gobierno de datos de Adobe Experience Platform. La [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) le permite crear y administrar políticas DULE para determinar qué acciones de mercadotecnia se pueden realizar con datos que contienen ciertas etiquetas DULE.

Este documento proporciona un tutorial paso a paso para crear una directiva DULE mediante la API de servicio de directivas. Para obtener una guía más completa de las distintas operaciones disponibles en la API, consulte la guía [para desarrolladores de](../api/getting-started.md)Policy Service.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes conceptos clave relacionados con la creación y evaluación de las políticas DULE:

* [Administración](../home.md)de datos: El marco mediante el cual Platform impone el cumplimiento de la normativa de uso de datos.
* [Etiquetas](../labels/overview.md)de uso de datos: Las etiquetas de uso de datos se aplican a los campos de datos XDM, especificando restricciones para acceder a los datos.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [Simuladores](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la guía [para](../api/getting-started.md) desarrolladores para obtener información importante que necesita conocer a fin de realizar llamadas exitosas a la API del servicio de directivas DULE, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Definir una acción de mercadotecnia {#define-action}

En el marco de la Administración de datos, una acción de marketing es una acción que realiza un consumidor de datos Experience Platform, para la cual es necesario verificar las infracciones de las políticas de uso de datos.

El primer paso para crear una política DULE es determinar qué acción de mercadotecnia evaluará la política. Esto se puede realizar con una de las siguientes opciones:

* [Buscar una acción de mercadotecnia existente](#look-up)
* [Crear una nueva acción de mercadotecnia](#create-new)

### Buscar una acción de mercadotecnia existente {#look-up}

Puede consultar las acciones de marketing existentes que su directiva DULE debe evaluar mediante una solicitud GET a uno de los `/marketingActions` extremos.

**Formato API**

En función de si está buscando una acción de marketing proporcionada por un Experience Platform o una acción de marketing personalizada creada por su organización, utilice los puntos finales `marketingActions/core` o `marketingActions/custom` finales, respectivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud utiliza el punto final, que obtiene una lista de todas las acciones de marketing definidas por la organización de IMS. `marketingActions/custom`

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el número total de acciones de mercadotecnia encontradas (`count`) y lista los detalles de las propias acciones de mercadotecnia dentro de la `children` matriz.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `_links.self.href` | Cada elemento de la `children` matriz contiene un identificador URI para la acción de marketing de la lista. |

Cuando encuentre la acción de marketing que desea utilizar, registre el valor de su `href` propiedad. Este valor se utiliza durante el próximo paso de [crear una directiva](#create-policy)DULE.

### Crear una nueva acción de mercadotecnia {#create-new}

Puede crear una nueva acción de mercadotecnia realizando una solicitud PUT al extremo y proporcionando un nombre para la acción de mercadotecnia al final de la ruta de solicitud. `/marketingActions/custom/`

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la nueva acción de marketing que desea crear. Este nombre actúa como el identificador principal de la acción de marketing y, por lo tanto, debe ser único. Lo mejor es dar a la acción de mercadotecnia un nombre descriptivo pero conciso. |

**Solicitud**

La siguiente solicitud crea una nueva acción de marketing personalizada denominada &quot;exportToThirdParty&quot;. Observe que `name` en la carga útil de la solicitud es el mismo nombre que el proporcionado en la ruta de la solicitud.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la acción de marketing que desea crear. Este nombre debe coincidir con el nombre proporcionado en la ruta de la solicitud o se producirá un error 400 (Solicitud incorrecta). |
| `description` | Descripción legible por el usuario de la acción de marketing. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y los detalles de la acción de marketing recién creada.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `_links.self.href` | ID de URI de la acción de marketing. |

Registre el identificador URI de la acción de marketing recién creada, tal como se utilizará en el próximo paso de crear una directiva DULE.

## Crear una directiva DULE {#create-policy}

La creación de una nueva directiva requiere que proporcione el identificador URI de una acción de marketing con una expresión de las etiquetas DULE que prohíben esa acción de marketing.

Esta expresión se denomina expresión **de** política y es un objeto que contiene (A) una etiqueta DULE o (B) un operador y operandos, pero no ambos. A su vez, cada operando es también un objeto de expresión de políticas. Por ejemplo, una política relativa a la exportación de datos a un tercero podría estar prohibida si están presentes `C1 OR (C3 AND C7)` etiquetas. Esta expresión se especificaría como:

```json
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
}
```

>[!NOTE] Solo se admiten los operadores OR y AND.

Una vez configurada la expresión de directivas, puede crear una nueva directiva DULE haciendo una solicitud POST al extremo del `/policies/custom` mismo.

**Formato API**

```http
POST /policies/custom
```

**Solicitud**

La siguiente solicitud crea una directiva DULE llamada &quot;Exportar datos a terceros&quot; proporcionando una acción de marketing y una expresión de política en la carga útil de la solicitud.

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

| Propiedad | Descripción |
| --- | --- |
| `marketingActionRefs` | Matriz que contiene el `href` valor de una acción de marketing, obtenido en el paso [](#define-action)anterior. Aunque el ejemplo anterior lista una sola acción de marketing, también se pueden proporcionar varias acciones. |
| `deny` | El objeto de expresión de directivas. Define las etiquetas y condiciones DULE que harían que la política rechazara la acción de marketing a la que se hace referencia en `marketingActionRefs`. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y los detalles de la directiva recién creada.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | Valor de sólo lectura generado por el sistema que identifica de forma exclusiva la política DULE. |

Registre el identificador URI de la directiva DULE recién creada, tal como se utiliza en el paso siguiente para habilitar la directiva.

## Habilitar la directiva DULE

>[!NOTE] Aunque este paso es opcional si desea dejar la directiva DULE en `DRAFT` estado, tenga en cuenta que, de forma predeterminada, una directiva debe tener su estado establecido `ENABLED` para participar en la evaluación. Consulte el tutorial sobre la [aplicación de políticas](../enforcement/api-enforcement.md) DULE para obtener información sobre cómo hacer excepciones para políticas en `DRAFT` estado.

De forma predeterminada, las directivas DULE que tienen sus `status` propiedades establecidas para `DRAFT` no participan en la evaluación. Puede habilitar la directiva para la evaluación realizando una solicitud PATCH en el extremo y proporcionando el identificador único para la directiva al final de la ruta de la solicitud. `/policies/custom/`

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El `id` valor de la directiva que desea habilitar. |

**Solicitud**

La siguiente solicitud realiza una operación PATCH en la `status` propiedad de la directiva DULE, cambiando su valor de `DRAFT` a `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `op` | El tipo de operación PATCH que se va a realizar. Esta solicitud realiza una operación de &quot;reemplazo&quot;. |
| `path` | Ruta al campo que se va a actualizar. Al habilitar una directiva, el valor debe establecerse en &quot;/status&quot;. |
| `value` | El nuevo valor que se asignará a la propiedad especificada en `path`. Esta solicitud establece la propiedad de la política en `status` &quot;HABILITADO&quot;. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Aceptar) y los detalles de la directiva actualizada, con su `status` ahora establecido en `ENABLED`.

```json
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
    "createdUser": "{CREATED_USER}",
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
```

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente una directiva de uso de datos para una acción de marketing. Ahora puede continuar con el tutorial sobre la [aplicación de políticas](../enforcement/api-enforcement.md) de uso de datos para aprender a comprobar las infracciones de políticas y a gestionarlas en la aplicación de experiencia.

Para obtener más información sobre las distintas operaciones disponibles en la API de servicio de directivas, consulte la guía [para desarrolladores de](../api/getting-started.md)Policy Service. Para obtener información sobre cómo aplicar políticas para datos de Perfil de clientes en tiempo real, consulte el tutorial sobre [la aplicación del cumplimiento de la normativa de uso de datos para segmentos](../../segmentation/tutorials/governance.md)de audiencia.

Para obtener información sobre cómo administrar las directivas de uso en la interfaz de usuario del Experience Platform, consulte la guía [de usuario de](user-guide.md)directivas.