---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;alerta;
title: Extremo de suscripciones de alerta
description: Esta guía proporciona solicitudes HTTP de ejemplo y respuestas para las distintas llamadas API que puede realizar al extremo de suscripciones de alerta con la API del servicio de consultas.
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 2%

---

# Extremo de suscripciones de alerta

El servicio de consultas de Adobe Experience Platform le permite suscribirse a alertas para consultas ad hoc y programadas. Las alertas se pueden recibir por correo electrónico, en la interfaz de usuario de Platform o en ambas. El contenido de notificación es el mismo para las alertas en la plataforma y las alertas por correo electrónico. Actualmente, las alertas de consulta solo se pueden suscribir a mediante el uso del [API del servicio de consultas](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Para recibir alertas por correo electrónico, primero debe habilitar esta configuración en la interfaz de usuario de. Consulte la documentación de [instrucciones sobre cómo habilitar las alertas por correo electrónico](../../observability/alerts/ui.md#enable-email-alerts).

En la tabla siguiente se explican los tipos de alerta admitidos para los distintos tipos de consultas:

| Tipo de consulta | Tipos de alerta admitidos |
|---|---|
| Consultas ad hoc | `success` o `failed` ejecuciones. |
| Consultas programadas | `start`, `success`, o `failed` ejecuciones. |

>[!NOTE]
>
>Todas las consultas que no son de SELECT admiten suscripciones de alerta y no es necesario que sea el creador de la consulta para suscribirse a una alerta. Otros usuarios también pueden inscribirse para recibir alertas en una consulta que no hayan creado.

Las siguientes alertas se aplican sin una suscripción de alerta:

* Cuando finaliza un trabajo de consulta por lotes, los usuarios reciben una notificación.
* Cuando la duración de un trabajo de consulta por lotes supera un umbral, se activa una alerta para la persona que programó la consulta.

>[!NOTE]
>
>Las consultas utilizadas para las pruebas se pueden excluir de estas alertas si se configuran correctamente.

## Llamadas de API de muestra

Las siguientes secciones describen las distintas llamadas a la API que puede realizar mediante la API del servicio de consultas. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

## Recuperación de una lista de todas las alertas de una organización y una zona protegida {#get-list-of-org-alert-subs}

Recupere una lista de todas las alertas de una zona protegida de la organización realizando una solicitud de GET a `/alert-subscriptions` punto final.

**Formato de API**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| Propiedad | Descripción |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | (Opcional) Parámetros añadidos a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;). Los parámetros disponibles se enumeran a continuación. |

**Parámetros de consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar consultas. Todos estos parámetros son opcionales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las consultas disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `orderby` | Campo que especifica el orden de los resultados. Los campos admitidos son `created` y `updated`. Anteponer el nombre de la propiedad con `+` para ascendente y `-` en orden descendente. El valor predeterminado es `-created`. Observe que el signo más (`+`) tiene que ser escapado con `%2B`. Por ejemplo `%2Bcreated` es el valor de un orden creado ascendente. |
| `pagesize` | Utilice este parámetro para controlar el número de registros que desea recuperar de la llamada de API por página. El límite predeterminado se establece en la cantidad máxima de 50 registros por página. |
| `page` | Indique el número de página de los resultados devueltos para los que desea ver los registros. |
| `property` | Filtre los resultados en función de los campos seleccionados. Los filtros **debe** ser HTML escapado. Las comas se utilizan para combinar varios conjuntos de filtros. Las siguientes propiedades permiten el filtrado: <ul><li>id</li><li>assetId</li><li>status</li><li>alertType</li></ul> Los operadores admitidos son `==` (igual a). Por ejemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá la alerta con un ID coincidente. |

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

Una respuesta correcta devuelve un estado HTTP 200 y la variable `alerts` matriz con información de paginación y versión. El `alerts` contiene detalles de todas las alertas de una organización y de una zona protegida concreta. Hay un máximo de tres alertas disponibles por respuesta; el cuerpo de la respuesta contiene una alerta por cada tipo de alerta.

>[!NOTE]
>
>El `alerts._links` objeto en el `alerts` La matriz se ha truncado para ser más breve. Un ejemplo completo de la `alerts._links` se puede encontrar en la [respuesta de la solicitud del POST](#subscribe-users).

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
| `alerts.assetId` | El ID de consulta que asoció la alerta con una consulta en particular. |
| `alerts.id` | El nombre de la alerta. Este nombre lo genera el servicio Alertas y se utiliza en el panel Alertas. El nombre de la alerta consta de la carpeta que almacena la alerta, la variable `alertType`y el ID de flujo. Encontrará información sobre las alertas disponibles en la [Documentación del panel Alertas de Platform](../../observability/alerts/ui.md). |
| `alerts.status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`, y `disabling`. Una alerta escucha activamente los eventos, se pone en pausa para un uso futuro mientras conserva todos los suscriptores y la configuración relevantes o realiza la transición entre estos estados. |
| `alerts.alertType` | El tipo de alerta. Existen tres valores potenciales para una alerta: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `alerts._links` | Proporciona información sobre los métodos y extremos disponibles que se pueden utilizar para recuperar, actualizar, editar o eliminar información relacionada con este ID de alerta. |
| `_page` | El objeto contiene propiedades para describir el orden, el tamaño, el número total de páginas y la página actual. |
| `_links` | El objeto contiene referencias de URI que pueden utilizarse para obtener la página siguiente o anterior de los recursos. |

## Recuperar la información de suscripción de alerta de una consulta o ID de programación determinados {#retrieve-all-alert-subscriptions-by-id}

Recupere la información de suscripción de alertas para un ID de consulta o ID de programación concreto realizando una solicitud de GET a `/alert-subscriptions/{QUERY_ID}` o el `/alert-subscriptions/{SCHEDULE_ID}` punto final.

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

Una respuesta correcta devuelve un estado HTTP de 200 y el `alerts` matriz que contiene información de suscripción para la consulta o el ID de programación proporcionados.

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
| `id` | El nombre de la alerta. Este nombre lo genera el servicio Alertas y se utiliza en el panel Alertas. El nombre de la alerta consta de la carpeta que almacena la alerta, la variable `alertType`y el ID de flujo. Encontrará información sobre las alertas disponibles en la [Documentación del panel Alertas de Platform](../../observability/alerts/ui.md). |
| `status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`, y `disabling`. Una alerta escucha activamente los eventos, se pone en pausa para un uso futuro mientras conserva todos los suscriptores y la configuración relevantes o realiza la transición entre estos estados. |
| `alertType` | Cada alerta puede tener tres tipos diferentes. Estos son: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions.emailNotifications` | Una matriz de direcciones de correo electrónico registradas de Adobe para los usuarios que se han suscrito para recibir correos electrónicos para la alerta. |
| `subscriptions.inContextNotifications` | Una matriz de direcciones de correo electrónico registradas en el Adobe para los usuarios que se han suscrito a las notificaciones de la interfaz de usuario para la alerta. |

## Recuperar información de suscripción de alerta para una consulta o ID de programación y tipo de alerta determinados {#get-alert-info-by-id-and-alert-type}

Recupere la información de suscripción de alerta para un ID y tipo de alerta en particular realizando una solicitud de GET a `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` punto final. Esto es aplicable tanto a las consultas como a los ID de consultas programadas.

**Formato de API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `ALERT_TYPE` | Esta propiedad describe el estado de ejecución de una déclencheur. La respuesta solo incluirá información de suscripción de alerta para alertas de este tipo. Cada alerta puede tener tres tipos diferentes. Estos son: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `QUERY_ID` | El identificador único de la consulta que se va a actualizar. |
| `SCHEDULE_ID` | El identificador único de la consulta programada que se va a actualizar. |

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

Una respuesta correcta devuelve un estado HTTP de 200 y todas las alertas a las que se ha suscrito. Esto incluye el ID de alerta, el tipo de alerta, los ID de correo electrónico registrado de Adobe del suscriptor y su canal de notificación preferido.

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
| `assetId` | El ID de consulta que asoció la alerta con una consulta en particular. |
| `alertType` | El tipo de alerta. Existen tres valores potenciales para una alerta: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions` | Un objeto utilizado para pasar los ID de correo electrónico registrados de Adobe asociados con las alertas y los canales en los que los usuarios recibirán las alertas. |
| `subscriptions.inContextNotifications` | Una matriz de direcciones de correo electrónico registradas en el Adobe para los usuarios que se han suscrito a las notificaciones de la interfaz de usuario para la alerta. |
| `subscriptions.emailNotifications` | Una matriz de direcciones de correo electrónico registradas de Adobe para los usuarios que se han suscrito para recibir correos electrónicos para la alerta. |

## Recuperar una lista de todas las alertas a las que está suscrito un usuario {#get-alert-subscription-list}

Recupere una lista de todas las alertas a las que está suscrito un usuario realizando una solicitud de GET al `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` punto final. La respuesta incluye el nombre de la alerta, los ID, el estado, el tipo de alerta y los canales de notificación.

**Formato de API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `{EMAIL_ID}` | Una dirección de correo electrónico registrada en una cuenta Adobe se utiliza para identificar a los usuarios suscritos a las alertas. |
| `orderby` | Campo que especifica el orden de los resultados. Los campos admitidos son `created` y `updated`. Anteponer el nombre de la propiedad con `+` para ascendente y `-` en orden descendente. El valor predeterminado es `-created`. Observe que el signo más (`+`) tiene que ser escapado con `%2B`. Por ejemplo `%2Bcreated` es el valor de un orden creado ascendente. |
| `pagesize` | Utilice este parámetro para controlar el número de registros que desea recuperar de la llamada de API por página. El límite predeterminado se establece en la cantidad máxima de 50 registros por página. |
| `page` | Indique el número de página de los resultados devueltos para los que desea ver los registros. |
| `property` | Filtre los resultados en función de los campos seleccionados. Los filtros **debe** ser HTML escapado. Las comas se utilizan para combinar varios conjuntos de filtros. Las siguientes propiedades permiten el filtrado: <ul><li>id</li><li>assetId</li><li>status</li><li>alertType</li></ul> Los operadores admitidos son `==` (igual a). Por ejemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` devolverá la alerta con un ID coincidente. |

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

Una respuesta correcta devuelve el estado HTTP 200 y la variable `items` matriz con detalles de las alertas a las que se ha suscrito el `emailId` siempre.

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
| `name` | El nombre de la alerta. Este nombre lo genera el servicio Alertas y se utiliza en el panel Alertas. El nombre de la alerta consta de la carpeta que almacena la alerta, la variable `alertType`y el ID de flujo. Encontrará información sobre las alertas disponibles en la [Documentación del panel Alertas de Platform](../../observability/alerts/ui.md). |
| `assetId` | El ID de consulta que asoció la alerta con una consulta en particular. |
| `status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`, y `disabling`. Una alerta escucha activamente los eventos, se pone en pausa para un uso futuro mientras conserva todos los suscriptores y la configuración relevantes o realiza la transición entre estos estados. |
| `alertType` | El tipo de alerta. Existen tres valores potenciales para una alerta: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions` | Un objeto utilizado para pasar los ID de correo electrónico registrados de Adobe asociados con las alertas y los canales en los que los usuarios recibirán las alertas. |
| `subscriptions.inContextNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` Este valor confirma que las alertas deben proporcionarse a través de la interfaz de usuario de. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |
| `subscriptions.emailNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` El valor de confirma que las alertas deben proporcionarse por correo electrónico. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |

## Creación de una alerta y suscripción de usuarios {#subscribe-users}

Para crear una alerta y suscribir a un usuario para recibirla, realice una `POST` solicitud a la `/alert-subscriptions` punto final. Esta solicitud asocia una consulta a una alerta recién creada mediante un `assetId` y suscribe a los usuarios a alertas para esa consulta mediante el uso de `emailIds`.

>[!IMPORTANT]
>
>Puede pasar hasta cinco ID de correo electrónico registrados de Adobe en una sola solicitud. Para suscribir a más de cinco usuarios a una alerta, se deben realizar solicitudes posteriores.

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
| `alertType` | El tipo de alerta. Existen tres valores potenciales para una alerta: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `subscriptions` | Un objeto utilizado para pasar los ID de correo electrónico registrados de Adobe asociados con las alertas y los canales en los que los usuarios recibirán las alertas. |
| `subscriptions.emailIds` | Una matriz de direcciones de correo electrónico para identificar a los usuarios que deben recibir las alertas. Las direcciones de correo electrónico **debe** estar registrado en una cuenta de Adobe. |
| `subscriptions.inContextNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` Este valor confirma que las alertas deben proporcionarse a través de la interfaz de usuario de. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |
| `subscriptions.emailNotifications` | Un valor booleano que determina cómo reciben los usuarios las notificaciones de alerta. A `true` El valor de confirma que las alertas deben proporcionarse por correo electrónico. A `false` garantiza que los usuarios no reciban notificaciones a través de ese canal. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) con detalles de la alerta recién creada.

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
| `id` | El nombre de la alerta. Este nombre lo genera el servicio Alertas y se utiliza en el panel Alertas. El nombre de la alerta consta de la carpeta que almacena la alerta, la variable `alertType`y el ID de flujo. Encontrará información sobre las alertas disponibles en la [Documentación del panel Alertas de Platform](../../observability/alerts/ui.md). |
| `_links` | Proporciona información sobre los métodos y extremos disponibles que se pueden utilizar para recuperar, actualizar, editar o eliminar información relacionada con este ID de alerta. |

## Habilitar o deshabilitar una alerta {#enable-or-disable-alert}

Esta solicitud hace referencia a una alerta concreta mediante una consulta o un ID de programación y un tipo de alerta, y actualiza el estado de alerta a `enable` o `disable`. Puede actualizar el estado de una alerta realizando una `PATCH` solicitud a la `/alert-subscriptions/{queryId}/{alertType}` o `/alert-subscriptions/{scheduleId}/{alertType}` punto final.

**Formato de API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `ALERT_TYPE` | El tipo de alerta. Existen tres valores potenciales para una alerta: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul>Debe especificar el tipo de alerta actual en el área de nombres de extremo para cambiarlo. |
| `QUERY_ID` | El identificador único de la consulta que se va a actualizar. |
| `SCHEDULE_ID` | El identificador único de la consulta programada que se va a actualizar. |

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
| `op` | Operación que se va a realizar. Actualmente, el único valor aceptado es `replace`. |
| `path` | Este valor está relacionado con el área de nombres del extremo. Actualmente, el único valor aceptado es `/status`. |
| `value` | En una solicitud de PATCH correcta, esto cambia el `status` valor de la alerta. Actualmente, los valores aceptados son `enable` o `disable`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del estado, el tipo y el ID de la alerta, así como la consulta a la que se relaciona.

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
| `id` | El nombre de la alerta. Este nombre lo genera el servicio Alertas y se utiliza en el panel Alertas. El nombre de la alerta consta de la carpeta que almacena la alerta, la variable `alertType`y el ID de flujo. Encontrará información sobre las alertas disponibles en la [Documentación del panel Alertas de Platform](../../observability/alerts/ui.md). |
| `assetId` | La alerta está asociada a este ID. El ID puede ser un ID de consulta o un ID de programación. |
| `alertType` | Cada alerta puede tener tres tipos diferentes. Estos son: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> |
| `status` | La alerta tiene cuatro valores de estado: `enabled`, `enabling`, `disabled`, y `disabling`. Una alerta escucha activamente los eventos, se pone en pausa para un uso futuro mientras conserva todos los suscriptores y la configuración relevantes o realiza la transición entre estos estados. |

## Eliminar la alerta de una consulta y un tipo de alerta determinados {#delete-alert-info-by-id-and-alert-type}

Eliminar una alerta para una consulta o ID de programación determinados y tipo de alerta realizando una solicitud de DELETE a la variable `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` o `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` punto final.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parámetros | Descripción |
| -------- | ----------- |
| `ALERT_TYPE` | El tipo de alerta. Existen tres valores potenciales para una alerta: <ul><li>`start`: notifica a un usuario cuando se ha iniciado la ejecución de la consulta.</li><li>`success`: notifica al usuario cuando se completa la consulta.</li><li>`failure`: notifica al usuario si la consulta falla.</li></ul> La solicitud del DELETE solo se aplica al tipo de alerta específico proporcionado. |
| `QUERY_ID` | El identificador único de la consulta que se va a actualizar. |
| `SCHEDULE_ID` | El identificador único de la consulta programada que se va a actualizar. |

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

Una respuesta correcta devuelve un estado HTTP 200 y un mensaje de confirmación que incluye el ID de recurso y el tipo de alerta de la alerta eliminada.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Pasos siguientes

Esta guía trata sobre el uso de `/alert-subscriptions` en la API del servicio de consultas. Después de leer esta guía, tiene una mejor comprensión de cómo crear una alerta para una consulta, suscribir a los usuarios a la alerta, los tipos de alertas disponibles y cómo se puede recuperar, actualizar y eliminar la información de suscripción de alerta.

Consulte la [Guía de API del servicio de consultas](./getting-started.md) para obtener más información sobre otras funciones y operaciones disponibles.
