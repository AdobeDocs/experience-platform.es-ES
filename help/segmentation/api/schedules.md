---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;programaciones;programación;api;API;
solution: Experience Platform
title: Punto final de API de programa
topic-legacy: developer guide
description: Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: 84026b447eea00955bc9e6482b81ae1aad3c312e
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 4%

---

# Punto final de programación

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede usar la variable `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

## Primeros pasos

Los extremos utilizados en esta guía forman parte del [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de programaciones {#retrieve-list}

Puede recuperar una lista de todas las programaciones de su organización realizando una solicitud de GET al `/config/schedules` punto final.

**Formato de API**

La variable `/config/schedules` el extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las programaciones disponibles para su organización. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`).

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

La siguiente solicitud recuperará las últimas diez programaciones publicadas en su organización.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
| `children.properties.segments` | Uso `["*"]` garantiza que se incluyan todos los segmentos. |
| `children.schedule` | Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. Para obtener más información sobre los programas cron, lea el apéndice de la [formato de expresión cron](#appendix). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a la 1 a. m. todos los días. |
| `children.state` | Cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

## Crear una nueva programación {#create}

Puede crear una nueva programación realizando una solicitud de POST al `/config/schedules` punto final.

**Formato de API**

```http
POST /config/schedules
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `properties.segments` | **Requerido cuando `type` es igual a &quot;batch_segmentation&quot;.** Uso `["*"]` garantiza que se incluyan todos los segmentos. |
| `schedule` | *Opcional.* Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. Para obtener más información sobre los programas cron, lea el apéndice de la [formato de expresión cron](#appendix). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a la 1 a. m. todos los días. <br><br>Si no se proporciona esta cadena, se generará automáticamente una programación generada por el sistema. |
| `state` | *Opcional.* Cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la programación recién creada.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

Puede recuperar información detallada sobre una programación específica realizando una solicitud de GET al `/config/schedules` y proporcionando el ID de la programación que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` del programa que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la programación especificada.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `type` | Tipo de trabajo como cadena. Los dos tipos compatibles son `batch_segmentation` y `export`. |
| `properties` | Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | Uso `["*"]` garantiza que se incluyan todos los segmentos. |
| `schedule` | Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. Para obtener más información sobre los programas cron, lea el apéndice de la [formato de expresión cron](#appendix). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a la 1 a. m. todos los días. |
| `state` | Cadena que contiene el estado de programación. Los dos estados admitidos son `active` y `inactive`. De forma predeterminada, el estado se establece en `inactive`. |

## Actualización de detalles de una programación específica {#update}

Puede actualizar una programación específica realizando una solicitud de PATCH al `/config/schedules` y proporcionando el ID de la programación que está intentando actualizar en la ruta de solicitud.

La solicitud del PATCH le permite actualizar cualquiera de los [state](#update-state) o [programación de cron](#update-schedule) para una programación individual.

### Actualizar el estado de la programación {#update-state}

Puede utilizar una operación de parche JSON para actualizar el estado de la programación. Para actualizar el estado, se declara la variable `path` property as `/state` y establezca la variable `value` para `active` o `inactive`. Para obtener más información sobre el parche JSON, lea la [Parche JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentación.

**Formato de API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` del programa que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | La ruta del valor que desea parche. En este caso, dado que está actualizando el estado de la programación, debe establecer el valor de `path` a &quot;/state&quot;. |
| `value` | El valor actualizado del estado de la programación. Este valor se puede configurar como &quot;activo&quot; o &quot;inactivo&quot; para activar o desactivar la programación. Tenga en cuenta que **cannot** deshabilite una programación si la organización IMS está habilitada para la transmisión. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

### Actualizar programación de cron {#update-schedule}

Puede utilizar una operación JSON Patch para actualizar la programación cron. Para actualizar la programación, declare la variable `path` property as `/schedule` y establezca la variable `value` a una programación de cron válida. Para obtener más información sobre el parche JSON, lea la [Parche JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentación. Para obtener más información sobre los programas cron, lea el apéndice de la [formato de expresión cron](#appendix).

**Formato de API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` del programa que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Ruta del valor que desea actualizar. En este caso, dado que está actualizando la programación cron, debe establecer el valor de `path` a `/schedule`. |
| `value` | El valor actualizado de la programación cron. Este valor debe presentar la forma de una programación cron. En este ejemplo, la programación se ejecutará el segundo de cada mes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Eliminar una programación específica

Puede solicitar la eliminación de una programación específica realizando una solicitud de DELETE al `/config/schedules` y proporcione el ID de la programación que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` del programa que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Pasos siguientes

Después de leer esta guía, ahora tiene una mejor comprensión de cómo funcionan los programas.

## Apéndice {#appendix}

El siguiente apéndice explica el formato de las expresiones cron utilizadas en las programaciones.

### Formato

Una expresión cron es una cadena formada por 6 o 7 campos. La expresión tendría un aspecto similar al siguiente:

`0 0 12 * * ?`

En una cadena de expresión cron, el primer campo representa los segundos, el segundo campo representa los minutos, el tercer campo representa las horas, el cuarto campo representa el día del mes, el quinto campo representa el mes y el sexto campo representa el día de la semana. También puede incluir un séptimo campo, que representa el año.

| Nombre del campo | Requerido | Valores posibles | Caracteres especiales permitidos |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Sí | 0-59 | `, - * /` |
| Minutes | Sí | 0-59 | `, - * /` |
| Horas | Sí | 0-23 | `, - * /` |
| Día del mes | Sí | 1-31 | `, - * ? / L W` |
| Mes | Sí | 1-12, ENERO-DEC | `, - * /` |
| Día de la semana | Sí | 1-7, SUN-SAT | `, - * ? / L #` |
| Año | No | Vacío, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Los nombres de los meses y los nombres de los días de la semana son **not** distingue entre mayúsculas y minúsculas. Por lo tanto, `SUN` equivale a usar `sun`.

Los caracteres especiales permitidos representan los siguientes significados:

| Carácter especial | Descripción |
| ----------------- | ----------- |
| `*` | Este valor se utiliza para seleccionar **all** valores de un campo. Por ejemplo, poner `*` en el campo horas significaría **every** hora. |
| `?` | Este valor significa que no se requiere ningún valor específico. Generalmente se utiliza para especificar algo en un campo en el que se permite el carácter, pero no para especificarlo en el otro. Por ejemplo, si desea que se active un evento cada tres meses del mes, pero no le importa qué día de la semana es, pondría `3` en el campo día del mes y `?` en el campo día de la semana . |
| `-` | Este valor se utiliza para especificar **inclusivo** rangos para el campo . Por ejemplo, si pone `9-15` en el campo horas, esto significaría que las horas incluirían 9, 10, 11, 12, 13, 14 y 15. |
| `,` | Este valor se utiliza para especificar valores adicionales. Por ejemplo, si pone `MON, FRI, SAT` en el campo día de la semana, esto significaría que los días de la semana incluirían lunes, viernes y sábado. |
| `/` | Este valor se utiliza para especificar incrementos. El valor colocado antes de la variable `/` determina desde dónde se incrementa, mientras que el valor se coloca después de la variable `/` determina en qué medida aumenta. Por ejemplo, si pone `1/7` en el campo de minutos, esto significaría que los minutos incluirían 1, 8, 15, 22, 29, 36, 43, 50 y 57. |
| `L` | Este valor se utiliza para especificar `Last`y tiene un significado diferente según el campo por el que lo utilice. Si se utiliza con el campo día del mes, representa el último día del mes. Si se utiliza con el campo día de la semana por sí solo, representa el último día de la semana, que es sábado (`SAT`). Si se utiliza con el campo día de la semana, junto con otro valor, representa el último día de ese tipo para el mes. Por ejemplo, si pone `5L` en el campo día de la semana, se **only** incluir el último viernes del mes. |
| `W` | Este valor se utiliza para especificar el día de la semana más cercano al día dado. Por ejemplo, si pone `18W` en el campo día del mes, y el día 18 de ese mes era sábado, se déclencheur el viernes 17, que es el día laboral más cercano. Si el 18 de ese mes fuera un domingo, sería un déclencheur el lunes 19, que es el día laboral más cercano. Tenga en cuenta que si pone `1W` en el campo día del mes y el día de la semana más cercano sería el mes anterior, el evento seguirá teniendo lugar en déclencheur el día de la semana más cercano del **current** mes.</br></br>Además, puede combinar `L` y `W` para `LW`, que especificaría el último día laborable del mes. |
| `#` | Este valor se utiliza para especificar el nésimo día de la semana de un mes. El valor colocado antes de la variable `#` representa el día de la semana, mientras que el valor colocado después de la variable `#` representa qué ocurrencia está ocurriendo en el mes en que está. Por ejemplo, si pone `1#3`, el evento se celebraría en déclencheur el tercer domingo del mes. Tenga en cuenta que si pone `X#5` y no hay una quinta incidencia de ese día de la semana en ese mes, el evento **not** se activará. Por ejemplo, si pone `1#5`, y no hay quinto domingo en ese mes, el evento **not** se activará. |

### Ejemplos

En la tabla siguiente se muestran las cadenas de expresión cron de ejemplo y se explica su significado.

| Expresión | Explicación |
| ---------- | ----------- |
| `0 0 13 * * ?` | El evento se activará a la 1 PM todos los días. |
| `0 30 9 * * ? 2022` | El evento se activará todos los días a las 9:30 AM del año 2022. |
| `0 * 18 * * ?` | El evento se activará cada minuto, a partir de las 6 p. m. y terminará a las 6:59 p. m. todos los días. |
| `0 0/10 17 * * ?` | El evento se activará cada 10 minutos, a partir de las 5 pm y terminará a las 6 pm, cada día. |
| `0 13,38 5 ? 6 WED` | El evento se activará a las 5:13 am y 5:38 am cada miércoles en junio. |
| `0 30 12 ? * 4#3` | El evento se activará cada mes a las 12:30 pm del tercer miércoles. |
| `0 30 12 ? * 6L` | El evento se activará a las 12:30 pm del último viernes de cada mes. |
| `0 45 11 ? * MON-THU` | El evento se activará a las 11:45 todos los lunes, martes, miércoles y jueves. |