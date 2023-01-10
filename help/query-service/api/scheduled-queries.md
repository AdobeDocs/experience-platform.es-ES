---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consultas programadas;consulta programada;
solution: Experience Platform
title: Punto final de API de consultas programadas
description: Las secciones siguientes recorren las distintas llamadas de API que puede realizar para consultas programadas con la API del servicio de consulta.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 3%

---

# Punto final de consultas programadas

## Ejemplo de llamadas a API

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas al [!DNL Query Service] API. Las siguientes secciones explican las distintas llamadas a la API que puede realizar mediante el [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de consultas programadas

Puede recuperar una lista de todas las consultas programadas para su organización IMS realizando una solicitud de GET al `/schedules` punto final.

**Formato de API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`). A continuación se enumeran los parámetros disponibles. |

**Parámetros de consulta**

A continuación se muestra una lista de parámetros de consulta disponibles para enumerar consultas programadas. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las consultas programadas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo mediante el cual se deben solicitar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` clasificará los resultados por creación en orden ascendente. Adición de un `-` antes de crear (`orderby=-created`) ordenará los elementos creando en orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Desplaza la lista de respuestas utilizando la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista a partir de la tercera consulta de la lista. (*Valor predeterminado: 0*) |
| `property` | Filtre los resultados según los campos. Los filtros **must** se escapó el HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `templateId`y `userId`. La lista de operadores admitidos es `>` (bueno que) `<` (menor que) y `==` (igual a). Por ejemplo, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá todas las consultas programadas donde el ID de usuario sea el especificado. |

**Solicitud**

La siguiente solicitud recupera la última consulta programada creada para su organización IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de consultas programadas para la organización de IMS especificada. La siguiente respuesta devuelve la última consulta programada creada para su organización IMS.

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

Puede crear una nueva consulta programada realizando una solicitud de POST al `/schedules` punto final. Cuando crea una consulta programada en la API, también puede verla en el Editor de consultas. Para obtener más información sobre las consultas programadas en la interfaz de usuario, lea la [Documentación del Editor de consultas](../ui/user-guide.md#scheduled-queries).

**Formato de API**

```http
POST /schedules
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schedule.schedule` | La programación cron de la consulta. Para obtener más información sobre los programas de cron, lea la [formato de expresión cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentación. En este ejemplo, &quot;30 * * * *&quot; significa que la consulta se ejecutará cada hora con la marca de 30 minutos.<br><br>También puede utilizar las siguientes expresiones taquigráfica:<ul><li>`@once`: La consulta solo se ejecuta una vez.</li><li>`@hourly`: La consulta se ejecuta cada hora al principio de la hora. Esto equivale a la expresión cron `0 * * * *`.</li><li>`@daily`: La consulta se ejecuta una vez al día a medianoche. Esto equivale a la expresión cron `0 0 * * *`.</li><li>`@weekly`: La consulta se ejecuta una vez a la semana, el domingo, a medianoche. Esto equivale a la expresión cron `0 0 * * 0`.</li><li>`@monthly`: La consulta se ejecuta una vez al mes, el primer día del mes, a medianoche. Esto equivale a la expresión cron `0 0 1 * *`.</li><li>`@yearly`: La consulta se ejecuta una vez al año, el 1 de enero, a medianoche. Esto equivale a la expresión cron `1 0 0 1 1 *`. |
| `schedule.startDate` | La fecha de inicio de la consulta programada, escrita como una marca de tiempo UTC. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la consulta programada recién creada. Una vez que la consulta programada haya terminado de activarse, la variable `state` cambiará de `REGISTERING` a `ENABLED`.

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
>Puede utilizar el valor de `_links.delete` a [eliminar la consulta programada creada](#delete-a-specified-scheduled-query).

### Detalles de solicitud de una consulta programada especificada

Puede recuperar información para una consulta programada específica realizando una solicitud de GET al `/schedules` y proporcione su ID en la ruta de solicitud.

**Formato de API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Puede utilizar el valor de `_links.delete` a [eliminar la consulta programada creada](#delete-a-specified-scheduled-query).

### Actualizar detalles de una consulta programada especificada

Puede actualizar los detalles de una consulta programada especificada realizando una solicitud de PATCH al `/schedules` y proporcionando su ID en la ruta de solicitud.

La solicitud del PATCH admite dos rutas diferentes: `/state` y `/schedule/schedule`.

### Actualizar estado de consulta programada

Puede usar `/state` para actualizar el estado de la consulta programada seleccionada - ENABLED o DESHABILITADA. Para actualizar el estado, deberá establecer el valor como `enable` o `disable`.

**Formato de API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada que desea PATCH. |


**Solicitud**

Esta solicitud de API utiliza la sintaxis JSON Patch para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de fundamentos de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | La ruta del valor que desea parche. En este caso, dado que está actualizando el estado de la consulta programada, debe establecer el valor de `path` a `/state`. |
| `value` | El valor actualizado de la variable `/state`. Este valor puede establecerse como `enable` o `disable` para activar o desactivar la consulta programada. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Actualizar la programación de consultas programadas

Puede usar `/schedule/schedule` para actualizar la programación cron de la consulta programada. Para obtener más información sobre los programas de cron, lea la [formato de expresión cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentación.

**Formato de API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada que desea PATCH. |

**Solicitud**

Esta solicitud de API utiliza la sintaxis JSON Patch para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de fundamentos de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | La ruta del valor que desea parche. En este caso, dado que está actualizando la programación de la consulta programada, debe configurar el valor de `path` a `/schedule/schedule`. |
| `value` | El valor actualizado de la variable `/schedule`. Este valor debe presentar la forma de una programación cron. Por lo tanto, en este ejemplo, la consulta programada se ejecutará cada hora con la marca de 45 minutos. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Eliminar una consulta programada especificada

Puede eliminar una consulta programada especificada realizando una solicitud de DELETE al `/schedules` y proporcionando el ID de la consulta programada que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
>La programación **must** antes de eliminarse.

**Formato de API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada que desea DELETE. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
