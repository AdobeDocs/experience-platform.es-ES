---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Programaciones
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guía del programador de programadores de programadores

intro

- Recuperar una lista de programaciones
- Crear una nueva programación
- Recuperar una programación específica
- Actualizar una programación específica
- Eliminar una programación específica

## Primeros pasos

Los extremos de API que se utilizan en esta guía forman parte de la API de segmentación. Antes de continuar, consulte la guía para desarrolladores [de Segmentación](./getting-started.md).

En particular, la sección [de](./getting-started.md#getting-started) introducción de la guía para desarrolladores de Segmentación incluye vínculos a temas relacionados, una guía para leer las llamadas de la API de muestra en el documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas exitosas a cualquier API de la plataforma de experiencia.

## Recuperar una lista de programaciones

Puede recuperar una lista de todas las programaciones de su organización de IMS haciendo una solicitud GET al `/config/schedules` extremo.

**Formato API**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:: (*Opcional*) Se han agregado parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación.

**Parámetros de Consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para los programas de listado. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las programaciones disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `start` | Especifica de qué página se inicio el desplazamiento. De forma predeterminada, este valor será 0. |
| `limit` | Especifica el número de programas devueltos. De forma predeterminada, este valor será 100. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de programaciones para la organización de IMS especificada como JSON.

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Crear una nueva programación

Puede crear una nueva programación realizando una solicitud POST al `/config/schedules` extremo.

**Formato API**

```http
POST /config/schedules
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Parámetro | Descripción |
| --------- | ------------ |
| `name` | **Requerido.** El nombre de la programación como una cadena. |
| `type` | **Requerido.** Tipo de trabajo como cadena. Los dos tipos admitidos son `batch_segmentation` y `export`. |
| `properties` | **Requerido.** Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **Necesario cuando`type`es igual a`batch_segmentation`.** El uso `["*"]` garantiza la inclusión de todos los segmentos. |
| `schedule` | **Requerido.** Cadena que contiene la programación de trabajos. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. En este ejemplo, &quot;0 0 1 *&quot; significa que esta programación se ejecutará a medianoche el primero de cada mes. |
| `state` | *Opcional.* Una cadena que contiene el estado de programación. Los dos estados admitidos son `active` y `inactive`. De forma predeterminada, el estado se establece en `inactive`. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la programación recién creada.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Recuperar una programación específica

Puede recuperar información detallada sobre una programación específica realizando una solicitud GET al extremo y proporcionando el valor de la programación en la ruta de la solicitud `/config/schedules` y el valor `id` de la misma.

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:: El `id` valor de la programación que desea recuperar.

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la programación especificada.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## Actualizar detalles de una programación específica

Puede actualizar una programación especificada realizando una solicitud PATCH al extremo y proporcionando el valor de la programación en la ruta de acceso de la solicitud `/config/schedules` y el valor `id` de la misma.

La solicitud PATCH admite dos rutas diferentes: `/state` y `/schedule`.

### Actualizar estado de programación

Puede utilizar `/state` para actualizar el estado de la programación: ACTIVA o INACTIVA. Para actualizar el estado, deberá establecer el valor como `active` o `inactive`.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:: El `id` valor de la programación que desea actualizar.

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `path` | La ruta del valor que desea aplicar el parche. En este caso, como está actualizando el estado de la programación, debe establecer el valor de `path` en `/state`. |
| `value` | El valor actualizado del `/state`. Este valor se puede establecer como `active` o `inactive` para activar o desactivar la programación. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

### Actualizar programación cronológica

Puede usar `schedule` para actualizar la programación de cron. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:: El `id` valor de la programación que desea actualizar.

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `path` | La ruta del valor que desea aplicar el parche. En este caso, como está actualizando la programación cron de la programación, debe establecer el valor de `path` en `/schedule`. |
| `value` | El valor actualizado del `/state`. Este valor debe tener la forma de un cronograma de crones. En este ejemplo, la programación se ejecutará el segundo de cada mes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Eliminar una programación específica

Puede solicitar la eliminación de una programación especificada realizando una solicitud de ELIMINACIÓN al programa `/config/schedules` y proporcionando el valor de la programación `id` en la ruta de la solicitud.

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:: El `id` valor de la programación que desea eliminar.

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) con el siguiente mensaje:

```json
(No Content) Schedule deleted successfully
```

## Pasos siguientes
