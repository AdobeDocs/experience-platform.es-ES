---
keywords: Experience Platform;guía para desarrolladores;extremo;Área de trabajo de ciencias de datos;temas populares;mlservices;API de aprendizaje automático sensei
solution: Experience Platform
title: Extremo de API de MLServices
topic: Developer guide
description: Un MLService es un modelo publicado y capacitado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad para automatizar la capacitación y la puntuación de manera programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficacia y la precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que se generen nuevas perspectivas de forma coherente.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---


# Extremo de MLServices

Un MLService es un modelo publicado y capacitado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad para automatizar la capacitación y la puntuación de manera programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficacia y la precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que se generen nuevas perspectivas de forma coherente.

Las programaciones automatizadas de capacitación y puntuación se definen con una marca de fecha y hora de inicio, una marca de hora de finalización y una frecuencia representada como una [expresión cron](https://en.wikipedia.org/wiki/Cron). Las programaciones se pueden definir cuando [cree un MLService](#create-an-mlservice) o cuando se apliquen [actualizando un MLService](#update-an-mlservice) existente.

## Crear un MLService {#create-an-mlservice}

Puede crear un MLService realizando una solicitud de POST y una carga útil que proporcione un nombre para el servicio y un ID de instancia MLI válido. La instancia MLI utilizada para crear un servicio MLService no es necesaria para tener experimentos de formación existentes, pero puede elegir crear el servicio MLService con un modelo entrenado existente proporcionando la ID del experimento y la ID de ejecución de formación correspondientes.

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

Una respuesta correcta devuelve una carga útil que contiene los detalles del nuevo servicio MLService, incluido su identificador único (`id`), el ID del experimento para la formación (`trainingExperimentId`), el ID del experimento para la puntuación (`scoringExperimentId`) y el ID del conjunto de datos de formación de entrada (`trainingDataSetId`).

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

Puede recuperar una lista de MLServices realizando una sola solicitud de GET. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de activos](./appendix.md#query).

**Formato de API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno de los [parámetros de consulta disponibles](./appendix.md#query) utilizados para filtrar los resultados. |
| `{VALUE}` | El valor del parámetro de consulta anterior. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de MLServices que comparte el mismo ID de instancia MLI (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de MLServices y sus detalles, incluyendo su ID de MLService (`{MLSERVICE_ID}`), ID de experimento para formación (`{TRAINING_ID}`), ID de experimento para la puntuación (`{SCORING_ID}`) y el ID de conjunto de datos de capacitación de entrada (`{DATASET_ID}`).

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

Puede recuperar los detalles de un experimento específico realizando una solicitud de GET que incluya el ID de MLService deseado en la ruta de solicitud.

**Formato de API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:: Un ID de MLService válido.

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Puede actualizar un MLService existente sobrescribiendo sus propiedades mediante una solicitud de PUT que incluya el ID de destinatario MLService en la ruta de la solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP]
>
>Para garantizar el éxito de esta solicitud de PUT, se sugiere que primero realice una solicitud de GET para [recuperar el MLService por ID](#retrieve-a-specific-mlservice). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud de PUT.

**Formato de API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:: Un ID de MLService válido.

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Puede eliminar un único MLService realizando una solicitud de DELETE que incluya el ID de destinatario MLService en la ruta de solicitud.

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
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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

Puede eliminar todos los servicios MLServices pertenecientes a una instancia MLI concreta realizando una solicitud de DELETE que especifique un ID de instancia MLI como parámetro de consulta.

**Formato de API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID de instancia MLI válido. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
