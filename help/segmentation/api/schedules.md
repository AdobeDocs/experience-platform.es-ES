---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;programaciones;programación;api;API;
solution: Experience Platform
title: Punto final de API de programa
topic-legacy: developer guide
description: Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 3%

---

# Punto final de programación

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede utilizar el extremo `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de programaciones {#retrieve-list}

Puede recuperar una lista de todas las programaciones de su organización IMS realizando una solicitud de GET al extremo `/config/schedules` .

**Formato de API**

El extremo `/config/schedules` admite varios parámetros de consulta para ayudar a filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las programaciones disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo &quot;`&`&quot;.

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{START}` | Especifica de qué página comenzará el desplazamiento. De forma predeterminada, este valor es 0. |
| `{LIMIT}` | Especifica el número de programaciones devueltas. De forma predeterminada, este valor es 100. |

**Solicitud**

La siguiente solicitud recuperará las diez últimas programaciones publicadas en su organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de programaciones para la organización de IMS especificada como JSON.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y solo muestra la primera programación devuelta.

```json
{
    "_page": {
        "totalCount": 10,
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

| Propiedad | Descripción |
| -------- | ------------ |
| `_page.totalCount` | Número total de programaciones devueltas. |
| `_page.pageSize` | El tamaño de la página de programaciones. |
| `children.name` | Nombre de la programación como una cadena. |
| `children.type` | Tipo de trabajo como cadena. Los dos tipos admitidos son &quot;batch_segmentation&quot; y &quot;export&quot;. |
| `children.properties` | Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `children.properties.segments` | El uso de `["*"]` garantiza que se incluyan todos los segmentos. |
| `children.schedule` | Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. Para obtener más información sobre las programaciones de cron, lea la documentación de [formato de expresión cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a medianoche el primer día de cada mes. |
| `children.state` | Cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

## Crear una nueva programación {#create}

Puede crear una nueva programación realizando una solicitud de POST al extremo `/config/schedules` .

**Formato de API**

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
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Propiedad | Descripción |
| -------- | ------------ |
| `name` | **Requerido.** Nombre de la programación como una cadena. |
| `type` | **Requerido.** Tipo de trabajo como cadena. Los dos tipos admitidos son &quot;batch_segmentation&quot; y &quot;export&quot;. |
| `properties` | **Requerido.** Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **Necesario cuando  `type` es igual a &quot;batch_segmentation&quot;.** El uso de  `["*"]` garantiza que se incluyan todos los segmentos. |
| `schedule` | *Opcional.* Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. Para obtener más información sobre las programaciones de cron, lea la documentación de [formato de expresión cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a medianoche el primer día de cada mes. <br><br>Si no se proporciona esta cadena, se generará automáticamente una programación generada por el sistema. |
| `state` | *Opcional.* Cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

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

## Recuperar una programación específica {#get}

Puede recuperar información detallada sobre una programación específica realizando una solicitud de GET al extremo `/config/schedules` y proporcionando el ID de la programación que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la programación que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
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
}
```

| Propiedad | Descripción |
| -------- | ------------ |
| `name` | Nombre de la programación como una cadena. |
| `type` | Tipo de trabajo como cadena. Los dos tipos admitidos son `batch_segmentation` y `export`. |
| `properties` | Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | El uso de `["*"]` garantiza que se incluyan todos los segmentos. |
| `schedule` | Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. Para obtener más información sobre las programaciones de cron, lea la documentación de [formato de expresión cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a medianoche el primer día de cada mes. |
| `state` | Cadena que contiene el estado de programación. Los dos estados admitidos son `active` y `inactive`. De forma predeterminada, el estado se establece en `inactive`. |

## Actualización de detalles de una programación específica {#update}

Puede actualizar una programación específica realizando una solicitud de PATCH al extremo `/config/schedules` y proporcionando el ID de la programación que está intentando actualizar en la ruta de solicitud.

La solicitud del PATCH le permite actualizar el [estado](#update-state) o el [calendario cron](#update-schedule) para una programación individual.

### Actualizar estado de programación {#update-state}

Puede utilizar una operación de parche JSON para actualizar el estado de la programación. Para actualizar el estado, declare la propiedad `path` como `/state` y establezca el `value` como `active` o `inactive`. Para obtener más información sobre el parche JSON, lea la documentación de [JSON Patch](http://jsonpatch.com/).

**Formato de API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la programación que desea actualizar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `path` | La ruta del valor que desea parche. En este caso, dado que está actualizando el estado de la programación, debe establecer el valor de `path` en &quot;/state&quot;. |
| `value` | El valor actualizado del estado de la programación. Este valor se puede configurar como &quot;activo&quot; o &quot;inactivo&quot; para activar o desactivar la programación. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

### Actualizar la programación de cron {#update-schedule}

Puede utilizar una operación JSON Patch para actualizar la programación cron. Para actualizar la programación, declare la propiedad `path` como `/schedule` y establezca el `value` en una programación de cron válida. Para obtener más información sobre el parche JSON, lea la documentación de [JSON Patch](http://jsonpatch.com/). Para obtener más información sobre las programaciones de cron, lea la documentación de [formato de expresión cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Formato de API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la programación que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `path` | Ruta del valor que desea actualizar. En este caso, dado que está actualizando la programación cron, debe establecer el valor de `path` en `/schedule`. |
| `value` | El valor actualizado de la programación cron. Este valor debe presentar la forma de una programación cron. En este ejemplo, la programación se ejecutará el segundo de cada mes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Eliminar una programación específica

Puede solicitar la eliminación de una programación específica realizando una solicitud de DELETE al extremo `/config/schedules` y proporcionando el ID de la programación que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El valor `id` de la programación que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Pasos siguientes

Después de leer esta guía, ahora tiene una mejor comprensión de cómo funcionan los programas.
