---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;guía de API;consultas;consulta;servicio de Consulta;
solution: Experience Platform
title: Extremo de la API de consultas
topic: queries
description: Las siguientes secciones explican las llamadas que puede realizar mediante el extremo /consultas de la API del servicio de Consulta.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 3%

---


# Extremo de consultas

## Ejemplos de llamadas a API

Las siguientes secciones explican las llamadas que puede realizar mediante el extremo `/queries` de la API [!DNL Query Service]. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de consultas

Puede recuperar una lista de todas las consultas para su organización de IMS haciendo una solicitud de GET al extremo `/queries`.

**Formato API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:: (*Opcional*) Se han agregado parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación.

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar consultas. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las consultas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se ordenan los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` ordenará los resultados por medio de la creación en orden ascendente. Al añadir un `-` antes de crear (`orderby=-created`) se ordenarán los elementos por orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Desplaza la lista de respuesta mediante la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista que comienza en la tercera consulta de la lista. (*Valor predeterminado: 0*) |
| `property` | Filtre los resultados en función de los campos. Los filtros **deben** ser de escape HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `updated`, `state` y `id`. La lista de los operadores admitidos es `>` (buena que), `<` (menor que), `>=` (buena o igual que), `<=` (menor o igual que), `==` (igual a), `!=` (no igual a) y `~` (contiene). Por ejemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá todas las consultas con el ID especificado. |
| `excludeSoftDeleted` | Indica si se debe incluir una consulta que se ha eliminado en forma suave. Por ejemplo, `excludeSoftDeleted=false` incluirá **consultas eliminadas en pantalla**. (*Valor predeterminado booleano: true*) |
| `excludeHidden` | Indica si se deben mostrar consultas no dirigidas por usuarios. Si este valor se establece en false, **incluirá** consultas no dirigidas por el usuario, como definiciones de CURSOR, FETCH o consultas de metadatos. (*Valor predeterminado booleano: true*) |

**Solicitud**

La siguiente solicitud recupera la consulta más reciente creada para su organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de consultas para la organización de IMS especificada como JSON. La siguiente respuesta devuelve la consulta más reciente creada para su organización de IMS.

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

### Cree una consulta

Puede crear una nueva consulta haciendo una solicitud de POST al extremo `/queries`.

**Formato API**

```http
POST /queries
```

**Solicitud**

La siguiente solicitud crea una nueva consulta, configurada por los valores proporcionados en la carga útil:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| Propiedad | Descripción |
| -------- | ----------- |
| `dbName` | Nombre de la base de datos para la que está creando una consulta SQL. |
| `sql` | La consulta SQL que desea crear. |
| `name` | Nombre de la consulta SQL. |
| `description` | Descripción de la consulta SQL. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con detalles de la consulta recién creada. Una vez que la consulta haya terminado de activarse y se haya ejecutado correctamente, el `state` cambiará de `SUBMITTED` a `SUCCESS`.

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
>Puede utilizar el valor de `_links.cancel` para [cancelar la consulta creada](#cancel-a-query).

### Recuperar una consulta por ID

Puede recuperar información detallada sobre una consulta específica haciendo una solicitud de GET al extremo `/queries` y proporcionando el valor `id` de la consulta en la ruta de la solicitud.

**Formato API**

```http
GET /queries/{QUERY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_ID}` | El valor `id` de la consulta que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>Puede utilizar el valor de `_links.cancel` para [cancelar la consulta creada](#cancel-a-query).

### Cancelar una consulta

Puede solicitar la eliminación de una consulta especificada realizando una solicitud de PATCH al extremo `/queries` y proporcionando el valor `id` de la consulta en la ruta de la solicitud.

**Formato API**

```http
PATCH /queries/{QUERY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_ID}` | El valor `id` de la consulta que desea cancelar. |


**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche JSON para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de los principios fundamentales de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `op` | Para cancelar la consulta, debe establecer el parámetro op con el valor `cancel `. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
