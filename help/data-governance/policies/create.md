---
keywords: Experience Platform;inicio;temas populares;control de datos;política de uso de datos
solution: Experience Platform
title: Crear una directiva de uso de datos en la API
topic-legacy: policies
type: Tutorial
description: La API del servicio de directivas le permite crear y administrar políticas de uso de datos para determinar qué acciones de marketing se pueden realizar con datos que contienen ciertas etiquetas de uso de datos. Este documento proporciona un tutorial paso a paso para crear una política mediante la API del servicio de directivas.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 2%

---

# Crear una directiva de uso de datos en la API

La [API del servicio de directivas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) le permite crear y administrar políticas de uso de datos para determinar qué acciones de marketing se pueden realizar con datos que contienen ciertas etiquetas de uso de datos.

Este documento proporciona un tutorial paso a paso para crear una política mediante la API [!DNL Policy Service]. Para obtener una guía más completa de las diferentes operaciones disponibles en la API, consulte la [Guía para desarrolladores del Servicio de directivas](../api/getting-started.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes conceptos clave involucrados en la creación y evaluación de políticas:

* [Administración de datos de Adobe Experience Platform](../home.md): El marco mediante el cual se  [!DNL Platform] aplica el cumplimiento de las normas de uso de datos.
   * [Etiquetas](../labels/overview.md) de uso de datos: Las etiquetas de uso de datos se aplican a los campos de datos XDM, especificando restricciones para el acceso a esos datos.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.
* [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API [!DNL Policy Service] , incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Definir una acción de marketing {#define-action}

En el marco [!DNL Data Governance], una acción de marketing es una acción que realiza un [!DNL Experience Platform] consumidor de datos, para la cual es necesario comprobar las infracciones de las políticas de uso de datos.

El primer paso para crear una política de uso de datos es determinar qué acción de marketing evaluará la política. Esto se puede hacer con una de las siguientes opciones:

* [Buscar una acción de marketing existente](#look-up)
* [Crear una nueva acción de marketing](#create-new)

### Buscar una acción de marketing existente {#look-up}

Puede buscar las acciones de marketing existentes que su directiva debe evaluar realizando una solicitud de GET a uno de los `/marketingActions` extremos.

**Formato de API**

Dependiendo de si está buscando una acción de marketing proporcionada por [!DNL Experience Platform] o una acción de marketing personalizada creada por su organización, utilice los `marketingActions/core` o `marketingActions/custom` extremos, respectivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud utiliza el extremo `marketingActions/custom` , que obtiene una lista de todas las acciones de marketing definidas por su organización de IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el número total de acciones de marketing encontradas (`count`) y enumera los detalles de las propias acciones de marketing dentro de la matriz `children`.

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
| `_links.self.href` | Cada elemento de la matriz `children` contiene un ID de URI para la acción de marketing enumerada. |

Cuando encuentre la acción de marketing que desea utilizar, registre el valor de su propiedad `href` . Este valor se utiliza durante el siguiente paso de [creación de una directiva](#create-policy).

### Crear una nueva acción de marketing {#create-new}

Puede crear una nueva acción de marketing realizando una solicitud de PUT al extremo `/marketingActions/custom/` y proporcionando un nombre para la acción de marketing al final de la ruta de solicitud.

**Formato de API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la nueva acción de marketing que desea crear. Este nombre actúa como identificador principal de la acción de marketing y, por lo tanto, debe ser único. Una práctica recomendada es dar a la acción de marketing un nombre descriptivo pero conciso. |

**Solicitud**

La siguiente solicitud crea una nueva acción de marketing personalizada llamada &quot;exportToThirdParty&quot;. Observe que `name` en la carga útil de la solicitud es el mismo que el nombre proporcionado en la ruta de la solicitud.

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
| `name` | Nombre de la acción de marketing que desea crear. Este nombre debe coincidir con el nombre proporcionado en la ruta de solicitud o se producirá un error 400 (solicitud incorrecta). |
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

Registre el ID de URI de la acción de marketing recién creada, tal como se utilizará en el siguiente paso de creación de una política.

## Crear una directiva {#create-policy}

La creación de una nueva directiva requiere que proporcione el ID de URI de una acción de marketing con una expresión de las etiquetas de uso que prohíben esa acción de marketing.

Esta expresión se denomina expresión de política y es un objeto que contiene (A) una etiqueta o (B) un operador y operandos, pero no ambos. A su vez, cada operando también es un objeto de expresión de política. Por ejemplo, una directiva relativa a la exportación de datos a terceros podría estar prohibida si están presentes las etiquetas `C1 OR (C3 AND C7)` . Esta expresión se especificaría como:

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

>[!NOTE]
>
>Solo se admiten los operadores OR y AND.

Una vez configurada la expresión de directiva, puede crear una nueva directiva realizando una solicitud de POST al extremo `/policies/custom` .

**Formato de API**

```http
POST /policies/custom
```

**Solicitud**

La siguiente solicitud crea una directiva denominada &quot;Exportar datos a terceros&quot; al proporcionar una acción de marketing y una expresión de política en la carga útil de la solicitud.

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
| `marketingActionRefs` | Matriz que contiene el valor `href` de una acción de marketing, obtenido en el [paso anterior](#define-action). Aunque en el ejemplo anterior solo se muestra una acción de marketing, también se pueden proporcionar varias acciones. |
| `deny` | El objeto de expresión de directiva. Define las etiquetas de uso y las condiciones que harían que la directiva rechazara la acción de marketing a la que se hace referencia en `marketingActionRefs`. |

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
| `id` | Valor generado por el sistema de solo lectura que identifica de forma exclusiva la política. |

Registre el ID de URI de la política recién creada, tal como se utiliza en el paso siguiente para habilitar la directiva.

## Habilitar la directiva

>[!NOTE]
>
>Aunque este paso es opcional si desea dejar la directiva en estado `DRAFT`, tenga en cuenta que, de forma predeterminada, una directiva debe tener su estado establecido en `ENABLED` para poder participar en la evaluación. Consulte la guía de [aplicación de directivas](../enforcement/api-enforcement.md) para obtener información sobre cómo hacer excepciones para directivas en estado `DRAFT`.

De forma predeterminada, las directivas que tienen su propiedad `status` establecida en `DRAFT` no participan en la evaluación. Puede habilitar la directiva para la evaluación realizando una solicitud de PATCH al extremo `/policies/custom/` y proporcionando el identificador único para la directiva al final de la ruta de solicitud.

**Formato de API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{POLICY_ID}` | El valor `id` de la directiva que desea habilitar. |

**Solicitud**

La siguiente solicitud realiza una operación de PATCH en la propiedad `status` de la directiva, cambiando su valor de `DRAFT` a `ENABLED`.

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
| `op` | Tipo de operación de PATCH que se va a realizar. Esta solicitud realiza una operación &quot;replace&quot;. |
| `path` | Ruta al campo que se va a actualizar. Al habilitar una directiva, el valor debe establecerse en &quot;/status&quot;. |
| `value` | El nuevo valor que se asignará a la propiedad especificada en `path`. Esta solicitud establece la propiedad `status` de la directiva en &quot;ENABLED&quot;. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y los detalles de la directiva actualizada, con su `status` ahora configurado como `ENABLED`.

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

Al seguir este tutorial, ha creado correctamente una directiva de uso de datos para una acción de marketing. Ahora puede continuar con el tutorial sobre [aplicación de políticas de uso de datos](../enforcement/api-enforcement.md) para aprender a comprobar las infracciones de políticas y manejarlas en su aplicación de experiencia.

Para obtener más información sobre las diferentes operaciones disponibles en la API [!DNL Policy Service], consulte la [Guía para desarrolladores del Servicio de políticas](../api/getting-started.md). Para obtener información sobre cómo aplicar directivas para datos [!DNL Real-time Customer Profile], consulte el tutorial sobre [aplicación del cumplimiento de normas de uso de datos para segmentos de audiencia](../../segmentation/tutorials/governance.md).

Para obtener información sobre cómo administrar las políticas de uso en la interfaz de usuario [!DNL Experience Platform], consulte la [guía del usuario de directivas](user-guide.md).
