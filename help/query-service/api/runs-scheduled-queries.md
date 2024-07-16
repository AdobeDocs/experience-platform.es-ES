---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;ejecutar consultas programadas;ejecutar consulta programada;servicio de consultas;consultas programadas;consultas programadas;
solution: Experience Platform
title: La consulta programada ejecuta el extremo de API
description: En las siguientes secciones se describen las distintas llamadas a la API que puede realizar para ejecutar consultas programadas con la API del servicio de consultas.
role: Developer
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# Extremo de ejecuciones de consulta programadas

## Llamadas de API de muestra

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API [!DNL Query Service]. Las siguientes secciones describen las distintas llamadas a la API que puede realizar mediante la API [!DNL Query Service]. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Recuperar una lista de todas las ejecuciones de una consulta programada especificada

Puede recuperar una lista de todas las ejecuciones de una consulta programada específica, independientemente de si se están ejecutando actualmente o ya se han completado. Para ello, realice una solicitud de GET al extremo `/schedules/{SCHEDULE_ID}/runs`, donde `{SCHEDULE_ID}` es el valor `id` de la consulta programada cuyas ejecuciones desea recuperar.

**Formato de API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada que desea recuperar. |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por el símbolo et (`&`). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar las ejecuciones de una consulta programada especificada. Todos estos parámetros son opcionales. Realizar una llamada a este extremo sin parámetros recuperará todas las ejecuciones disponibles para la consulta programada especificada.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se van a ordenar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` ordenará los resultados por orden de subida. Si se agrega un(a) `-` antes de crearlo (`orderby=-created`), los elementos se ordenarán por orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Especifique una marca de tiempo en formato ISO para ordenar los resultados. Si no se especifica una fecha de inicio, la llamada de API devolverá primero las ejecuciones más antiguas y, a continuación, seguirá enumerando los resultados más recientes.<br> Las marcas de tiempo ISO permiten diferentes niveles de granularidad en la fecha y la hora. Las marcas de tiempo ISO básicas tienen el formato de: `2020-09-07` para expresar la fecha 7 de septiembre de 2020. Un ejemplo más complejo se escribiría como `2022-11-05T08:15:30-05:00` y corresponde al 5 de noviembre de 2022, a las 8:15:30 a.m., hora estándar del este de EE.UU. Se puede proporcionar una zona horaria con un desplazamiento UTC y se indica con el sufijo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Si no se proporciona ninguna zona horaria, el valor predeterminado es cero. |
| `property` | Filtre los resultados según los campos. Los filtros **deben** ser de escape de HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `state` y `externalTrigger`. La lista de operadores admitidos es `>` (mayor que), `<` (menor que), `==` (igual a) y `!=` (no igual a). Por ejemplo, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` devolverá todas las ejecuciones que se hayan creado, ejecutado correctamente y creado manualmente después del 20 de abril de 2019. |

**Solicitud**

La siguiente solicitud recupera las últimas cuatro ejecuciones para la consulta programada especificada.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de ejecuciones para la consulta programada especificada como JSON. La siguiente respuesta devuelve las últimas cuatro ejecuciones para la consulta programada especificada.

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
>Puede usar el valor de `_links.cancel` para [detener una ejecución de una consulta programada especificada](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Almacenar en déclencheur inmediatamente una ejecución para una consulta programada específica

Puede almacenar inmediatamente en déclencheur una ejecución para una consulta programada especificada realizando una solicitud de POST al extremo `/schedules/{SCHEDULE_ID}/runs`, donde `{SCHEDULE_ID}` es el valor `id` de la consulta programada cuya ejecución desea almacenar en déclencheur.

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

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperar detalles de una ejecución para una consulta programada específica

Puede recuperar detalles sobre una ejecución para una consulta programada específica realizando una solicitud de GET al extremo `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` y proporcionando tanto el ID de la consulta programada como la ejecución en la ruta de solicitud.

**Formato de API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada cuya ejecución desea recuperar detalles. |
| `{RUN_ID}` | El valor `id` de la ejecución que desea recuperar. |

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

Puede detener inmediatamente una ejecución para una consulta programada específica realizando una solicitud de PATCH al extremo `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` y proporcionando el ID de la consulta programada y la ejecución en la ruta de solicitud.

**Formato de API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada cuya ejecución desea recuperar detalles. |
| `{RUN_ID}` | El valor `id` de la ejecución que desea recuperar. |

**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche de JSON para su carga útil. Para obtener más información sobre cómo funciona el parche JSON, lea el documento de aspectos básicos de la API.

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

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
