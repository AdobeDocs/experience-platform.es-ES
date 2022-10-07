---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;alerta;
title: Punto final de la API de suscripciones de alertas
description: Esta guía proporciona ejemplos de solicitudes HTTP y respuestas para las distintas llamadas de API que puede realizar al extremo de suscripciones de alerta con la API del servicio de consulta.
hide: true
hidefromtoc: true
source-git-commit: df894d8b52aff3708aa06e73d4c5ba3e1e501f10
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 2%

---

# Punto final de la API de suscripciones de alertas

El servicio de consulta de Adobe Experience Platform le permite suscribirse a las alertas para consultas ad hoc y programadas. Las alertas se pueden recibir por correo electrónico, en la interfaz de usuario de Platform o en ambos. El contenido de la notificación es el mismo para las alertas en la plataforma y las alertas por correo electrónico. Actualmente, las alertas de consulta solo se pueden suscribir a mediante el uso de [API del servicio de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Para recibir alertas por correo electrónico, primero debe habilitar esta configuración dentro de la interfaz de usuario. Consulte la documentación para [instrucciones sobre cómo habilitar las alertas de correo electrónico](../../observability/alerts/ui.md#enable-email-alerts).

La tabla siguiente explica los tipos de alerta admitidos para diferentes tipos de consultas:

| Tipo de consulta | Tipos de alertas compatibles |
|---|---|
| Consultas ad hoc | `success` o `failed` ejecuciones. |
| Consultas programadas | `start`, `success`o `failed` ejecuciones. |

>[!NOTE]
>
>Todas las consultas que no sean SELECT admiten suscripciones de alerta y no es necesario que sea el creador de consultas para suscribirse a una alerta. Otros usuarios también pueden inscribirse para recibir alertas en una consulta que no hayan creado.

Las siguientes alertas se aplican sin una suscripción de alerta:

* Cuando finaliza un trabajo de consulta por lotes, los usuarios reciben una notificación.
* Cuando la duración de un trabajo de consulta por lotes supera un umbral, se activa una alerta para la persona que programó la consulta.

>[!NOTE]
>
>Las consultas utilizadas para las pruebas pueden excluirse de estas alertas si se han configurado correctamente.

## Ejemplo de llamadas a API

Las siguientes secciones explican las distintas llamadas de API que puede realizar mediante la API del servicio de consulta. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

## Recuperar una lista de todas las alertas de una organización y un simulador de pruebas {#get-list-of-org-alert-subs}

Recupere una lista de todas las alertas de un entorno limitado de una organización realizando una solicitud de GET al `/alert-subscriptions` punto final.

**Formato de API**

```http
GET /alert-subscriptions
```

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve un estado HTTP 200 y la variable `alerts` matriz con información de paginación y versión. La variable `alerts` matriz contiene detalles de todas las alertas de una organización y un entorno limitado concreto. Hay un máximo de tres alertas disponibles por respuesta; una alerta por cada tipo de alerta está incluida en el cuerpo de respuesta.

>[!NOTE]
>
>La variable `alerts._links` en el `alerts` se ha truncado para la brevedad. Un ejemplo completo de la variable `alerts._links` se puede encontrar en la variable [respuesta de la solicitud del POST](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `alerts.assetId` | El ID de consulta que asoció la alerta a una consulta en particular. |
| `alerts.id` | Nombre de la alerta. Este nombre lo genera el servicio Alerts y se utiliza en el panel Alerts . El nombre de la alerta está formado por la carpeta que almacena la alerta, la `alertType`y el ID de flujo. La información sobre las alertas disponibles se encuentra en la [Documentación del tablero de alertas de plataforma](../../observability/alerts/ui.md). |
| `alerts.status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`y `disabling`. Una alerta está escuchando activamente los eventos, pausada para uso futuro mientras conserva todos los suscriptores y la configuración relevantes, o bien realizando una transición entre estos estados. |
| `alerts.alertType` | Tipo de alerta. Hay tres valores posibles para una alerta: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `alerts._links` | Proporciona información sobre los métodos y extremos disponibles que se pueden usar para recuperar, actualizar, editar o eliminar información relacionada con este ID de alerta. |
| `_page` | El objeto contiene propiedades para describir el orden, el tamaño, el número total de páginas y la página actual. |
| `_links` | El objeto contiene referencias de URI que se pueden utilizar para obtener la página siguiente o anterior de los recursos. |

## Recuperar la información de suscripción de alerta para una consulta o ID de programación en particular {#retrieve-all-alert-subscriptions-by-id}

Recupere la información de suscripción de alerta para un ID de consulta o ID de programación concreto realizando una solicitud de GET al `/alert-subscriptions/{QUERY_ID}` o `/alert-subscriptions/{SCHEDULE_ID}` punto final.

**Formato de API**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{QUERY_ID}` | El ID de la consulta para la que desea devolver la información de suscripción. |
| `{SCHEDULE_ID}` | El ID de la consulta programada para la que desea devolver la información de suscripción. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve un estado HTTP de 200 y la variable `alerts` matriz que contiene información de suscripción para la consulta o el ID de programación proporcionados.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `assetId` | La alerta está asociada a este ID. El ID puede ser un ID de consulta o un ID de programación. |
| `id` | Nombre de la alerta. Este nombre lo genera el servicio Alerts y se utiliza en el panel Alerts . El nombre de la alerta está formado por la carpeta que almacena la alerta, la `alertType`y el ID de flujo. La información sobre las alertas disponibles se encuentra en la [Documentación del tablero de alertas de plataforma](../../observability/alerts/ui.md). |
| `status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`y `disabling`. Una alerta está escuchando activamente los eventos, pausada para uso futuro mientras conserva todos los suscriptores y la configuración relevantes, o bien realizando una transición entre estos estados. |
| `alertType` | Cada alerta puede tener tres tipos diferentes de alertas. Son: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions.emailNotifications` | Conjunto de direcciones de correo electrónico registradas de Adobe para los usuarios que se han suscrito a recibir correos electrónicos para la alerta. |
| `subscriptions.inContextNotifications` | Matriz de direcciones de correo electrónico registradas de Adobe para los usuarios que se han suscrito a las notificaciones de la interfaz de usuario para la alerta. |

## Recuperar información de suscripción de alerta para una consulta o ID de programación en particular y tipo de alerta {#get-alert-info-by-id-and-alert-type}

Recupere la información de suscripción de alerta para un ID y tipo de alerta específicos realizando una solicitud de GET al `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` punto final. Esto se aplica tanto a los ID de consulta como a los ID de consulta programados.

**Formato de API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `ALERT_TYPE` | Cada alerta puede tener tres tipos diferentes de alertas. Son: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `QUERY_ID` | Identificador único de la consulta que se va a actualizar. |
| `SCHEDULE_ID` | Identificador único de la consulta programada que se va a actualizar. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve un estado HTTP de 200 y todas las alertas suscritas. Esto incluye el ID de alerta, el tipo de alerta, los ID de correo electrónico registrados por el Adobe del suscriptor y su canal de notificación preferido.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `assetId` | El ID de consulta que asoció la alerta a una consulta en particular. |
| `alertType` | Tipo de alerta. Hay tres valores posibles para una alerta: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions` | Un objeto que se utiliza para pasar los ID de correo electrónico de Adobe registrados asociados a las alertas y los canales en los que los usuarios recibirán las alertas. |
| `subscriptions.inContextNotifications` | Matriz de direcciones de correo electrónico registradas de Adobe para los usuarios que se han suscrito a las notificaciones de la interfaz de usuario para la alerta. |
| `subscriptions.emailNotifications` | Conjunto de direcciones de correo electrónico registradas de Adobe para los usuarios que se han suscrito a recibir correos electrónicos para la alerta. |

## Recupere una lista de todas las alertas a las que está suscrito un usuario {#get-alert-subscription-list}

Recupere una lista de todas las alertas a las que está suscrito un usuario realizando una solicitud de GET al `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` punto final. La respuesta incluye el nombre de la alerta, los ID, el estado, el tipo de alerta y los canales de notificación.

**Formato de API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `{EMAIL_ID}` | Se utiliza una dirección de correo electrónico registrada en una cuenta de Adobe para identificar a los usuarios suscritos a las alertas. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 y la variable `items` matriz con detalles de las alertas suscritas por el `emailId` proporcionado.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la alerta. Este nombre lo genera el servicio Alerts y se utiliza en el panel Alerts . El nombre de la alerta está formado por la carpeta que almacena la alerta, la `alertType`y el ID de flujo. La información sobre las alertas disponibles se encuentra en la [Documentación del tablero de alertas de plataforma](../../observability/alerts/ui.md). |
| `assetId` | El ID de consulta que asoció la alerta a una consulta en particular. |
| `status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`y `disabling`. Una alerta está escuchando activamente los eventos, pausada para uso futuro mientras conserva todos los suscriptores y la configuración relevantes, o bien realizando una transición entre estos estados. |
| `alertType` | Tipo de alerta. Hay tres valores posibles para una alerta: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions` | Un objeto que se utiliza para pasar los ID de correo electrónico de Adobe registrados asociados a las alertas y los canales en los que los usuarios recibirán las alertas. |
| `subscriptions.inContextNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` confirma que las alertas deben proporcionarse a través de la interfaz de usuario. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |
| `subscriptions.emailNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` confirma que las alertas deben proporcionarse por correo electrónico. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |

## Crear una alerta y suscribir usuarios {#subscribe-users}

Para crear una alerta y suscribir a un usuario para recibirla, cree un `POST` solicitud al `/alert-subscriptions` punto final. Esta solicitud asocia una consulta a una alerta recién creada mediante una `assetId` y suscribe a los usuarios a las alertas para esa consulta mediante el uso de `emailIds`.

>[!IMPORTANT]
>
>Puede pasar hasta cinco ID de correo electrónico registrados en Adobe en una única solicitud. Para suscribir a más de cinco usuarios a una alerta, se deben realizar solicitudes posteriores.

**Formato de API**

```http
POST /alert-subscriptions
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `assetId` | La alerta está asociada a este ID. El ID puede ser un ID de consulta o un ID de programación. |
| `alertType` | Tipo de alerta. Hay tres valores posibles para una alerta: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions` | Un objeto que se utiliza para pasar los ID de correo electrónico de Adobe registrados asociados a las alertas y los canales en los que los usuarios recibirán las alertas. |
| `subscriptions.emailIds` | Matriz de direcciones de correo electrónico para identificar a los usuarios que deben recibir las alertas. Las direcciones de correo electrónico **must** se registrarán en una cuenta de Adobe. |
| `subscriptions.inContextNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` confirma que las alertas deben proporcionarse a través de la interfaz de usuario. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |
| `subscriptions.emailNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` confirma que las alertas deben proporcionarse por correo electrónico. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) con detalles de la alerta recién creada.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Nombre de la alerta. Este nombre lo genera el servicio Alerts y se utiliza en el panel Alerts . El nombre de la alerta está formado por la carpeta que almacena la alerta, la `alertType`y el ID de flujo. La información sobre las alertas disponibles se encuentra en la [Documentación del tablero de alertas de plataforma](../../observability/alerts/ui.md). |
| `_links` | Proporciona información sobre los métodos y extremos disponibles que se pueden usar para recuperar, actualizar, editar o eliminar información relacionada con este ID de alerta. |

## Habilitar o deshabilitar una alerta {#enable-or-disable-alert}

Esta solicitud hace referencia a una alerta concreta mediante un ID de consulta o programación y un tipo de alerta y actualiza el estado de alerta a `enable` o `disable`. Puede actualizar el estado de una alerta realizando una `PATCH` solicitud al `/alert-subscriptions/{queryId}/{alertType}` o `/alert-subscriptions/{scheduleId}/{alertType}` punto final.

**Formato de API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo de alerta. Hay tres valores posibles para una alerta: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul>Debe especificar el tipo de alerta actual en el área de nombres del extremo para cambiarlo. |
| `QUERY_ID` | Identificador único de la consulta que se va a actualizar. |
| `SCHEDULE_ID` | Identificador único de la consulta programada que se va a actualizar. |

**Solicitud**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `op` | La operación que se va a realizar. Actualmente, el único valor aceptado es `replace`. |
| `path` | Este valor está relacionado con el área de nombres en el extremo. Actualmente, el único valor aceptado es `/status`. |
| `value` | En una solicitud de PATCH correcta, esto cambia la variable `status` de la alerta. Actualmente, los valores aceptados son `enable` o `disable`. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del estado de alerta, tipo e ID, así como la consulta con la que se relaciona.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Nombre de la alerta. Este nombre lo genera el servicio Alerts y se utiliza en el panel Alerts . El nombre de la alerta está formado por la carpeta que almacena la alerta, la `alertType`y el ID de flujo. La información sobre las alertas disponibles se encuentra en la [Documentación del tablero de alertas de plataforma](../../observability/alerts/ui.md). |
| `assetId` | La alerta está asociada a este ID. El ID puede ser un ID de consulta o un ID de programación. |
| `alertType` | Cada alerta puede tener tres tipos diferentes de alertas. Son: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> |
| `status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`y `disabling`. Una alerta está escuchando activamente los eventos, pausada para uso futuro mientras conserva todos los suscriptores y la configuración relevantes, o bien realizando una transición entre estos estados. |

## Eliminar la alerta de una consulta en particular y un tipo de alerta {#delete-alert-info-by-id-and-alert-type}

Elimine una alerta para una consulta o ID de programación y un tipo de alerta concretos realizando una solicitud del DELETE al `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` o `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` punto final.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo de alerta. Hay tres valores posibles para una alerta: <ul><li>`start`: Notifica al usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: Notifica al usuario cuando la consulta se completa.</li><li>`failure`: Notifica al usuario si la consulta falla.</li></ul> La solicitud del DELETE solo se aplica al tipo de alerta específico proporcionado. |
| `QUERY_ID` | Identificador único de la consulta que se va a actualizar. |
| `SCHEDULE_ID` | Identificador único de la consulta programada que se va a actualizar. |

**Solicitud**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve un estado HTTP 200 y un mensaje de confirmación que incluye el ID del recurso y el tipo de alerta de la alerta eliminada.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Pasos siguientes

Esta guía abarcaba el uso de la variable `/alert-subscriptions` en la API del servicio de consulta. Después de leer esta guía, ahora tiene una mejor comprensión de cómo crear una alerta para una consulta, suscribir a los usuarios a la alerta, los tipos de alertas disponibles y cómo se puede recuperar, actualizar y eliminar la información de suscripción de alerta.

Consulte la [Guía de API del servicio de consulta](./getting-started.md) para obtener más información sobre otras funciones y operaciones disponibles.
