---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;plantillas de consulta;guía de api;plantillas;servicio de consulta;
solution: Experience Platform
title: Extremo de API de plantillas de consulta
topic-legacy: query templates
description: La siguiente documentación explica las distintas llamadas de API que puede realizar mediante plantillas de consulta para la API del servicio de consulta.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 5%

---

# Extremo de plantillas de consulta

## Ejemplo de llamadas a API

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas al [!DNL Query Service] API. Las siguientes secciones explican las distintas llamadas a la API que puede realizar mediante el [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de plantillas de consulta

Puede recuperar una lista de todas las plantillas de consulta para su organización IMS realizando una solicitud de GET al `/query-templates` punto final.

**Formato de API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`). A continuación se enumeran los parámetros disponibles. |

**Parámetros de consulta**

La siguiente es una lista de parámetros de consulta disponibles para listar plantillas de consulta. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las plantillas de consulta disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo mediante el cual se deben solicitar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` clasificará los resultados por creación en orden ascendente. Adición de un `-` antes de crear (`orderby=-created`) ordenará los elementos creando en orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Desplaza la lista de respuestas utilizando la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista a partir de la tercera consulta de la lista. (*Valor predeterminado: 0*) |
| `property` | Filtre los resultados según los campos. Los filtros **must** se escapó el HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `name` y `userId`. El único operador admitido es `==` (igual a). Por ejemplo, `name==my_template` devolverá todas las plantillas de consulta con el nombre `my_template`. |

**Solicitud**

La siguiente solicitud recupera la plantilla de consulta más reciente creada para su organización IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de plantillas de consulta para la organización IMS especificada. La siguiente respuesta devuelve la última plantilla de consulta creada para su organización IMS.

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
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
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
>Puede utilizar el valor de `_links.delete` a [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Creación de una plantilla de consulta

Puede crear una plantilla de consulta realizando una solicitud de POST al `/query-templates` punto final.

**Formato de API**

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
| `name` | El nombre de la plantilla de consulta. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la plantilla de consulta recién creada.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` a [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Recuperar una plantilla de consulta especificada

Puede recuperar una plantilla de consulta específica realizando una solicitud de GET al `/query-templates/{TEMPLATE_ID}` y proporcionando el ID de la plantilla de consulta en la ruta de solicitud.

**Formato de API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | La variable `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la plantilla de consulta especificada.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` a [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Actualizar una plantilla de consulta especificada

Puede actualizar una plantilla de consulta específica realizando una solicitud de PUT al `/query-templates/{TEMPLATE_ID}` y proporcionando el ID de la plantilla de consulta en la ruta de solicitud.

**Formato de API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TEMPLATE_ID}` | La variable `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

>[!NOTE]
>
>La solicitud del PUT requiere que se rellenen el campo sql y el campo name, y **sobrescribir** el contenido actual de esa plantilla de consulta.

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

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con la información actualizada para la plantilla de consulta especificada.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` a [eliminar la plantilla de consulta](#delete-a-specified-query-template).

### Eliminar una plantilla de consulta especificada

Puede eliminar una plantilla de consulta específica realizando una solicitud de DELETE al `/query-templates/{TEMPLATE_ID}` y proporcionando el ID de la plantilla de consulta en la ruta de solicitud.

**Formato de API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TEMPLATE_ID}` | La variable `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
