---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;plantillas de consulta;guía de API;plantillas;servicio de Consulta;
solution: Experience Platform
title: Extremo de API de plantillas de consulta
topic: query templates
description: La siguiente documentación describe las distintas llamadas de API que puede realizar mediante plantillas de consulta para la API de servicio de Consulta.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---


# Extremo de plantillas de consulta

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la API [!DNL Query Service]. Las siguientes secciones explican las distintas llamadas de API que puede realizar mediante la API [!DNL Query Service]. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de plantillas de consulta

Puede recuperar una lista de todas las plantillas de consulta para su organización de IMS haciendo una solicitud de GET al extremo `/query-templates`.

**Formato API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Se agregaron parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar las plantillas de consulta. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las plantillas de consulta disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se ordenan los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` ordenará los resultados por medio de la creación en orden ascendente. Al añadir un `-` antes de crear (`orderby=-created`) se ordenarán los elementos por orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Desplaza la lista de respuesta mediante la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista que comienza en la tercera consulta de la lista. (*Valor predeterminado: 0*) |
| `property` | Filtre los resultados en función de los campos. Los filtros **deben** ser de escape HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `name` y `userId`. El único operador admitido es `==` (igual a). Por ejemplo, `name==my_template` devolverá todas las plantillas de consulta con el nombre `my_template`. |

**Solicitud**

La siguiente solicitud recupera la plantilla de consulta más reciente creada para su organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de plantillas de consulta para la organización de IMS especificada. La siguiente respuesta devuelve la plantilla de consulta más reciente creada para su organización de IMS.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` para [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Creación de una plantilla de consulta

Puede crear una plantilla de consulta haciendo una solicitud de POST al extremo `/query-templates`.

**Formato API**

```http
POST /query-templates
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sql` | La consulta SQL que desea crear. |
| `name` | Nombre de la plantilla de consulta. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con los detalles de la plantilla de consulta recién creada.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` para [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Recuperar una plantilla de consulta especificada

Puede recuperar una plantilla de consulta específica realizando una solicitud de GET al extremo `/query-templates/{TEMPLATE_ID}` y proporcionando el ID de la plantilla de consulta en la ruta de la solicitud.

**Formato API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | El valor `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la plantilla de consulta especificada.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` para [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Actualizar una plantilla de consulta especificada

Puede actualizar una plantilla de consulta específica realizando una solicitud de PUT al extremo `/query-templates/{TEMPLATE_ID}` y proporcionando el ID de la plantilla de consulta en la ruta de la solicitud.

**Formato API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TEMPLATE_ID}` | El valor `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

>[!NOTE]
>
>La solicitud de PUT requiere que se rellenen tanto el campo sql como el campo name, y **sobrescribirá** el contenido actual de esa plantilla de consulta.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sql` | La consulta SQL que desea actualizar. |
| `name` | Nombre de la consulta programada. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con la información actualizada de la plantilla de consulta especificada.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` para [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Eliminar una plantilla de consulta específica

Puede eliminar una plantilla de consulta específica haciendo una solicitud de DELETE a `/query-templates/{TEMPLATE_ID}` y proporcionando el ID de la plantilla de consulta en la ruta de la solicitud.

**Formato API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TEMPLATE_ID}` | El valor `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
