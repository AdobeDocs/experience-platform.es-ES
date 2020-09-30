---
keywords: Experience Platform;home;popular topics;query service;run scheduled queries;run scheduled query;Query service;scheduled queries;scheduled query;
solution: Experience Platform
title: Guía para desarrolladores de consulta Service
topic: runs for scheduled queries
description: Las siguientes secciones recorren las distintas llamadas de API que puede realizar para ejecutar consultas programadas con la API de servicio de Consulta.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---


# Ejecuta para consultas programadas

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la [!DNL Query Service] API. Las siguientes secciones explican las distintas llamadas de API que puede realizar con la [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de todas las ejecuciones para una consulta programada especificada

Puede recuperar una lista de todas las ejecuciones para una consulta programada específica, independientemente de si se están ejecutando o ya se han completado. Esto se realiza realizando una solicitud de GET al `/schedules/{SCHEDULE_ID}/runs` extremo, donde `{SCHEDULE_ID}` es el `id` valor de la consulta programada cuyas ejecuciones desea recuperar.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada que desea recuperar. |
| `{QUERY_PARAMETERS}` | (*Opcional*) Se han agregado parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar las ejecuciones de una consulta programada específica. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros se recuperarán todas las ejecuciones disponibles para la consulta programada especificada.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se ordenan los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` clasificará los resultados por creación en orden ascendente. Al añadir un `-` antes de crear (`orderby=-created`), los elementos se ordenarán en orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Default value: 20*) |
| `start` | Desplaza la lista de respuesta mediante la numeración basada en cero. Por ejemplo, `start=2` devolverá una lista a partir de la tercera consulta de la lista. (*Default value: 0*) |
| `property` | Filtre los resultados en función de los campos. Los filtros **deben** ser de escape HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `state`y `externalTrigger`. La lista de los operadores admitidos es `>` (buena que), `<` (menor que), y `==` (igual a), y `!=` (no igual a). Por ejemplo, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` devolverá todas las ejecuciones que se hayan creado, realizado correctamente y creado manualmente después del 20 de abril de 2019. |

**Solicitud**

La siguiente solicitud recupera las cuatro últimas ejecuciones de la consulta programada especificada.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de ejecuciones para la consulta programada especificada como JSON. La siguiente respuesta devuelve las cuatro últimas ejecuciones de la consulta programada especificada.

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
>Puede utilizar el valor de `_links.cancel` para [detener una ejecución para una consulta](#immediately-stop-a-run-for-a-specific-scheduled-query)programada específica.

### Activar inmediatamente una ejecución para una consulta programada específica

Puede activar inmediatamente una ejecución para una consulta programada especificada realizando una solicitud de POST al `/schedules/{SCHEDULE_ID}/runs` extremo, donde `{SCHEDULE_ID}` `id` es el valor de la consulta programada cuya ejecución desea activar.

**Formato API**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperar detalles de una ejecución para una consulta programada específica

Puede recuperar detalles sobre una ejecución para una consulta programada específica realizando una solicitud de GET al extremo y proporcionando el ID de la consulta programada y la ejecución en la ruta de la solicitud. `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada cuya ejecución desea recuperar los detalles. |
| `{RUN_ID}` | El `id` valor de la ejecución que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la ejecución especificada.

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

Puede detener inmediatamente una ejecución para una consulta programada específica haciendo una solicitud de PATCH al extremo y proporcionando tanto el ID de la consulta programada como la ejecución en la ruta de la solicitud. `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la consulta programada cuya ejecución desea recuperar los detalles. |
| `{RUN_ID}` | El `id` valor de la ejecución que desea recuperar. |

**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche JSON para su carga útil. Para obtener más información sobre cómo funciona JSON Patch, lea el documento de los principios fundamentales de API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con el siguiente mensaje.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
