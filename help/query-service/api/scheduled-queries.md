---
keywords: Experience Platform;home;popular topics;query service;Query service;scheduled queries;scheduled query;
solution: Experience Platform
title: Guía para desarrolladores de consulta Service
topic: scheduled queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 3%

---


# Consultas programadas

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la [!DNL Query Service] API. Las siguientes secciones explican las distintas llamadas de API que puede realizar con la [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de consultas programadas

Puede recuperar una lista de todas las consultas programadas para su organización de IMS realizando una solicitud de GET al `/schedules` extremo.

**Formato API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Se han agregado parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar consultas programadas. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las consultas programadas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se ordenan los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` clasificará los resultados por creación en orden ascendente. Al añadir un `-` antes de crear (`orderby=-created`), los elementos se ordenarán en orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Default value: 20*) |
| `start` | Desplaza la lista de respuesta mediante la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista a partir de la tercera consulta de la lista. (*Default value: 0*) |
| `property` | Filtre los resultados en función de los campos. Los filtros **deben** ser de escape HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `templateId`y `userId`. La lista de los operadores admitidos es `>` (buena que), `<` (menor que) y `==` (igual a). Por ejemplo, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá todas las consultas programadas en las que el ID de usuario sea el especificado. |

**Solicitud**

La siguiente solicitud recupera la última consulta programada creada para su organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de consultas programadas para la organización de IMS especificada. La siguiente respuesta devuelve la última consulta programada creada para su organización de IMS.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Crear una nueva consulta programada

Puede crear una nueva consulta programada realizando una solicitud de POST al `/schedules` extremo.

**Formato API**

```http
POST /schedules
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Propiedad | Descripción |
| -------- | ----------- |
| `query.dbName` | Nombre de la base de datos para la que está creando una consulta programada. |
| `query.sql` | La consulta SQL que desea crear. |
| `query.name` | Nombre de la consulta programada. |
| `schedule.schedule` | El cronograma de crones para la consulta. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. En este ejemplo, &quot;30 * * * *&quot; significa que la consulta se ejecutará cada hora con la marca de 30 minutos. |
| `schedule.startDate` | La fecha de inicio de la consulta programada, escrita como una marca de hora UTC. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con detalles de la consulta programada recién creada. Una vez que la consulta programada haya terminado de activarse, la variable `state` cambiará de `REGISTERING` a `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` para [eliminar la consulta](#delete-a-specified-scheduled-query)programada creada.

### Solicitar detalles de una consulta programada específica

Puede recuperar información de una consulta programada específica realizando una solicitud de GET al extremo y proporcionando su ID en la ruta de la solicitud. `/schedules`

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la consulta programada especificada.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.delete` para [eliminar la consulta](#delete-a-specified-scheduled-query)programada creada.

### Actualizar detalles de una consulta programada específica

Puede actualizar los detalles de una consulta programada específica realizando una solicitud de PATCH al extremo y proporcionando su ID en la ruta de la solicitud `/schedules` .

La solicitud de PATCH admite dos rutas diferentes: `/state` y `/schedule/schedule`.

### Actualizar estado de consulta programado

Puede usar `/state` para actualizar el estado de la consulta programada seleccionada: HABILITADA o DESHABILITADA. Para actualizar el estado, deberá establecer el valor como `enable` o `disable`.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada que desea recuperar. |


**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche JSON para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de los principios fundamentales de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `path` | La ruta del valor que desea aplicar el parche. En este caso, como está actualizando el estado de la consulta programada, debe establecer el valor de `path` en `/state`. |
| `value` | El valor actualizado del `/state`. Este valor se puede establecer como `enable` o `disable` para habilitar o deshabilitar la consulta programada. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Actualizar programación de consultas programadas

Puede usar `/schedule/schedule` para actualizar la programación cron de la consulta programada. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada que desea recuperar. |

**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche JSON para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de los principios fundamentales de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `path` | La ruta del valor que desea aplicar el parche. En este caso, como está actualizando la programación de la consulta programada, debe establecer el valor de `path` en `/schedule/schedule`. |
| `value` | El valor actualizado del `/schedule`. Este valor debe tener la forma de un cronograma de crones. Así, en este ejemplo, la consulta programada se ejecutará cada hora con la marca de 45 minutos. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Eliminar una consulta programada especificada

Puede eliminar una consulta programada especificada realizando una solicitud de DELETE al extremo y proporcionando el ID de la consulta programada que desea eliminar en la ruta de la solicitud. `/schedules`

>[!NOTE]
>
>La programación **debe** deshabilitarse antes de eliminarse.

**Formato API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada que desea recuperar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
