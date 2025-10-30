---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consultas programadas;consultas programadas;
solution: Experience Platform
title: Extremo de programaciones
description: En las siguientes secciones se describen las distintas llamadas a la API que puede realizar para consultas programadas con la API del servicio de consultas.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 2%

---

# Extremo de programaciones

Obtenga información sobre cómo crear, administrar y supervisar consultas programadas mediante programación mediante la API de programación del servicio de consultas con información detallada y ejemplos.

## Requisitos y requisitos previos

Puede crear consultas programadas mediante una cuenta técnica (autenticada mediante credenciales de servidor a servidor de OAuth) o una cuenta de usuario personal (token de usuario). Sin embargo, Adobe recomienda encarecidamente utilizar una cuenta técnica para garantizar la ejecución ininterrumpida y segura de consultas programadas, especialmente para cargas de trabajo de producción o a largo plazo.

Las consultas creadas con una cuenta de usuario personal fallarán si se revoca el acceso de ese usuario o se deshabilita su cuenta. Las cuentas técnicas proporcionan una mayor estabilidad porque no están vinculadas a la situación laboral o los derechos de acceso de un usuario individual.

>[!IMPORTANT]
>
>Consideraciones importantes al administrar consultas programadas:<ul><li>Las consultas programadas fallarán si la cuenta (técnica o de usuario) utilizada para crearlas pierde el acceso o los permisos.</li><li>Las consultas programadas deben desactivarse antes de eliminarse mediante la API o la interfaz de usuario.</li><li>No se admite la programación indefinida sin fecha de finalización; siempre se debe especificar una fecha de finalización.</li></ul>

