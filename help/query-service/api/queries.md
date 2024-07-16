---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;guía de api;consultas;consulta;servicio de consultas;
solution: Experience Platform
title: Extremo de API de consultas
description: Las siguientes secciones describen las llamadas que puede realizar mediante el extremo /queries en la API del servicio de consultas.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 3%

---

# Extremo de consultas

## Llamadas de API de muestra

Las siguientes secciones describen las llamadas que puede realizar mediante el extremo `/queries` en la API [!DNL Query Service]. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperación de una lista de consultas

Puede recuperar una lista de todas las consultas de su organización realizando una solicitud de GET al extremo `/queries`.

**Formato de API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Se agregaron parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por el símbolo et (`&`). Los parámetros disponibles se enumeran a continuación.

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar consultas. Todos estos parámetros son opcionales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las consultas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se van a ordenar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` ordenará los resultados por orden de subida. Si se agrega un(a) `-` antes de crearlo (`orderby=-created`), los elementos se ordenarán por orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Especifique una marca de tiempo en formato ISO para ordenar los resultados. Si no se especifica ninguna fecha de inicio, la llamada de API devolverá primero la consulta creada más antigua y, a continuación, seguirá enumerando los resultados más recientes.Las marcas de tiempo ISO <br> permiten diferentes niveles de granularidad en la fecha y la hora. Las marcas de tiempo ISO básicas tienen el formato de: `2020-09-07` para expresar la fecha 7 de septiembre de 2020. Un ejemplo más complejo se escribiría como `2022-11-05T08:15:30-05:00` y corresponde al 5 de noviembre de 2022, a las 8:15:30 a.m., hora estándar del este de EE.UU. Se puede proporcionar una zona horaria con un desplazamiento UTC y se indica con el sufijo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Si no se proporciona ninguna zona horaria, el valor predeterminado es cero. |
| `property` | Filtre los resultados según los campos. Los filtros **deben** ser de escape de HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `updated`, `state` y `id`. La lista de operadores admitidos es `>` (mayor que), `<` (menor que), `>=` (mayor o igual que), `<=` (menor o igual que), `==` (igual a), `!=` (no igual a) y `~` (contiene). Por ejemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá todas las consultas con el identificador especificado. |
| `excludeSoftDeleted` | Indica si se debe incluir una consulta que se ha eliminado de forma suave. Por ejemplo, `excludeSoftDeleted=false` **incluirá** consultas eliminadas parcialmente. (*Booleano, valor predeterminado: true*) |
| `excludeHidden` | Indica si se deben mostrar consultas no dirigidas por el usuario. Si este valor se establece en false **se incluirán** consultas que no sean dirigidas por el usuario, como las consultas de definiciones de CURSOR, FETCH o de metadatos. (*Booleano, valor predeterminado: true*) |
| `isPrevLink` | El parámetro de consulta `isPrevLink` se usa para la paginación. Los resultados de la llamada de API se ordenan con la marca de tiempo `created` y la propiedad `orderby`. Al navegar por las páginas de resultados, `isPrevLink` se establece como verdadero al paginar hacia atrás. Invierte el orden de la consulta. Consulte los vínculos &quot;siguiente&quot; y &quot;anterior&quot; como ejemplos. |

**Solicitud**

La siguiente solicitud recupera la consulta más reciente creada para su organización.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de consultas para la organización especificada como JSON. La siguiente respuesta devuelve la consulta más reciente creada para su organización.

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

Puede crear una nueva consulta realizando una solicitud de POST al extremo `/queries`.

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
| `name` | Nombre de la consulta SQL. |
| `description` | La descripción de la consulta SQL. |
| `queryParameters` | Un emparejamiento de valor clave para reemplazar cualquier valor parametrizado en la instrucción SQL. Solo es necesario **si** está usando reemplazos de parámetros dentro del SQL proporcionado. No se realizará ninguna comprobación de tipo de valor en estos pares de valor clave. |
| `templateId` | El identificador único de una consulta preexistente. Puede proporcionar esto en lugar de una instrucción SQL. |
| `insertIntoParameters` | (Opcional) Si se define esta propiedad, esta consulta se convertirá en una consulta INSERT INTO. |
| `ctasParameters` | (Opcional) Si se define esta propiedad, esta consulta se convertirá en una consulta CTAS. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la consulta recién creada. Una vez que la consulta haya terminado de activarse y se haya ejecutado correctamente, `state` cambiará de `SUBMITTED` a `SUCCESS`.

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
>Puede usar el valor de `_links.cancel` para [cancelar la consulta creada](#cancel-a-query).

### Recuperación de una consulta por ID

Puede recuperar información detallada sobre una consulta específica realizando una solicitud de GET al extremo `/queries` y proporcionando el valor `id` de la consulta en la ruta de solicitud.

**Formato de API**

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
>Puede usar el valor de `_links.cancel` para [cancelar la consulta creada](#cancel-a-query).

### Cancelar o eliminar una consulta

Puede solicitar que se cancele o elimine de forma suave una consulta especificada realizando una solicitud de PATCH al extremo `/queries` y proporcionando el valor `id` de la consulta en la ruta de acceso de la solicitud.

**Formato de API**

```http
PATCH /queries/{QUERY_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{QUERY_ID}` | El valor `id` de la consulta en la que desea realizar la operación. |


**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche de JSON para su carga útil. Para obtener más información sobre cómo funciona el parche JSON, lea el documento de aspectos básicos de la API.

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
| `op` | Tipo de operación que se va a realizar en el recurso. Los valores aceptados son `cancel` y `soft_delete`. Para cancelar la consulta, debe establecer el parámetro op con el valor `cancel `. Tenga en cuenta que la operación de eliminación suave impide que se devuelva la consulta en solicitudes de GET, pero no la elimina del sistema. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
