---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;plantillas de consultas;guía de api;plantillas;servicio de consultas;
solution: Experience Platform
title: Punto final de API de plantillas de consulta
description: Esta guía detalla las distintas llamadas a la API de plantilla de consulta que puede realizar mediante la API del servicio de consultas.
role: Developer
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 3%

---

# Extremo de plantillas de consulta

## Llamadas de API de muestra

Las secciones siguientes describen las distintas llamadas de API que puede realizar mediante la API [!DNL Query Service]. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

Consulte la [documentación de plantillas de consulta de IU](../ui/query-templates.md) para obtener información sobre cómo crear plantillas a través de la interfaz de usuario del Experience Platform.

### Recuperación de una lista de plantillas de consulta

Puede recuperar una lista de todas las plantillas de consultas de su organización realizando una solicitud de GET al extremo `/query-templates`.

**Formato de API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por el símbolo et (`&`). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar las plantillas de consulta. Todos estos parámetros son opcionales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las plantillas de consulta disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se van a ordenar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` ordenará los resultados por orden de subida. Si se agrega un(a) `-` antes de crearlo (`orderby=-created`), los elementos se ordenarán por orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Especifique una marca de tiempo en formato ISO para ordenar los resultados. Si no se especifica ninguna fecha de inicio, la llamada de API devolverá primero las plantillas creadas más antiguas y, a continuación, seguirá enumerando los resultados más recientes.Las marcas de tiempo ISO <br> permiten diferentes niveles de granularidad en la fecha y la hora. Las marcas de tiempo ISO básicas tienen el formato de: `2020-09-07` para expresar la fecha 7 de septiembre de 2020. Un ejemplo más complejo se escribiría como `2022-11-05T08:15:30-05:00` y corresponde al 5 de noviembre de 2022, a las 8:15:30 a.m., hora estándar del este de EE.UU. Se puede proporcionar una zona horaria con un desplazamiento UTC y se indica con el sufijo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Si no se proporciona ninguna zona horaria, el valor predeterminado es cero. |
| `property` | Filtre los resultados según los campos. Los filtros **deben** ser de escape de HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `name` y `userId`. El único operador admitido es `==` (igual a). Por ejemplo, `name==my_template` devolverá todas las plantillas de consulta con el nombre `my_template`. |

**Solicitud**

La siguiente solicitud recupera la plantilla de consulta más reciente creada para su organización.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de plantillas de consulta para la organización especificada. La siguiente respuesta devuelve la plantilla de consulta más reciente creada para su organización.

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
>Puede usar el valor de `_links.delete` para [eliminar su plantilla de consulta](#delete-a-specified-query-template).

### Creación de una plantilla de consulta

Puede crear una plantilla de consulta realizando una solicitud de POST al extremo `/query-templates`.

**Formato de API**

```http
POST /query-templates
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sql` | La consulta SQL que desea crear. Puede utilizar SQL estándar o un reemplazo de parámetros. Para usar un reemplazo de parámetro en SQL, debe anteponer la clave de parámetro con un `$`. Por ejemplo, `$key` y proporcione los parámetros utilizados en SQL como pares de valor clave JSON en el campo `queryParameters`. Los valores pasados aquí son los parámetros predeterminados utilizados en la plantilla. Si desea anular estos parámetros, debe hacerlo en la solicitud del POST. |
| `name` | Nombre de la plantilla de consulta. |
| `queryParameters` | Un emparejamiento de valor clave para reemplazar cualquier valor parametrizado en la instrucción SQL. Solo es necesario **si** está usando reemplazos de parámetros dentro del SQL proporcionado. No se realizará ninguna comprobación de tipo de valor en estos pares de valor clave. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la plantilla de consulta recién creada.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
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
>Puede usar el valor de `_links.delete` para [eliminar su plantilla de consulta](#delete-a-specified-query-template).

### Recuperar una plantilla de consulta especificada

Puede recuperar una plantilla de consulta específica realizando una solicitud de GET al extremo `/query-templates/{TEMPLATE_ID}` y proporcionando el identificador de la plantilla en la ruta de solicitud.

**Formato de API**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Puede usar el valor de `_links.delete` para [eliminar su plantilla de consulta](#delete-a-specified-query-template).

### Actualizar una plantilla de consulta especificada

Puede actualizar una plantilla de consulta específica realizando una solicitud de PUT al extremo `/query-templates/{TEMPLATE_ID}` y proporcionando el identificador de la plantilla en la ruta de solicitud.

**Formato de API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TEMPLATE_ID}` | El valor `id` de la plantilla de consulta que desea recuperar. |

**Solicitud**

>[!NOTE]
>
>La solicitud del PUT requiere que se rellene el campo SQL y el campo de nombre, y **sobrescribirá** el contenido actual de esa plantilla de consulta.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sql` | La consulta SQL que desea crear. Puede utilizar SQL estándar o un reemplazo de parámetros. Para usar un reemplazo de parámetro en SQL, debe anteponer la clave de parámetro con un `$`. Por ejemplo, `$key` y proporcione los parámetros utilizados en SQL como pares de valor clave JSON en el campo `queryParameters`. Los valores pasados aquí son los parámetros predeterminados utilizados en la plantilla. Si desea anular estos parámetros, debe hacerlo en la solicitud del POST. |
| `name` | Nombre de la plantilla de consulta. |
| `queryParameters` | Un emparejamiento de valor clave para reemplazar cualquier valor parametrizado en la instrucción SQL. Solo es necesario **si** está usando reemplazos de parámetros dentro del SQL proporcionado. No se realizará ninguna comprobación de tipo de valor en estos pares de valor clave. |

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puede usar el valor de `_links.delete` para [eliminar su plantilla de consulta](#delete-a-specified-query-template).

### Eliminar una plantilla de consulta especificada

Puede eliminar una plantilla de consulta específica realizando una solicitud de DELETE a `/query-templates/{TEMPLATE_ID}` y proporcionando el identificador de la plantilla en la ruta de solicitud.

**Formato de API**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
