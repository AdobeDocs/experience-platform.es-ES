---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;guía de api;consultas;consulta;servicio de consulta;
solution: Experience Platform
title: Punto final de API de consultas
description: Las secciones siguientes recorren las llamadas que puede realizar utilizando el extremo /queries en la API del servicio de consulta.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 08e19149a84273231c6261d2a4e09584dfb6e38d
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 3%

---

# Extremo de consultas

## Llamadas de API de muestra

Las secciones siguientes recorren las llamadas que puede realizar mediante el `/queries` en la variable [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de consultas

Puede recuperar una lista de todas las consultas de su organización IMS realizando una solicitud de GET al `/queries` punto final.

**Formato de API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`). A continuación se enumeran los parámetros disponibles.

**Parámetros de consulta**

A continuación se muestra una lista de parámetros de consulta disponibles para enumerar consultas. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las consultas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo mediante el cual se deben solicitar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` clasificará los resultados por creación en orden ascendente. Adición de un `-` antes de crear (`orderby=-created`) ordenará los elementos creando en orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Desplaza la lista de respuestas utilizando la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista a partir de la tercera consulta de la lista. (*Valor predeterminado: 0*) |
| `property` | Filtre los resultados según los campos. Los filtros **must** se escapó el HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `updated`, `state`y `id`. La lista de operadores admitidos es `>` (bueno que) `<` (menor que), `>=` (bueno o igual que), `<=` (menor o igual que), `==` (igual a), `!=` (no es igual a) y `~` (contiene). Por ejemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá todas las consultas con el ID especificado. |
| `excludeSoftDeleted` | Indica si se debe incluir una consulta que se ha eliminado de forma suave. Por ejemplo, `excludeSoftDeleted=false` will **include** consultas eliminadas de software. (*Booleano, valor predeterminado: true*) |
| `excludeHidden` | Indica si se deben mostrar consultas no dirigidas por el usuario. Si este valor se establece en &quot;false&quot;, se obtendrá **include** consultas no dirigidas por el usuario, como definiciones de CURSOR, FETCH o consultas de metadatos. (*Booleano, valor predeterminado: true*) |
| `isPrevLink` | La variable `isPrevLink` el parámetro de consulta se utiliza para la paginación. Los resultados de la llamada a la API se ordenan mediante sus `created` marca de tiempo y `orderby` propiedad. Al navegar por las páginas de resultados, `isPrevLink` se establece en true al volver a la página. Revierte el orden de la consulta. Consulte los vínculos &quot;next&quot; y &quot;prev&quot; como ejemplos. |

**Solicitud**

La siguiente solicitud recupera la consulta más reciente creada para su organización IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de consultas para la organización de IMS especificada como JSON. La siguiente respuesta devuelve la consulta más reciente creada para su organización IMS.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Creación de una consulta

Puede crear una nueva consulta realizando una solicitud de POST al `/queries` punto final.

**Formato de API**

```http
POST /queries
```

**Solicitud**

La siguiente solicitud crea una nueva consulta, con una instrucción SQL proporcionada en la carga útil:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

El ejemplo de solicitud siguiente crea una nueva consulta utilizando un ID de plantilla de consulta existente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Propiedad | Descripción |
| -------- | ----------- |
| `dbName` | Nombre de la base de datos para la que está creando una consulta SQL. |
| `sql` | La consulta SQL que desea crear. |
| `name` | El nombre de la consulta SQL. |
| `description` | La descripción de la consulta SQL. |
| `queryParameters` | Enlace de valor clave para reemplazar cualquier valor parametrizado en la instrucción SQL. Solo es obligatorio **if** está utilizando reemplazos de parámetros dentro del SQL proporcionado. No se realizará ninguna comprobación del tipo de valor en estos pares de valor clave. |
| `templateId` | Identificador único de una consulta preexistente. Puede proporcionarlo en lugar de una instrucción SQL. |
| `insertIntoParameters` | (Opcional) Si esta propiedad está definida, esta consulta se convertirá en una consulta INSERT INTO . |
| `ctasParameters` | (Opcional) Si esta propiedad está definida, esta consulta se convertirá en una consulta CTAS. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la consulta recién creada. Una vez que la consulta ha terminado de activarse y se ha ejecutado correctamente, la variable `state` cambiará de `SUBMITTED` a `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.cancel` a [cancelar la consulta creada](#cancel-a-query).

### Recuperar una consulta por ID

Puede recuperar información detallada sobre una consulta específica realizando una solicitud de GET al `/queries` y proporcionando el `id` en la ruta de solicitud.

**Formato de API**

```http
GET /queries/{QUERY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_ID}` | La variable `id` de la consulta que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la consulta especificada.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.cancel` a [cancelar la consulta creada](#cancel-a-query).

### Cancelar o eliminar en blanco una consulta

Puede solicitar la cancelación o eliminación suave de una consulta especificada realizando una solicitud de PATCH al `/queries` y proporcionando el `id` en la ruta de solicitud.

**Formato de API**

```http
PATCH /queries/{QUERY_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{QUERY_ID}` | La variable `id` de la consulta en la que desea realizar la operación. |


**Solicitud**

Esta solicitud de API utiliza la sintaxis JSON Patch para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de fundamentos de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `op` | Tipo de operación que se realizará en el recurso. Los valores aceptados son `cancel` y `soft_delete`. Para cancelar la consulta, debe establecer el parámetro op con el valor `cancel `. Tenga en cuenta que la operación de eliminación suave impide que la consulta se devuelva en las solicitudes de GET, pero no la elimina del sistema. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
