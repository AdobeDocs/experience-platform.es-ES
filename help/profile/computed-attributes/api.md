---
title: Punto final de API de atributos calculados
description: Obtenga información sobre cómo crear, ver, actualizar y eliminar atributos calculados mediante la API de perfil del cliente en tiempo real.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 49196473f304585193e87393f8dc5dc37be7e4d9
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 2%

---

# Extremo de API de atributos calculados

>[!IMPORTANT]
>
>El acceso a la API está restringido. Para obtener información sobre cómo obtener acceso a la API de atributos calculados, póngase en contacto con el Soporte técnico de Adobe.

Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Esta guía incluye llamadas de API de ejemplo para realizar operaciones básicas de CRUD usando el extremo `/attributes`.

Para obtener más información sobre los atributos calculados, comience por leer la [descripción general de los atributos calculados](overview.md).

## Introducción

El extremo de API usado en esta guía es parte de la [API del perfil del cliente en tiempo real](https://www.adobe.com/go/profile-apis-en).

Antes de continuar, revisa la [Guía de introducción a la API de perfil](../api/getting-started.md) para ver vínculos a la documentación recomendada, una guía para leer las llamadas de API de ejemplo que aparecen en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

Además, revise la documentación del siguiente servicio:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Guía de introducción al Registro de esquemas](../../xdm/api/getting-started.md#know-your-tenant_id): se proporciona información sobre su `{TENANT_ID}`, que aparece en las respuestas de esta guía.

## Recuperación de una lista de atributos calculados {#list}

Puede recuperar una lista de todos los atributos calculados para su organización realizando una solicitud de GET al extremo `/attributes`.

**Formato de API**

El extremo `/attributes` admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir la costosa sobrecarga al enumerar recursos. Si realiza una llamada a este extremo sin parámetros, se recuperarán todos los atributos calculados disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

Los siguientes parámetros de consulta se pueden utilizar al recuperar una lista de atributos calculados:

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `limit` | Un parámetro que especifica el número máximo de elementos devueltos como parte de la respuesta. El valor mínimo de este parámetro es 1 y el valor máximo es 40. Si este parámetro no se incluye, se devolverán 20 elementos de forma predeterminada. | `limit=20` |
| `offset` | Un parámetro que especifica el número de elementos que se omitirán antes de devolver los elementos. | `offset=5` |
| `sortBy` | Un parámetro que especifica el orden en que se ordenan los elementos devueltos. Las opciones disponibles son `name`, `status`, `updateEpoch` y `createEpoch`. También puede elegir si desea ordenar en orden ascendente o descendente si no incluye o incluye `-` delante de la opción de ordenación. De forma predeterminada, los elementos se ordenarán por `updateEpoch` en orden descendente. | `sortBy=name` |
| `property` | Un parámetro que permite filtrar varios campos de atributos calculados. Entre las propiedades admitidas se incluyen `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch` y `status`. Las operaciones admitidas dependen de la propiedad enumerada. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contiene()), `NOT_CONTAINS` (=!contiene())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contiene()), `NOT_CONTAINS` (=!contiene())</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contiene()), `NOT_CONTAINS` (=!contiene())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Solicitud**

La siguiente solicitud recupera los tres últimos atributos calculados que se actualizaron en su organización.

+++ Una solicitud de ejemplo para recuperar una lista de atributos calculados.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de los últimos 3 atributos calculados actualizados que pertenecen a su organización y a la zona protegida.

