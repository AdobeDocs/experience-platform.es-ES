---
keywords: Experience Platform;inicio;temas populares;administración de datos;política de uso de datos
solution: Experience Platform
title: Crear una directiva de uso de datos en la API
topic: policies
type: Tutorial
description: La API de servicio de directivas le permite crear y administrar políticas de uso de datos para determinar qué acciones de marketing se pueden realizar con datos que contienen ciertas etiquetas de uso de datos. Este documento proporciona un tutorial paso a paso para crear una política mediante la API de servicio de directivas.
translation-type: tm+mt
source-git-commit: 55a54463e918fc62378c660ef17f36e2ede471e0
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 2%

---


# Crear una directiva de uso de datos en la API

La [API de servicio de directivas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) permite crear y administrar políticas de uso de datos para determinar qué acciones de mercadotecnia se pueden realizar con datos que contienen ciertas etiquetas de uso de datos.

Este documento proporciona un tutorial paso a paso para crear una política mediante la API [!DNL Policy Service]. Para obtener una guía más completa de las distintas operaciones disponibles en la API, consulte la [guía para desarrolladores de servicios de políticas](../api/getting-started.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes conceptos clave relacionados con la creación y evaluación de políticas:

* [Administración](../home.md) de datos de Adobe Experience Platform: Marco mediante el cual se  [!DNL Platform] aplica el cumplimiento de la normativa de uso de datos.
   * [Etiquetas](../labels/overview.md) de uso de datos: Las etiquetas de uso de datos se aplican a los campos de datos XDM, especificando restricciones para acceder a los datos.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.
* [Simuladores](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que debe conocer a fin de realizar llamadas exitosas a la API [!DNL Policy Service], incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Definir una acción de mercadotecnia {#define-action}

En el entorno [!DNL Data Governance], una acción de mercadotecnia es una acción que realiza un [!DNL Experience Platform] consumidor de datos, para la cual es necesario verificar las violaciones de las políticas de uso de datos.

El primer paso para crear una política de uso de datos es determinar qué acción de mercadotecnia evaluará la política. Esto se puede realizar con una de las siguientes opciones:

* [Buscar una acción de mercadotecnia existente](#look-up)
* [Crear una nueva acción de mercadotecnia](#create-new)

### Buscar una acción de mercadotecnia existente {#look-up}

Puede buscar las acciones de marketing existentes que su directiva debe evaluar mediante una solicitud de GET a uno de los `/marketingActions` extremos.

**Formato API**

Dependiendo de si está buscando una acción de mercadotecnia proporcionada por [!DNL Experience Platform] o una acción de mercadotecnia personalizada creada por su organización, utilice los extremos `marketingActions/core` o `marketingActions/custom`, respectivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud utiliza el extremo `marketingActions/custom`, que obtiene una lista de todas las acciones de mercadotecnia definidas por la organización de IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el número total de acciones de mercadotecnia encontradas (`count`) y lista los detalles de las propias acciones de mercadotecnia dentro de la matriz `children`.

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
| `_links.self.href` | Cada elemento dentro de la matriz `children` contiene un identificador URI para la acción de mercadotecnia enumerada. |

Cuando encuentre la acción de mercadotecnia que desea utilizar, registre el valor de su propiedad `href`. Este valor se utiliza durante el siguiente paso de [creación de una directiva](#create-policy).

### Crear una nueva acción de mercadotecnia {#create-new}

Puede crear una nueva acción de mercadotecnia haciendo una solicitud de PUT al extremo `/marketingActions/custom/` y proporcionando un nombre para la acción de mercadotecnia al final de la ruta de solicitud.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la nueva acción de marketing que desea crear. Este nombre actúa como el identificador principal de la acción de marketing y, por lo tanto, debe ser único. Lo mejor es dar a la acción de mercadotecnia un nombre descriptivo pero conciso. |

**Solicitud**

La siguiente solicitud crea una nueva acción de marketing personalizada denominada &quot;exportToThirdParty&quot;. Observe que el `name` de la carga útil de la solicitud es el mismo que el nombre proporcionado en la ruta de la solicitud.

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

Registre el identificador URI de la acción de marketing recién creada, tal como se utilizará en el próximo paso de crear una política.

## Crear una directiva {#create-policy}

La creación de una nueva directiva requiere que proporcione el identificador URI de una acción de marketing con una expresión de las etiquetas de uso que prohíben esa acción de marketing.

Esta expresión se denomina expresión de directiva y es un objeto que contiene (A) una etiqueta o (B) un operador y operandos, pero no ambos. A su vez, cada operando es también un objeto de expresión de políticas. Por ejemplo, una política relativa a la exportación de datos a un tercero podría estar prohibida si están presentes etiquetas `C1 OR (C3 AND C7)`. Esta expresión se especificaría como:

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

Una vez configurada la expresión de directivas, puede crear una nueva directiva haciendo una solicitud de POST al extremo `/policies/custom`.

**Formato API**

```http
POST /policies/custom
```

**Solicitud**

La siguiente solicitud crea una directiva denominada &quot;Exportar datos a terceros&quot;, que proporciona una acción de marketing y una expresión de política en la carga útil de la solicitud.

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
| `marketingActionRefs` | Matriz que contiene el valor `href` de una acción de mercadotecnia, obtenido en el [paso anterior](#define-action). Aunque el ejemplo anterior lista una sola acción de marketing, también se pueden proporcionar varias acciones. |
| `deny` | El objeto de expresión de directivas. Define las etiquetas y condiciones de uso que harían que la directiva rechazara la acción de marketing a la que se hace referencia en `marketingActionRefs`. |

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
| `id` | Valor de sólo lectura generado por el sistema que identifica de forma exclusiva la política. |

Registre el identificador URI de la directiva recién creada, tal como se utiliza en el paso siguiente para habilitar la directiva.

## Habilitar la directiva

>[!NOTE]
>
>Aunque este paso es opcional si desea dejar la directiva en estado `DRAFT`, tenga en cuenta que, de manera predeterminada, una directiva debe tener su estado establecido en `ENABLED` para poder participar en la evaluación. Consulte la guía sobre [cumplimiento de políticas](../enforcement/api-enforcement.md) para obtener información sobre cómo hacer excepciones para políticas en estado `DRAFT`.

De forma predeterminada, las directivas que tienen su propiedad `status` establecida en `DRAFT` no participan en la evaluación. Puede habilitar la directiva para la evaluación realizando una solicitud de PATCH al extremo `/policies/custom/` y proporcionando el identificador único para la directiva al final de la ruta de la solicitud.

**Formato API**

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
| `op` | Tipo de operación de PATCH que se va a realizar. Esta solicitud realiza una operación de &quot;reemplazo&quot;. |
| `path` | Ruta al campo que se va a actualizar. Al habilitar una directiva, el valor debe establecerse en &quot;/status&quot;. |
| `value` | El nuevo valor que se asignará a la propiedad especificada en `path`. Esta solicitud establece la propiedad `status` de la directiva en &quot;ENABLED&quot;. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Aceptar) y los detalles de la directiva actualizada, con su `status` establecido ahora en `ENABLED`.

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

Siguiendo este tutorial, ha creado correctamente una directiva de uso de datos para una acción de marketing. Ahora puede continuar con el tutorial sobre [aplicación de políticas de uso de datos](../enforcement/api-enforcement.md) para aprender a comprobar si hay infracciones de políticas y manejarlas en la aplicación de experiencia.

Para obtener más información sobre las diferentes operaciones disponibles en la API [!DNL Policy Service], consulte la [Guía para desarrolladores de servicios de políticas](../api/getting-started.md). Para obtener información sobre cómo aplicar políticas para datos [!DNL Real-time Customer Profile], consulte el tutorial sobre [cumplimiento de normas de uso de datos para segmentos de audiencia](../../segmentation/tutorials/governance.md).

Para obtener información sobre cómo administrar las políticas de uso en la interfaz de usuario [!DNL Experience Platform], consulte la [guía del usuario de directivas](user-guide.md).