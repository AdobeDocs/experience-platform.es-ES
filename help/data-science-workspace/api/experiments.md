---
keywords: Experience Platform;guía para desarrolladores;punto final;Data Science Workspace;temas populares;experimentos;api sensei de aprendizaje automático
solution: Experience Platform
title: Punto final de API de experimentos
topic-legacy: Developer guide
description: El desarrollo de modelos y la formación se realizan a nivel de Experimento, donde un Experimento consiste en una instancia MLI, ejecuciones de capacitación y ejecuciones de puntuación.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# Punto final de experimentos

El desarrollo de modelos y la formación se realizan a nivel de Experimento, donde un Experimento consiste en una instancia MLI, ejecuciones de capacitación y ejecuciones de puntuación.

## Crear un experimento {#create-an-experiment}

Puede crear un experimento realizando una solicitud de POST mientras proporciona un nombre y un ID de instancia MLI válido en la carga útil de la solicitud.

>[!NOTE]
>
>A diferencia de la formación de modelos en la interfaz de usuario, la creación de un experimento mediante una llamada API explícita no crea y ejecuta automáticamente una ejecución de formación.

**Formato de API**

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
| `name` | El nombre deseado para el experimento. La ejecución de formación correspondiente a este experimento heredará este valor que se mostrará en la interfaz de usuario como nombre de la ejecución de la formación. |
| `mlInstanceId` | Un ID de instancia MLI válido. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento recién creado, incluido su identificador único (`id`).

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

## Creación y ejecución de una ejecución de formación o puntuación {#experiment-training-scoring}

Puede crear ejecuciones de formación o puntuación realizando una solicitud de POST, proporcionando un ID de experimento válido y especificando la tarea de ejecución. Las ejecuciones de puntuación solo se pueden crear si el experimento tiene una ejecución de formación existente y correcta. La creación exitosa de una ejecución de capacitación inicializará el procedimiento de capacitación modelo y su finalización exitosa generará un modelo entrenado. La generación de modelos formados reemplazará a los ya existentes, de modo que un Experimento solo puede utilizar un modelo entrenado en un momento dado.

**Formato de API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de experimento válido. |

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
| `{TASK}` | Especifica la tarea de ejecución. Establezca este valor como: `train` para formación, `score` para la puntuación, o `featurePipeline` para la canalización de funciones. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles de la ejecución recién creada, incluidos los parámetros de puntuación o formación predeterminados heredados y el ID exclusivo de la ejecución (`{RUN_ID}`).

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

## Recuperar una lista de experimentos

Puede recuperar una lista de Experimentos pertenecientes a una instancia MLI concreta realizando una única solicitud de GET y proporcionando un ID de instancia MLI válido como parámetro de consulta. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice de [parámetros de consulta para la recuperación de recursos](./appendix.md#query).


**Formato de API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLINSTANCE_ID}` | Proporcione un ID de instancia MLI válido para recuperar una lista de experimentos pertenecientes a esa instancia MLI concreta. |

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

Una respuesta correcta devuelve una lista de experimentos que comparten el mismo ID de instancia MLI (`{MLINSTANCE_ID}`).

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

## Recuperar un experimento específico {#retrieve-specific}

Puede recuperar los detalles de un experimento específico realizando una solicitud de GET que incluya el ID del experimento deseado en la ruta de solicitud.

**Formato de API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de experimento válido. |

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

Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento solicitado.

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

## Recuperar una lista de ejecuciones de Experimento

Puede recuperar una lista de ejecuciones de capacitación o puntuación que pertenezcan a un experimento concreto realizando una única solicitud de GET y proporcionando un ID de experimento válido. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista completa de los parámetros de consulta disponibles, consulte la sección del apéndice de [parámetros de consulta para la recuperación de recursos](./appendix.md#query).

>[!NOTE]
>
>Cuando se combinan varios parámetros de consulta, deben separarse con el signo &amp;.

**Formato de API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de experimento válido. |
| `{QUERY_PARAMETER}` | Uno de los [parámetros de consulta disponibles](./appendix.md#query) se utiliza para filtrar los resultados. |
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

Una respuesta correcta devuelve una carga útil que contiene una lista de ejecuciones y cada uno de sus detalles, incluido su ID de ejecución del experimento (`{RUN_ID}`).

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

## Actualizar un experimento

Puede actualizar un experimento existente sobrescribiendo sus propiedades mediante una solicitud de PUT que incluya el ID del experimento de destino en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP]
>
>Para garantizar el éxito de esta solicitud del PUT, se sugiere que primero realice una solicitud de GET a [recuperar el experimento por ID](#retrieve-specific). A continuación, modifique y actualice el objeto JSON devuelto y aplique todo el objeto JSON modificado como carga útil para la solicitud del PUT.

La siguiente llamada de API de ejemplo actualiza el nombre de un Experimento mientras que inicialmente tiene estas propiedades:

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
| `{EXPERIMENT_ID}` | Un ID de experimento válido. |

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

Una respuesta correcta devuelve una carga útil que contiene los detalles actualizados del experimento.

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

## Eliminar un experimento

Puede eliminar un solo experimento realizando una solicitud de DELETE que incluya el ID del experimento de destino en la ruta de solicitud.

**Formato de API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de experimento válido. |

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

## Eliminar experimentos por ID de instancia MLI

Puede eliminar todos los experimentos pertenecientes a una instancia MLI concreta realizando una solicitud de DELETE que incluya el ID de instancia MLI como parámetro de consulta.

**Formato de API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | ---|
| `{MLINSTANCE_ID}` | Un ID de instancia MLI válido. |

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
