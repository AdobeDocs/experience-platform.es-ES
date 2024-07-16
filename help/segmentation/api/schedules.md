---
solution: Experience Platform
title: Programa el extremo de API
description: Los programas son una herramienta que se puede utilizar para ejecutar automáticamente trabajos de segmentación por lotes una vez al día.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 3%

---

# Extremo de programaciones

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente trabajos de segmentación por lotes una vez al día. Puede usar el extremo `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

## Introducción

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de programaciones {#retrieve-list}

Puede recuperar una lista de todas las programaciones de su organización realizando una solicitud de GET al extremo `/config/schedules`.

**Formato de API**

El extremo `/config/schedules` admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las programaciones disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{START}` | Especifica desde qué página comenzará el desplazamiento. De forma predeterminada, este valor es 0. |
| `{LIMIT}` | Especifica el número de programaciones devueltas. De forma predeterminada, este valor es 100. |

**Solicitud**

La siguiente solicitud recupera las diez últimas programaciones publicadas en su organización.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de programaciones para la organización especificada como JSON.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y muestra solo la primera programación devuelta.

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
| `children.name` | Nombre de la programación en forma de cadena. |
| `children.type` | El tipo de trabajo como cadena. Los dos tipos admitidos son &quot;batch_segmentation&quot; y &quot;export&quot;. |
| `children.properties` | Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `children.properties.segments` | Usar `["*"]` garantiza que todos los segmentos se incluyan. |
| `children.schedule` | Cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para que se ejecuten una vez al día, lo que significa que no puede programar un trabajo para que se ejecute más de una vez durante un período de 24 horas. Para obtener más información acerca de las programaciones de cron, lea el apéndice del [formato de expresión cron](#appendix). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a la 1 a. m. todos los días. |
| `children.state` | Cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

## Crear una nueva programación {#create}

Puede crear una nueva programación realizando una solicitud de POST al extremo `/config/schedules`.

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
| `name` | **Requerido.** El nombre de la programación como una cadena. |
| `type` | **Requerido.**: tipo de trabajo como cadena. Los dos tipos admitidos son &quot;batch_segmentation&quot; y &quot;export&quot;. |
| `properties` | **Requerido.** Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **Requerido cuando `type` es igual a &quot;batch_segmentation&quot;.** al usar `["*"]` se asegura de que se incluyan todos los segmentos. |
| `schedule` | *Opcional.* Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para que se ejecuten una vez al día, lo que significa que no puede programar un trabajo para que se ejecute más de una vez durante un período de 24 horas. Para obtener más información acerca de las programaciones de cron, lea el apéndice del [formato de expresión cron](#appendix). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a la 1 a. m. todos los días. <br><br>Si no se proporciona esta cadena, se generará automáticamente una programación generada por el sistema. |
| `state` | *Opcional.* Una cadena que contiene el estado de programación. Los dos estados admitidos son &quot;activo&quot; e &quot;inactivo&quot;. De forma predeterminada, el estado se establece en &quot;inactivo&quot;. |

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
| `name` | Nombre de la programación en forma de cadena. |
| `type` | El tipo de trabajo como cadena. Los dos tipos compatibles son `batch_segmentation` y `export`. |
| `properties` | Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | Usar `["*"]` garantiza que todos los segmentos se incluyan. |
| `schedule` | Cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para que se ejecuten una vez al día, lo que significa que no puede programar un trabajo para que se ejecute más de una vez durante un período de 24 horas. Para obtener más información acerca de las programaciones de cron, lea el apéndice del [formato de expresión cron](#appendix). En este ejemplo, &quot;0 0 1 * *&quot; significa que esta programación se ejecutará a la 1 a. m. todos los días. |
| `state` | Cadena que contiene el estado de programación. Los dos estados admitidos son `active` y `inactive`. De manera predeterminada, el estado se establece en `inactive`. |

## Actualizar los detalles de una programación específica {#update}

Puede actualizar una programación específica realizando una solicitud de PATCH al extremo `/config/schedules` y proporcionando el ID de la programación que está intentando actualizar en la ruta de solicitud.

La solicitud del PATCH le permite actualizar el [estado](#update-state) o la [programación cron](#update-schedule) para una programación individual.

### Actualizar estado de programación {#update-state}

Puede utilizar una operación de parche JSON para actualizar el estado de la programación. Para actualizar el estado, declare la propiedad `path` como `/state` y establezca `value` como `active` o `inactive`. Para obtener más información sobre el parche JSON, lea la documentación de [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902).

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
| `path` | La ruta del valor al que desea aplicar el parche. En este caso, ya que está actualizando el estado de la programación, debe establecer el valor de `path` en &quot;/state&quot;. |
| `value` | El valor actualizado del estado de la programación. Este valor puede establecerse como &quot;activo&quot; o &quot;inactivo&quot; para activar o desactivar la programación. Tenga en cuenta que **no puede** deshabilitar una programación si la organización se ha habilitado para la transmisión por secuencias. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

### Actualizar programación de cron {#update-schedule}

Puede utilizar una operación de parche de JSON para actualizar la programación de cron. Para actualizar la programación, declare la propiedad `path` como `/schedule` y establezca `value` como una programación cron válida. Para obtener más información sobre el parche JSON, lea la documentación de [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902). Para obtener más información acerca de las programaciones de cron, lea el apéndice del [formato de expresión cron](#appendix).

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `path` | La ruta del valor que desea actualizar. En este caso, ya que está actualizando la programación de cron, debe establecer el valor de `path` en `/schedule`. |
| `value` | El valor actualizado de la programación de cron. Este valor debe estar en forma de programación cron. En este ejemplo, la programación se ejecutará el segundo de cada mes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Eliminar una programación específica

Puede solicitar que se elimine una programación específica realizando una solicitud de DELETE al extremo `/config/schedules` y proporcionando el identificador de la programación que desea eliminar en la ruta de solicitud.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido).

## Pasos siguientes

Después de leer esta guía, ahora tiene una mejor comprensión de cómo funcionan los horarios.

## Apéndice {#appendix}

En el siguiente apéndice se explica el formato de las expresiones cron utilizadas en las programaciones.

### Formato

Una expresión cron es una cadena que consta de 6 o 7 campos. La expresión tendría un aspecto similar al siguiente:

`0 0 12 * * ?`

En una cadena de expresión cron, el primer campo representa los segundos, el segundo campo representa los minutos, el tercer campo representa las horas, el cuarto campo representa el día del mes, el quinto campo representa el mes y el sexto campo representa el día de la semana. Si lo desea, también puede incluir un séptimo campo, que representa el año.

| Nombre del campo | Requerido | Valores posibles | Caracteres especiales permitidos |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Sí | 0-59 | `, - * /` |
| Minutes | Sí | 0-59 | `, - * /` |
| Horas | Sí | 0-23 | `, - * /` |
| Día del mes | Sí | 1-31 | `, - * ? / L W` |
| Mes | Sí | 1 A 12 DE ENERO A DICIEMBRE | `, - * /` |
| Día de la semana | Sí | 1-7, SUN-SAT | `, - * ? / L #` |
| Año | No | Vacío, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Los nombres de los meses y los nombres de los días de la semana **no** distinguen entre mayúsculas y minúsculas. Por lo tanto, `SUN` equivale a usar `sun`.

Los caracteres especiales permitidos representan los siguientes significados:

| Carácter especial | Descripción |
| ----------------- | ----------- |
| `*` | Este valor se usa para seleccionar **todos** los valores de un campo. Por ejemplo, poner `*` en el campo de horas significaría **cada** hora. |
| `?` | Este valor significa que no se requiere ningún valor específico. Esto se utiliza generalmente para especificar algo en un campo donde el carácter está permitido, pero no para especificarlo en el otro. Por ejemplo, si desea que un evento se active cada tres días del mes, pero no le importa qué día de la semana sea, debe colocar `3` en el campo día del mes y `?` en el campo día de la semana. |
| `-` | Este valor se usa para especificar **inclusivo** intervalos para el campo. Por ejemplo, si pone `9-15` en el campo de horas, significaría que las horas incluirían 9, 10, 11, 12, 13, 14 y 15. |
| `,` | Este valor se utiliza para especificar valores adicionales. Por ejemplo, si pone `MON, FRI, SAT` en el campo de día de la semana, significaría que los días de la semana incluirían lunes, viernes y sábado. |
| `/` | Este valor se utiliza para especificar incrementos. El valor colocado antes de `/` determina desde dónde se incrementa, mientras que el valor colocado después de `/` determina en qué medida se incrementa. Por ejemplo, si pone `1/7` en el campo de minutos, significaría que los minutos incluirían 1, 8, 15, 22, 29, 36, 43, 50 y 57. |
| `L` | Este valor se usa para especificar `Last` y tiene un significado diferente según el campo por el que lo use. Si se utiliza con el campo de día del mes, representa el último día del mes. Si se utiliza con el campo de día de la semana de forma independiente, representa el último día de la semana, que es sábado (`SAT`). Si se utiliza con el campo de día de la semana, junto con otro valor, representa el último día de ese tipo para el mes. Por ejemplo, si pone `5L` en el campo de día de la semana, **solo** incluirá el último viernes del mes. |
| `W` | Este valor se utiliza para especificar el día de semana más cercano al día determinado. Por ejemplo, si pone `18W` en el campo de día del mes y el día 18 de ese mes es sábado, entrará en déclencheur el viernes 17, que es el día más cercano entre semana. Si el 18 de ese mes fuera domingo, déclencheur el lunes 19, que es el día más cercano entre semana. Tenga en cuenta que si coloca `1W` en el campo de día del mes y el día de la semana más cercano sería el mes anterior, el evento seguirá en déclencheur el día de la semana más cercano del mes **actual**.</br></br>Además, puede combinar `L` y `W` para crear `LW`, lo que especificaría el último día de la semana del mes. |
| `#` | Este valor se utiliza para especificar el enésimo día de la semana de un mes. El valor colocado antes de `#` representa el día de la semana, mientras que el valor colocado después de `#` representa qué ocurrencia del mes es. Por ejemplo, si pone `1#3`, el evento generaría déclencheur el tercer domingo del mes. Tenga en cuenta que si coloca `X#5` y no hay quinta incidencia de ese día de la semana en ese mes, el evento **no** se activará. Por ejemplo, si pone `1#5` y no hay quinto domingo en ese mes, el evento **no** se activará. |

### Ejemplos

La siguiente tabla muestra cadenas de expresión cron de muestra y explica qué significan.

| Expresión | Explicación |
| ---------- | ----------- |
| `0 0 13 * * ?` | El evento se activará a la 1 p. m. todos los días. |
| `0 30 9 * * ? 2022` | El evento se activará todos los días a las 9:30 a. m. en el año 2022. |
| `0 * 18 * * ?` | El evento se activará cada minuto, empezando a las 6 PM y terminando a las 6:59 PM, todos los días. |
| `0 0/10 17 * * ?` | El evento se activará cada 10 minutos, comenzando a las 5 PM y terminando a las 6 PM, todos los días. |
| `0 13,38 5 ? 6 WED` | El evento se activará a las 5:13AM y a las 5:38AM todos los miércoles en junio. |
| `0 30 12 ? * 4#3` | El evento se activará a las 12:30 p.m. el tercer miércoles de cada mes. |
| `0 30 12 ? * 6L` | El evento se activará a las 12:30 p.m. del último viernes de cada mes. |
| `0 45 11 ? * MON-THU` | El evento se activará a las 11:45 a.m. todos los lunes, martes, miércoles y jueves. |