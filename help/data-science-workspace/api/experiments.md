---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Experimentos
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Experimentos

El desarrollo de modelos y la formación se realizan en el nivel Experimento, donde un Experimento consiste en una instancia MLI, ejecuciones de capacitación y carreras de puntuación.

## Crear un experimento

Puede crear un experimento realizando una solicitud POST mientras proporciona un nombre y un ID de instancia MLI válido en la carga útil de la solicitud.

>[!NOTE] A diferencia de la formación de modelos en la interfaz de usuario, la creación de un experimento a través de una llamada de API explícita no crea ni ejecuta automáticamente una ejecución de formación.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "{MLINSTANCE_ID}"
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | El nombre deseado para el experimento. La ejecución de formación correspondiente a este experimento heredará este valor para que se muestre en la interfaz de usuario como nombre de la ejecución de formación. |
| `mlInstanceId` | Un ID de instancia MLI válido. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento recién creado, incluido su identificador único (`id`).

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Crear y ejecutar una ejecución de formación o puntuación

Puede crear ejecuciones de puntuación o formación realizando una solicitud POST, proporcionando un ID de experimento válido y especificando la tarea de ejecución. Las ejecuciones de puntuación solo se pueden crear si el experimento tiene una ejecución de formación existente y correcta. Si se crea correctamente una ejecución de formación, se inicializará el procedimiento de formación del modelo y su finalización con éxito generará un modelo capacitado. La generación de modelos formados reemplazará a los ya existentes, de modo que un experimento solo puede utilizar un modelo entrenado en un momento dado.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `{TASK}` | Especifica la tarea de la ejecución. Establezca este valor como `train` para formación, `score` puntuación o `fp` para la canalización de funciones. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles de la ejecución recién creada, incluidos los parámetros de puntuación o formación predeterminados heredados y el ID único (`{RUN_ID}`) de la ejecución.

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
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

Puede recuperar una lista de Experimentos que pertenezcan a una instancia MLI concreta realizando una sola solicitud GET y proporcionando un ID de instancia MLI válido como parámetro de consulta. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](./appendix.md#query)de recursos.


**Formato de API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLINSTANCE_ID}` | Proporcione un ID de entidad MLI válido para recuperar una lista de experimentos pertenecientes a esa instancia MLI en particular. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de experimentos que comparten el mismo ID de instancia MLI (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
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

Puede recuperar los detalles de un experimento específico realizando una solicitud GET que incluya el ID del experimento deseado en la ruta de solicitud.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento solicitado.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Recuperar una lista de ejecuciones de experimentos

Puede recuperar una lista de ejecuciones de formación o puntuación que pertenezcan a un experimento determinado realizando una sola solicitud GET y proporcionando un ID de experimento válido. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de la solicitud. Para obtener una lista completa de los parámetros de consulta disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](./appendix.md#query)de recursos.

>[!NOTE] Cuando se combinan varios parámetros de consulta, deben separarse con signos ampersands (&amp;).

**Formato de API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID de experimento válido. |
| `{QUERY_PARAMETER}` | Uno de los parámetros [de consulta](./appendix.md#query) disponibles para filtrar los resultados. |
| `{VALUE}` | El valor del parámetro de consulta anterior. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de ejecuciones de formación que pertenecen a algún experimento.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene una lista de ejecuciones y cada uno de sus detalles, incluido el ID de ejecución del experimento (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Actualizar un experimento

Puede actualizar un experimento existente sobrescribiendo sus propiedades mediante una solicitud PUT que incluya el ID del experimento de destinatario en la ruta de la solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP] Para garantizar el éxito de esta solicitud PUT, se sugiere que primero realice una solicitud GET para [recuperar el experimento por ID](#retrieve-specific). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud PUT.

La siguiente llamada de API de ejemplo actualiza el nombre de un experimento mientras que inicialmente tiene estas propiedades:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
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
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Eliminar un experimento

Puede eliminar un solo experimento realizando una solicitud de ELIMINACIÓN que incluya el ID del experimento de destinatario en la ruta de solicitud.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Puede eliminar todos los experimentos que pertenezcan a una instancia MLI concreta realizando una solicitud DELETE que incluya el ID de instancia MLI como parámetro de consulta.

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
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
