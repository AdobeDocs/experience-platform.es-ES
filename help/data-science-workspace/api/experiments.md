---
keywords: Experience Platform;guía para desarrolladores;extremo;Workspace de ciencia de datos;temas populares;experimentos;api de aprendizaje automático de sensei
solution: Experience Platform
title: Extremo de API de experimentos
description: El desarrollo y el aprendizaje de modelos se producen en el nivel de Experimento, donde un Experimento consta de una instancia MIL, ejecuciones de formación y ejecuciones de puntuación.
role: Developer
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# Extremo de experimentos

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

El desarrollo y el aprendizaje de modelos se producen en el nivel de Experimento, donde un Experimento consta de una instancia MIL, ejecuciones de formación y ejecuciones de puntuación.

## Crear un experimento {#create-an-experiment}

Puede crear un Experimento realizando una solicitud de POST mientras proporciona un nombre y un ID de instancia MIL válido en la carga útil de la solicitud.

>[!NOTE]
>
>A diferencia del aprendizaje de modelos en la IU de, la creación de un experimento a través de una llamada de API explícita no crea ni ejecuta automáticamente una ejecución de formación.

**Formato API**

```http
POST /experiments
```

**Solicitud**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre deseado para el Experimento. La ejecución aprendizaje correspondiente a este Experimento heredará este valor para mostrarse en la IU como nombre de ejecución aprendizaje. |
| `mlInstanceId` | Un ID de MLInstance válido. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles de la Experimento recién creada, incluido su identificador único (`id`).

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Crear y ejecutar un aprendizaje o una carrera de puntuación {#experiment-training-scoring}

Puede crear carreras de aprendizaje o anotación realizando un petición POST, proporcionando un ID de Experimento válido y especificando el tarea de carrera. Las carreras de puntuación solo se pueden crear si el Experimento tiene una ejecución de aprendizaje existente y exitosa. La creación exitosa de una ejecución aprendizaje inicializará el procedimiento de aprendizaje modelo y su finalización exitosa generará un modelo entrenado. La generación de modelos formados reemplazará a los existentes anteriormente, de modo que un experimento solo puede utilizar un único modelo entrenado en un momento determinado.

**Formato de API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de Experimento válido. |

**Solicitud**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `{TASK}` | Especifica la tarea de la ejecución. Establezca este valor como `train` para aprendizaje, `score` para puntuación o `featurePipeline` para canalización de características. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles de la ejecución recién creada, incluidos los parámetros de puntuación o aprendizaje predeterminados heredados y el ID único de la ejecución (`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Recuperar un lista de experimentos

Puede recuperar un lista de experimentos pertenecientes a un MLInstance en particular realizando un solo petición GET y proporcionando un ID de MLInstance válido como parámetro consulta. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [consulta parámetros para recurso recuperación](./appendix.md#query).


**Formato API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLINSTANCE_ID}` | Proporcione un ID de MLInstance válido para recuperar un lista de experimentos pertenecientes a esa MLInstance en particular. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve un lista de experimentos que comparten el mismo ID de MLInstance (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Recuperar un Experimento específico {#retrieve-specific}

GET Puede recuperar los detalles de un experimento específico realizando una solicitud que incluya el ID del experimento deseado en la ruta de solicitud.

**Formato API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de Experimento válido. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del Experimento solicitado.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Recuperar un lista de Experimento ejecuciones

Puede recuperar un lista de carreras de aprendizaje o anotación pertenecientes a un Experimento en particular realizando un solo petición GET y proporcionando un ID de Experimento válido. Para filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista completa de los parámetros de consulta disponibles, consulte la sección del apéndice sobre [consulta parámetros para recurso recuperación](./appendix.md#query).

>[!NOTE]
>
>Cuando se combinan varios parámetros consulta, estos deben separarse mediante ampersands (&amp;).

**Formato API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de Experimento válido. |
| `{QUERY_PARAMETER}` | Uno de los [parámetros](./appendix.md#query) de consulta disponibles que se usan para filtrar los resultados. |
| `{VALUE}` | El valor del parámetro de consulta anterior. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de ejecuciones de formación que pertenecen a algún experimento.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un lista de ejecuciones y cada uno de sus detalles, incluido el ID de ejecución Experimento (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Actualización de un experimento

Puede actualizar un experimento existente sobrescribiendo sus propiedades a través de una solicitud del PUT que incluya el ID del experimento de destinatario en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP]
>
>Para garantizar el éxito de esta solicitud de PUT, se recomienda que primero realice una solicitud de GET para [recuperar el experimento por ID](#retrieve-specific). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud del PUT.

La siguiente llamada de API de ejemplo actualiza el nombre de un experimento al tener estas propiedades inicialmente:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**Formato de API**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de Experimento válido. |

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles actualizados del Experimento.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Eliminar un Experimento

Puede eliminar una sola Experimento realizando un petición DELETE que incluya el ID del destino Experimento en la ruta de solicitud.

**Formato API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | ID de experimento válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Experimentos de Eliminar por MLInstance ID

Puede eliminar todos los experimentos que pertenezcan a un MLInstance en particular realizando un petición DELETE que incluya el ID de MLInstance como parámetro consulta.

**Formato API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | ---|
| `{MLINSTANCE_ID}` | ID de MLInstance válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiments successfully deleted"
}
```
