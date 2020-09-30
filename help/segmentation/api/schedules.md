---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;schedules;schedule;api;API;
solution: Experience Platform
title: Programaciones
topic: developer guide
description: Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 3%

---


# Extremo de programación

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede utilizar el extremo para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica. `/config/schedules`

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte la guía [de](./getting-started.md) introducción para obtener información importante que debe conocer a fin de realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de programaciones {#retrieve-list}

Puede recuperar una lista de todas las programaciones de su organización de IMS realizando una solicitud de GET al `/config/schedules` extremo.

**Formato API**

El extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. `/config/schedules` Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las programaciones disponibles para su organización. Se pueden incluir varios parámetros, separados por ampersands (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{START}` | Especifica de qué página se inicio el desplazamiento. De forma predeterminada, este valor será 0. |
| `{LIMIT}` | Especifica el número de programas devueltos. De forma predeterminada, este valor será 100. |

**Solicitud**

La siguiente solicitud recuperará los diez últimos programas publicados en su organización de IMS.

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
>La siguiente respuesta se ha truncado para el espacio y muestra únicamente la primera programación devuelta.

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
| `children.name` | El nombre de la programación como una cadena. |
| `children.type` | Tipo de trabajo como cadena. Los dos tipos admitidos son &quot;batch_segmentation&quot; y &quot;export&quot;. |
| `children.properties` | Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `children.properties.segments` | El uso `["*"]` garantiza la inclusión de todos los segmentos. |
| `children.schedule` | Cadena que contiene la programación de trabajos. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar que se ejecute más de una vez durante un período de 24 horas. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. En este ejemplo, &quot;0 0 1 *&quot; significa que esta programación se ejecutará a medianoche el primero de cada mes. |
| `children.state` | Una cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

## Create a new schedule {#create}

Puede crear una nueva programación realizando una solicitud de POST al `/config/schedules` extremo.

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
| `name` | **Requerido.** El nombre de la programación como una cadena. |
| `type` | **Requerido.** Tipo de trabajo como cadena. Los dos tipos admitidos son &quot;batch_segmentation&quot; y &quot;export&quot;. |
| `properties` | **Requerido.** Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **Necesario cuando`type`es igual a &quot;batch_segmentation&quot;.** El uso `["*"]` garantiza la inclusión de todos los segmentos. |
| `schedule` | *Opcional.* Cadena que contiene la programación de trabajos. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar que se ejecute más de una vez durante un período de 24 horas. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. En este ejemplo, &quot;0 0 1 *&quot; significa que esta programación se ejecutará a medianoche el primero de cada mes. <br><br>Si no se proporciona esta cadena, se generará automáticamente una programación generada por el sistema. |
| `state` | *Opcional.* Una cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

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

Puede recuperar información detallada sobre una programación específica haciendo una solicitud de GET al extremo y proporcionando el ID de la programación que desea recuperar en la ruta de solicitud. `/config/schedules`

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la programación que desea recuperar. |

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
| `name` | El nombre de la programación como una cadena. |
| `type` | Tipo de trabajo como cadena. Los dos tipos admitidos son `batch_segmentation` y `export`. |
| `properties` | Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | El uso `["*"]` garantiza la inclusión de todos los segmentos. |
| `schedule` | Cadena que contiene la programación de trabajos. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar que se ejecute más de una vez durante un período de 24 horas. Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. En este ejemplo, &quot;0 0 1 *&quot; significa que esta programación se ejecutará a medianoche el primero de cada mes. |
| `state` | Una cadena que contiene el estado de programación. Los dos estados admitidos son `active` y `inactive`. By default, the state is set to `inactive`. |

## Actualizar detalles de una programación específica {#update}

Para actualizar una programación específica, realice una solicitud de PATCH al extremo y proporcione el ID de la programación que intenta actualizar en la ruta de la solicitud. `/config/schedules`

La solicitud de PATCH le permite actualizar el [estado](#update-state) o la programación [](#update-schedule) cron de una programación individual.

### Actualizar estado de programación {#update-state}

Puede utilizar una operación de parche JSON para actualizar el estado de la programación. Para actualizar el estado, se declara la `path` propiedad como `/state` y se establece el `value` como `active` o `inactive`. Para obtener más información sobre JSON Patch, lea la documentación de [JSON Patch](http://jsonpatch.com/) .

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la programación que desea actualizar. |

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
| `path` | La ruta del valor que desea aplicar el parche. En este caso, como está actualizando el estado de la programación, debe establecer el valor de `path` en &quot;/state&quot;. |
| `value` | Valor actualizado del estado de la programación. Este valor puede configurarse como &quot;activo&quot; o &quot;inactivo&quot; para activar o desactivar la programación. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

### Actualizar programación de cron {#update-schedule}

Puede utilizar una operación de parche JSON para actualizar la programación de cron. Para actualizar la programación, se declara la `path` propiedad como `/schedule` y se establece en una programación `value` cron válida. Para obtener más información sobre JSON Patch, lea la documentación de [JSON Patch](http://jsonpatch.com/) . Para obtener más información sobre los programas de cron, lea la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la programación que desea actualizar. |

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
| `path` | Ruta del valor que desea actualizar. En este caso, como está actualizando la programación de crones, debe establecer el valor de `path` en `/schedule`. |
| `value` | Valor actualizado de la programación de crones. Este valor debe tener la forma de un cronograma de crones. En este ejemplo, la programación se ejecutará el segundo de cada mes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Eliminar una programación específica

Para solicitar la eliminación de una programación específica, realice una solicitud de DELETE al extremo y proporcione el ID de la programación que desea eliminar en la ruta de la solicitud. `/config/schedules`

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | El `id` valor de la programación que desea eliminar. |

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

Después de leer esta guía, ahora podrá comprender mejor cómo funcionan los horarios.