---
keywords: Experience Platform;guía para desarrolladores;extremo;Workspace de ciencia de datos;temas populares;mlservices;api de aprendizaje automático de sensei
solution: Experience Platform
title: Punto final de API de MLServices
description: Un MLService es un modelo entrenado publicado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad de automatizar la formación y la puntuación de forma programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficiencia y precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que las nuevas perspectivas se generen de forma coherente.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---

# Extremo de MLServices

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Un MLService es un modelo entrenado publicado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad de automatizar la formación y la puntuación de forma programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficiencia y precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que las nuevas perspectivas se generen de forma coherente.

Las programaciones de entrenamiento y puntuación automatizadas se definen con una marca de tiempo inicial, una marca de tiempo final y una frecuencia representada como una [expresión cron](https://en.wikipedia.org/wiki/Cron). Los horarios se pueden definir al [crear un MLService](#create-an-mlservice) o aplicar al [actualizar un MLService existente](#update-an-mlservice).

## Crear un MLService {#create-an-mlservice}

Puede crear un MLService realizando una solicitud de POST y una carga útil que proporcione un nombre para el servicio y un ID de instancia de MLI válido. La MLInstance utilizada para crear un MLService no es necesaria para tener experimentos de formación existentes, pero puede elegir crear el MLService con un modelo formado existente proporcionando el ID de experimento y el ID de ejecución de formación correspondientes.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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
| `name` | El nombre deseado para el servicio MLS. El servicio correspondiente a este MLService heredará este valor para mostrarlo en la interfaz de usuario de la Galería de servicios como el nombre del servicio. |
| `description` | Descripción opcional del servicio MLS. El servicio correspondiente a este MLService heredará este valor para mostrarlo en la interfaz de usuario de la Galería de servicios como la descripción del servicio. |
| `mlInstanceId` | ID de MLInstance válido. |
| `trainingDataSetId` | ID de conjunto de datos de formación que, de proporcionarse, anulará el ID de conjunto de datos predeterminado de la instancia de MLI. Si la MLInstance utilizada para crear el MLService no define un conjunto de datos de formación, debe proporcionar un ID de conjunto de datos de formación adecuado. |
| `trainingExperimentId` | Un ID de experimento que, opcionalmente, puede proporcionar. Si no se proporciona este valor, al crear el MLService se creará también un nuevo Experimento con las configuraciones predeterminadas de la MLInstance. |
| `trainingExperimentRunId` | Un ID de ejecución de formación que, opcionalmente, puede proporcionar. Si no se proporciona este valor, al crear el MLService también se creará y ejecutará una ejecución de formación utilizando los parámetros de formación predeterminados de la MLInstance. |
| `trainingSchedule` | Se ejecuta una programación para la formación automatizada. Si se define esta propiedad, MLService realizará automáticamente ejecuciones de formación de forma programada. |
| `trainingSchedule.startTime` | Una marca de tiempo para la cual comenzarán las ejecuciones de formación programadas. |
| `trainingSchedule.endTime` | Una marca de tiempo para la cual finalizarán las ejecuciones de formación programadas. |
| `trainingSchedule.cron` | Una expresión cron que define la frecuencia de las ejecuciones de formación automatizadas. |
| `scoringSchedule` | Se ejecuta una programación para la puntuación automatizada. Si se define esta propiedad, MLService realizará automáticamente ejecuciones de puntuación de forma programada. |
| `scoringSchedule.startTime` | Una marca de tiempo para la cual comenzarán las ejecuciones de puntuación programadas. |
| `scoringSchedule.endTime` | Una marca de tiempo para la cual finalizarán las ejecuciones de puntuación programadas. |
| `scoringSchedule.cron` | Expresión cron que define la frecuencia de las ejecuciones de puntuación automatizadas. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del MLService recién creado, incluido su identificador único (`id`), el identificador de experimento para formación (`trainingExperimentId`), el identificador de experimento para puntuación (`scoringExperimentId`) y el identificador del conjunto de datos de formación de entrada (`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
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

## Recuperar una lista de MLServices {#retrieve-a-list-of-mlservices}

Puede recuperar una lista de MLServices realizando una única solicitud de GET. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de recursos](./appendix.md#query).

**Formato de API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno de los [parámetros de consulta disponibles](./appendix.md#query) que se usa para filtrar los resultados. |
| `{VALUE}` | El valor del parámetro de consulta anterior. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de MLServices que comparten el mismo identificador de MLInstance (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de MLServices y sus detalles, incluidos el identificador de MLService (`{MLSERVICE_ID}`), el identificador de experimento para formación (`{TRAINING_ID}`), el identificador de experimento para puntuación (`{SCORING_ID}`) y el identificador del conjunto de datos de formación de entrada (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Recuperar un MLService específico {#retrieve-a-specific-mlservice}

Puede recuperar los detalles de un experimento específico realizando una solicitud de GET que incluya el ID del servicio MLS deseado en la ruta de solicitud.

**Formato de API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: ID de MLService válido.

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del MLService solicitado.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Actualizar un MLService {#update-an-mlservice}

Puede actualizar un MLService existente sobrescribiendo sus propiedades a través de una solicitud del PUT que incluya el ID del MLService de destino en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP]
>
>Para garantizar el éxito de esta solicitud de PUT, se recomienda que primero realice una solicitud de GET para [recuperar el MLService por ID](#retrieve-a-specific-mlservice). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud del PUT.

**Formato de API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: ID de MLService válido.

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
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
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
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

Puede eliminar un único MLService realizando una solicitud de DELETE que incluya el ID del MLService de destino en la ruta de solicitud.

**Formato de API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLSERVICE_ID}` | ID de MLService válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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
    "detail": "MLService deletion was successful"
}
```

## Eliminar MLServices por ID de MLInstance

Puede eliminar todos los MLServices que pertenezcan a una MLInstance determinada realizando una solicitud de DELETE que especifique un ID de MLInstance como parámetro de consulta.

**Formato de API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLINSTANCE_ID}` | ID de MLInstance válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLServices deletion was successful"
}
```
