---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Servicios
topic: Developer guide
translation-type: tm+mt
source-git-commit: dabeee04dd6ec2bbdd37a6987efcb54b285df7ca

---


# MLServices

Un MLService es un modelo publicado y capacitado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad para automatizar la capacitación y la puntuación de manera programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficacia y la precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que se generen nuevas perspectivas de forma coherente.

Las programaciones automatizadas de capacitación y puntuación se definen con una marca de tiempo inicial, una marca de tiempo final y una frecuencia representada como una expresión <a href="https://en.wikipedia.org/wiki/Cron" target="_blank"></a>cron. Las programaciones se pueden definir al [crear un MLService](#create-an-mlservice) o al [actualizar un MLService](#update-an-mlservice)existente.

## Crear un MLService

Puede crear un MLService realizando una solicitud POST y una carga útil que proporcione un nombre para el servicio y un ID de instancia MLI válido. La instancia MLI utilizada para crear un servicio MLService no es necesaria para tener experimentos de formación existentes, pero puede elegir crear el servicio MLService con un modelo entrenado existente proporcionando la ID del experimento y la ID de ejecución de formación correspondientes.

**Formato de API**

```http
POST /mlServices
```

**Solicitud**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingExperimentRunId": "{RUN_ID}",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre deseado para MLService. El servicio correspondiente a este MLService heredará este valor para que se muestre en la interfaz de usuario de la Galería de servicios como nombre del servicio. |
| `description` | Una descripción opcional para MLService. El servicio correspondiente a este MLService heredará este valor que se mostrará en la interfaz de usuario de la Galería de servicios como descripción del servicio. |
| `mlInstanceId` | Un ID de instancia MLI válido. |
| `trainingDataSetId` | Un ID de conjunto de datos de formación que, si se proporciona, sobrescribirá el ID de conjunto de datos predeterminado de MLInency. Si la instancia MLI utilizada para crear MLService no define un conjunto de datos de formación, debe proporcionar un ID de conjunto de datos de formación adecuado. |
| `trainingExperimentId` | ID del experimento que puede proporcionar de forma opcional. Si no se proporciona este valor, la creación de MLService también creará un nuevo experimento con las configuraciones predeterminadas de MLInstand. |
| `trainingExperimentRunId` | ID de ejecución de formación que puede proporcionar de forma opcional. Si no se proporciona este valor, la creación de MLService también creará y ejecutará una ejecución de formación utilizando los parámetros de formación predeterminados de MLInstand. |
| `trainingSchedule` | Una programación para las ejecuciones de formación automatizada. Si se define esta propiedad, MLService realizará automáticamente ejecuciones de formación programadas. |
| `trainingSchedule.startTime` | Marca de hora para la que se iniciarán las ejecuciones de formación programadas. |
| `trainingSchedule.endTime` | Marca de hora para la que finalizarán las ejecuciones de formación programadas. |
| `trainingSchedule.cron` | Una expresión cron que define la frecuencia de las ejecuciones de formación automatizada. |
| `scoringSchedule` | Un programa para las ejecuciones de puntuación automatizada. Si se define esta propiedad, MLService realizará automáticamente ejecuciones de puntuación programadas. |
| `scoringSchedule.startTime` | Marca de hora para la cual comenzarán las ejecuciones de puntuación programadas. |
| `scoringSchedule.endTime` | Marca de hora para la que finalizarán las ejecuciones de puntuación programadas. |
| `scoringSchedule.cron` | Una expresión cron que define la frecuencia de las ejecuciones de puntuación automatizada. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del nuevo servicio MLService, incluido su identificador único (`id`), ID del experimento para la formación (`trainingExperimentId`), ID del experimento para la puntuación (`scoringExperimentId`) y el ID del conjunto de datos de formación de entrada (`trainingDataSetId`).

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Recuperar una lista de MLServices

Puede recuperar una lista de MLServices realizando una sola solicitud GET. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de la solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](./appendix.md#query)de recursos.

**Formato de API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno de los parámetros [de consulta](./appendix.md#query) disponibles para filtrar los resultados. |
| `{VALUE}` | El valor del parámetro de consulta anterior. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de MLServices que comparte el mismo ID de instancia MLI (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId=={MLINSTANCE_ID}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de MLServices y sus detalles, incluyendo su ID de MLService (`{MLSERVICE_ID}`), ID de experimento para formación (`{TRAINING_ID}`), ID de experimento para la puntuación (`{SCORING_ID}`) y el ID de conjunto de datos de formación de entrada (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "{MLSERVICE_ID}",
            "name": "A service created in UI",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "trainingExperimentId": "{TRAINING_ID}",
            "trainingDataSetId": "{DATASET_ID}",
            "scoringExperimentId": "{SCORING_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId=={MLINSTANCE_ID},deleted==false",
        "count": 1
    }
}
```

## Recuperar un MLService específico

Puede recuperar los detalles de un experimento específico realizando una solicitud GET que incluya el ID de MLService deseado en la ruta de solicitud.

**Formato de API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:: Un ID de MLService válido.

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del MLService solicitado.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Actualizar un MLService

Puede actualizar un MLService existente sobrescribiendo sus propiedades mediante una solicitud PUT que incluya el ID de destinatario MLService en la ruta de la solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP] Para garantizar el éxito de esta solicitud PUT, se sugiere que primero realice una solicitud GET para [recuperar el MLService por ID](#retrieve-a-specific-mlservice). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud PUT.

**Formato de API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:: Un ID de MLService válido.

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "scoringExperimentId": "{SCORING_ID}",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles actualizados de MLService.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Eliminar un MLService

Puede eliminar un único MLService realizando una solicitud DELETE que incluya el ID de destinatario MLService en la ruta de solicitud.

**Formato de API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLSERVICE_ID}` | Un ID de MLService válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
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
    "detail": "MLService deletion was successful"
}
```

## Eliminar MLServices por ID de instancia MLI

Puede eliminar todos los servicios MLServices pertenecientes a una instancia MLI concreta realizando una solicitud DELETE que especifica un ID de instancia MLI como parámetro de consulta.

**Formato de API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLSERVICE_ID}` | Un ID de MLService válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId={MLINSTANCE_ID} \
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
    "detail": "MLServices deletion was successful"
}
```