+++ Una respuesta de ejemplo para recuperar una lista de atributos calculados.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `_links` | Objeto que contiene la información de paginación necesaria para tener acceso a la última página de resultados, a la siguiente página de resultados, a la página de resultados anterior o a la página de resultados actual. |
| `computedAttributes` | Matriz que contiene los atributos calculados en función de los parámetros de consulta. Encontrará más información sobre la matriz de atributos calculados en la sección [recuperar un atributo calculado específico](#get). |
| `_page` | Objeto que contiene metadatos sobre los resultados devueltos. Esto incluye información sobre el desplazamiento actual, el recuento de atributos calculados devueltos, el recuento total de atributos calculados, así como el límite de atributos calculados devueltos. |

+++

## Creación de un atributo calculado {#create}

Para crear un atributo calculado, comience realizando una solicitud de POST al extremo `/attributes` con un cuerpo de solicitud que contenga los detalles del atributo calculado que desea crear.

**Formato de API**

```http
POST /attributes
```

**Solicitud**

+++ Una solicitud de ejemplo para crear un nuevo atributo calculado.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre del campo de atributo calculado, como cadena. El nombre del atributo calculado solo puede estar compuesto por caracteres alfanuméricos sin espacios ni guiones bajos. Este valor **debe** ser único entre todos los atributos calculados. Como práctica recomendada, este nombre debe ser una versión camelCase de `displayName`. |
| `description` | Una descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros usuarios de la organización a determinar el atributo calculado correcto que se debe utilizar. |
| `displayName` | El nombre para mostrar del atributo calculado. Este es el nombre que se mostrará al enumerar los atributos calculados en la interfaz de usuario de Adobe Experience Platform. |
| `expression` | Un objeto que representa la expresión de consulta del atributo calculado que intenta crear. |
| `expression.type` | Tipo de la expresión. Actualmente, solo se admite PQL. |
| `expression.format` | El formato de la expresión. Actualmente, solo se admite `pql/text`. |
| `expression.value` | El valor de la expresión. |
| `keepCurrent` | Un booleano que determina si el valor del atributo calculado se mantiene actualizado mediante una actualización rápida. Actualmente, este valor debe establecerse en `false`. |
| `duration` | Un objeto que representa el período retroactivo del atributo calculado. El periodo de retrospectiva representa hasta dónde se puede retroceder para calcular el atributo calculado. |
| `duration.count` | Un número que representa la duración del periodo de retroactividad. Los valores posibles dependen del valor del campo `duration.unit`. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | Cadena que representa la unidad de tiempo que se utilizará para el período retroactivo. Los valores posibles incluyen: `HOURS`, `DAYS`, `WEEKS` y `MONTHS`. |
| `status` | El estado del atributo calculado. Los valores posibles incluyen `DRAFT` y `NEW`. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el atributo calculado recién creado.

+++ Una respuesta de ejemplo al crear un nuevo atributo calculado.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El ID generado por el sistema del atributo calculado recién creado. |
| `status` | El estado del atributo calculado. Puede ser `DRAFT` o `NEW`. |
| `createEpoch` | Hora a la que se creó el atributo calculado, en segundos. |
| `updateEpoch` | Hora a la que se actualizó por última vez el atributo calculado, en segundos. |
| `createdBy` | El ID del usuario que creó el atributo calculado. |

+++

## Recuperación de un atributo calculado específico {#get}

Puede recuperar información detallada sobre un atributo calculado específico realizando una solicitud de GET al extremo `/attributes` y proporcionando el identificador del atributo calculado que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Solicitud**

+++ Una solicitud de ejemplo para recuperar un atributo calculado específico.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el atributo calculado especificado.

+++ Una respuesta de ejemplo al recuperar un atributo calculado específico.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | ID único, de solo lectura y generado por el sistema que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de la API. |
| `type` | Cadena que muestra que el objeto devuelto es un atributo calculado. |
| `name` | Nombre del atributo calculado. |
| `displayName` | El nombre para mostrar del atributo calculado. Este es el nombre que se mostrará al enumerar los atributos calculados en la interfaz de usuario de Adobe Experience Platform. |
| `description` | Una descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros usuarios de la organización a determinar el atributo calculado correcto que se debe utilizar. |
| `imsOrgId` | El ID de la organización a la que pertenece el atributo calculado. |
| `sandbox` | El objeto de zona protegida contiene detalles de la zona protegida en la que se configuró el atributo calculado. Esta información se obtiene del encabezado de la zona protegida enviado en la solicitud. Para obtener más información, consulte la [descripción general de las zonas protegidas](../../sandboxes/home.md). |
| `path` | El `path` al atributo calculado. |
| `keepCurrent` | Un booleano que determina si el valor del atributo calculado se mantiene actualizado mediante una actualización rápida. |
| `expression` | Un objeto que contiene la expresión del atributo calculado. |
| `mergeFunction` | Objeto que contiene la función de combinación para el atributo calculado. Este valor se basa en el parámetro de agregación correspondiente dentro de la expresión del atributo calculado. Los valores posibles incluyen `SUM`, `MIN`, `MAX` y `MOST_RECENT`. |
| `status` | El estado del atributo calculado. Puede ser uno de los siguientes valores: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` o `DISABLED`. |
| `schema` | Un objeto que contiene información sobre el esquema en el que se evalúa la expresión. Actualmente, solo se admite `_xdm.context.profile`. |
| `lastEvaluationTs` | Una marca de tiempo que representa cuándo se evaluó por última vez el atributo calculado. |
| `createEpoch` | Hora a la que se creó el atributo calculado, en segundos. |
| `updateEpoch` | Hora a la que se actualizó por última vez el atributo calculado, en segundos. |
| `createdBy` | El ID del usuario que creó el atributo calculado. |

+++

## Eliminar un atributo calculado específico {#delete}

Puede eliminar un atributo calculado específico realizando una solicitud de DELETE al extremo `/attributes` y proporcionando el identificador del atributo calculado que desea eliminar en la ruta de solicitud.

>[!IMPORTANT]
>
>La solicitud de eliminación solo se puede usar para eliminar atributos calculados que tengan el estado **borrador** (`DRAFT`). Este extremo **no se puede** usar para eliminar atributos calculados en ningún otro estado.

**Formato de API**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | El valor `id` del atributo calculado que desea eliminar. |

**Solicitud**

+++ Una solicitud de ejemplo para eliminar un atributo calculado.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 con detalles del atributo calculado eliminado.

+++ Una respuesta de ejemplo al eliminar un atributo calculado.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Actualización de un atributo calculado específico

Puede actualizar un atributo calculado específico realizando una solicitud de PATCH al extremo `/attributes` y proporcionando el identificador del atributo calculado que desea actualizar en la ruta de solicitud.

>[!IMPORTANT]
>
>Al actualizar un atributo calculado, solo se pueden actualizar los siguientes campos:
>
>- Si el estado actual es `NEW`, el estado solo se puede cambiar a `DISABLED`.
>- Si el estado actual es `DRAFT`, puede cambiar los valores de los campos siguientes: `name`, `description`, `keepCurrent`, `expression` y `duration`. También puede cambiar el estado de `DRAFT` a `NEW`. Cualquier cambio en los campos generados por el sistema, como `mergeFunction` o `path`, devolverá un error.
>- Si el estado actual es `PROCESSING` o `PROCESSED`, el estado solo se puede cambiar a `DISABLED`.

**Formato de API**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | El valor `id` del atributo calculado que desea actualizar. |

**Solicitud**

La siguiente solicitud actualizará el estado del atributo calculado de `DRAFT` a `NEW`.

+++ Una solicitud de ejemplo para actualizar un atributo calculado.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el atributo calculado recién actualizado.

+++ Una respuesta de ejemplo al actualizar un atributo calculado.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Pasos siguientes

Ahora que ha aprendido los conceptos básicos de los atributos calculados, está listo para empezar a definirlos para su organización. Para aprender a utilizar atributos calculados en la interfaz de usuario de Experience Platform, lea la [guía de la interfaz de usuario de atributos calculados](./ui.md).
