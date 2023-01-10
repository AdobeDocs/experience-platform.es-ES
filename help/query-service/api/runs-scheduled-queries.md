---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;ejecutar consultas programadas;ejecutar consulta programada;servicio de consulta;consultas programadas;consulta programada;
solution: Experience Platform
title: La consulta programada ejecuta el extremo de la API
description: Las secciones siguientes recorren las distintas llamadas de API que puede realizar para ejecutar consultas programadas con la API del servicio de consulta.
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# El extremo de ejecución de la consulta programada

## Ejemplo de llamadas a API

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas al [!DNL Query Service] API. Las siguientes secciones explican las distintas llamadas a la API que puede realizar mediante el [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de todas las ejecuciones para una consulta programada especificada

Puede recuperar una lista de todas las ejecuciones para una consulta programada específica, independientemente de si se están ejecutando o ya se han completado. Para ello, realice una solicitud de GET al `/schedules/{SCHEDULE_ID}/runs` punto final, donde `{SCHEDULE_ID}` es la variable `id` de la consulta programada cuyas ejecuciones desea recuperar.

**Formato de API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada que desea recuperar. |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`). A continuación se enumeran los parámetros disponibles. |

**Parámetros de consulta**

La siguiente es una lista de parámetros de consulta disponibles para enumerar ejecuciones para una consulta programada especificada. Todos estos parámetros son opcionales. Si se realiza una llamada a este extremo sin parámetros, se recuperarán todas las ejecuciones disponibles para la consulta programada especificada.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo mediante el cual se deben solicitar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` clasificará los resultados por creación en orden ascendente. Adición de un `-` antes de crear (`orderby=-created`) ordenará los elementos creando en orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Desplaza la lista de respuestas utilizando la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista a partir de la tercera consulta de la lista. (*Valor predeterminado: 0*) |
| `property` | Filtre los resultados según los campos. Los filtros **must** se escapó el HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `state`y `externalTrigger`. La lista de operadores admitidos es `>` (bueno que) `<` (menor que) y  `==` (igual a) y `!=` (no es igual a). Por ejemplo, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` devolverá todas las ejecuciones que se hayan creado, creado y creado manualmente después del 20 de abril de 2019. |

**Solicitud**

La siguiente solicitud recupera las cuatro últimas ejecuciones para la consulta programada especificada.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de ejecuciones para la consulta programada especificada como JSON. La siguiente respuesta devuelve las cuatro últimas ejecuciones para la consulta programada especificada.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>Puede utilizar el valor de `_links.cancel` a [detener una ejecución para una consulta programada especificada](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Déclencheur inmediato de una ejecución para una consulta programada específica

Puede almacenar en déclencheur inmediatamente una ejecución para una consulta programada especificada realizando una solicitud de POST al `/schedules/{SCHEDULE_ID}/runs` punto final, donde `{SCHEDULE_ID}` es la variable `id` valor de la consulta programada cuya ejecución desea almacenar en déclencheur.

**Formato de API**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperar detalles de una ejecución para una consulta programada específica

Puede recuperar detalles sobre una ejecución para una consulta programada específica realizando una solicitud de GET al `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` y proporcionando el ID de la consulta programada y la ejecución en la ruta de solicitud.

**Formato de API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada cuya ejecución desea recuperar detalles de. |
| `{RUN_ID}` | La variable `id` de la ejecución que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la ejecución especificada.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Detener inmediatamente una ejecución para una consulta programada específica

Puede detener inmediatamente una ejecución para una consulta programada específica realizando una solicitud de PATCH al `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` y proporcionando el ID de la consulta programada y la ejecución en la ruta de solicitud.

**Formato de API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` de la consulta programada cuya ejecución desea recuperar detalles de. |
| `{RUN_ID}` | La variable `id` de la ejecución que desea recuperar. |

**Solicitud**

Esta solicitud de API utiliza la sintaxis JSON Patch para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de fundamentos de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