Para obtener instrucciones detalladas sobre los requisitos de cuenta, la configuración de permisos y la administración de consultas programadas, consulte la [documentación de programaciones de consultas](../ui/query-schedules.md#technical-account-user-requirements). Para obtener instrucciones paso a paso sobre cómo crear y configurar una cuenta técnica, consulte [Configuración de Developer Console](https://experienceleague.adobe.com/es/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) y [Configuración de cuenta técnica de extremo a extremo](https://experienceleague.adobe.com/es/docs/platform-learn/tutorial-comprehensive-technical/setup).

## Llamadas de API de muestra

Una vez configurados los encabezados de autenticación necesarios (consulte la [guía de autenticación de API](../../landing/api-authentication.md)), puede empezar a realizar llamadas a la API [!DNL Query Service]. Las siguientes secciones muestran varias llamadas de API con formatos generales, solicitudes de ejemplo, incluidos los encabezados requeridos, y respuestas de ejemplo.

### Recuperación de una lista de consultas programadas

Puede recuperar una lista de todas las consultas programadas para su organización realizando una petición GET al extremo `/schedules`.

**Formato de API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parámetros agregados a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por el símbolo et (`&`). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar consultas programadas. Todos estos parámetros son opcionales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las consultas programadas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Especifica el campo por el que se van a ordenar los resultados. Los campos admitidos son `created` y `updated`. Por ejemplo, `orderby=created` ordenará los resultados por orden de subida. Si se agrega un(a) `-` antes de crearlo (`orderby=-created`), los elementos se ordenarán por orden descendente. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. (*Valor predeterminado: 20*) |
| `start` | Especifique una marca de tiempo en formato ISO para ordenar los resultados. Si no se especifica ninguna fecha de inicio, la llamada de API devolverá primero la consulta programada creada más antigua y, a continuación, seguirá enumerando los resultados más recientes.Las marcas de tiempo ISO <br> permiten diferentes niveles de granularidad en la fecha y la hora. Las marcas de tiempo ISO básicas tienen el formato de: `2020-09-07` para expresar la fecha 7 de septiembre de 2020. Un ejemplo más complejo se escribiría como `2022-11-05T08:15:30-05:00` y corresponde al 5 de noviembre de 2022, a las 8:15:30 a.m., hora estándar del este de EE.UU. Se puede proporcionar una zona horaria con un desplazamiento UTC y se indica con el sufijo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Si no se proporciona ninguna zona horaria, el valor predeterminado es cero. |
| `property` | Filtre los resultados según los campos. Los filtros **deben** ser de escape de HTML. Las comas se utilizan para combinar varios conjuntos de filtros. Los campos admitidos son `created`, `templateId` y `userId`. La lista de operadores admitidos es `>` (mayor que), `<` (menor que) y `==` (igual a). Por ejemplo, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá todas las consultas programadas en las que el identificador de usuario sea el especificado. |

**Solicitud**

La siguiente solicitud recupera la última consulta programada creada para su organización.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de consultas programadas para la organización especificada. La siguiente respuesta devuelve la consulta programada más reciente creada para su organización.

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

### Creación de una nueva consulta programada

Puede crear una nueva consulta programada realizando una petición POST al extremo `/schedules`. Cuando crea una consulta programada en la API, también puede verla en el Editor de consultas. Para obtener más información sobre consultas programadas en la interfaz de usuario, lea la [documentación del Editor de consultas](../ui/user-guide.md#scheduled-queries).

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
| `query.dbName` | Nombre de la base de datos donde se ejecutará la consulta programada. |
| `query.sql` | La consulta SQL que se ejecutará en la programación definida. |
| `query.name` | Nombre de la consulta programada. |
| `query.description` | Una descripción opcional para la consulta programada. |
| `schedule.schedule` | La programación cron para la consulta. Consulte [Crontab.guru](https://crontab.guru/) para ver una forma interactiva de crear, validar y comprender expresiones cron. En este ejemplo, &quot;`30 * * * *`&quot; significa que la consulta se ejecutará cada hora en la marca de 30 minutos.<br><br>Como alternativa, puede utilizar las siguientes expresiones abreviadas:<ul><li>`@once`: la consulta solo se ejecuta una vez.</li><li>`@hourly`: la consulta se ejecuta cada hora al comienzo de la hora. Esto equivale a la expresión cron `0 * * * *`.</li><li>`@daily`: la consulta se ejecuta una vez al día a medianoche. Esto equivale a la expresión cron `0 0 * * *`.</li><li>`@weekly`: la consulta se ejecuta una vez a la semana, el domingo a medianoche. Esto equivale a la expresión cron `0 0 * * 0`.</li><li>`@monthly`: la consulta se ejecuta una vez al mes, el primer día del mes, a medianoche. Esto equivale a la expresión cron `0 0 1 * *`.</li><li>`@yearly`: la consulta se ejecuta una vez al año, el 1 de enero a medianoche. Esto equivale a la expresión cron `0 0 1 1 *`. |
| `schedule.startDate` | La fecha de inicio de la consulta programada, escrita como marca de tiempo UTC. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la consulta programada recién creada. Una vez que la consulta programada haya terminado de activarse, `state` cambiará de `REGISTERING` a `ENABLED`.

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
>Puede usar el valor de `_links.delete` para [eliminar la consulta programada creada](#delete-a-specified-scheduled-query).

### Solicitar detalles de una consulta programada especificada

Puede recuperar información para una consulta programada específica realizando una petición GET al extremo `/schedules` y proporcionando su ID en la ruta de solicitud.

**Formato de API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada que desea recuperar. |

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
>Puede usar el valor de `_links.delete` para [eliminar la consulta programada creada](#delete-a-specified-scheduled-query).

### Actualizar los detalles de una consulta programada especificada

Puede actualizar los detalles de una consulta programada especificada realizando una petición PATCH al extremo `/schedules` y proporcionando su ID en la ruta de acceso de la solicitud.

La solicitud de PATCH admite dos rutas diferentes: `/state` y `/schedule/schedule`.

### Actualizar estado de consulta programada

Puede actualizar el estado de la consulta programada seleccionada estableciendo la propiedad `path` en `/state` y la propiedad `value` como `enable` o `disable`.

**Formato de API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada que desea enviar a PATCH. |


**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche de JSON para su carga útil. Para obtener más información sobre cómo funciona el parche JSON, lea el documento de aspectos básicos de la API.

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
| `op` | La operación que se va a realizar en la programación de consultas. El valor aceptado es `replace`. |
| `path` | La ruta del valor al que desea aplicar el parche. En este caso, ya que está actualizando el estado de la consulta programada, debe establecer el valor de `path` en `/state`. |
| `value` | El valor actualizado de `/state`. Este valor puede establecerse como `enable` o `disable` para habilitar o deshabilitar la consulta programada. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Actualizar programación de consultas programadas

Puede actualizar la programación cron de la consulta programada estableciendo la propiedad `path` en `/schedule/schedule` en el cuerpo de la solicitud. Para obtener más información sobre las programaciones de cron, lea la [documentación sobre el formato de las expresiones cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Formato de API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada que desea enviar a PATCH. |

**Solicitud**

Esta solicitud de API utiliza la sintaxis de parche de JSON para su carga útil. Para obtener más información sobre cómo funciona el parche JSON, lea el documento de aspectos básicos de la API.

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
| `op` | La operación que se va a realizar en la programación de consultas. El valor aceptado es `replace`. |
| `path` | La ruta del valor al que desea aplicar el parche. En este caso, ya que está actualizando la programación de la consulta programada, debe establecer el valor de `path` en `/schedule/schedule`. |
| `value` | El valor actualizado de `/schedule`. Este valor debe estar en forma de programación cron. Por lo tanto, en este ejemplo, la consulta programada se ejecutará cada hora en la marca de 45 minutos. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Eliminar una consulta programada especificada

Puede eliminar una consulta programada especificada realizando una petición DELETE al extremo `/schedules` y proporcionando el identificador de la consulta programada que desea eliminar en la ruta de acceso de la solicitud.

>[!NOTE]
>
>La programación **debe** deshabilitarse antes de eliminarse.

**Formato de API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la consulta programada que desea enviar a DELETE. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Accepted) con el siguiente mensaje.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
