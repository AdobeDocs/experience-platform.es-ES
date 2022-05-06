---
keywords: Experience Platform;guía para desarrolladores;punto final;Data Science Workspace;temas populares;mlservices;api sensei de aprendizaje automático
solution: Experience Platform
title: Punto final de API de MLServices
topic-legacy: Developer guide
description: Un MLService es un modelo publicado y entrenado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad de automatizar la capacitación y la puntuación de forma programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficacia y la precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que se generen nuevas perspectivas de forma coherente.
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Extremo de MLServices

Un MLService es un modelo publicado y entrenado que proporciona a su organización la capacidad de acceder y reutilizar modelos desarrollados anteriormente. Una característica clave de MLServices es la capacidad de automatizar la capacitación y la puntuación de forma programada. Las ejecuciones de formación programadas pueden ayudar a mantener la eficacia y la precisión de un modelo, mientras que las ejecuciones de puntuación programadas pueden garantizar que se generen nuevas perspectivas de forma coherente.

Las programaciones de capacitación y puntuación automatizadas se definen con una marca de tiempo de inicio, una marca de tiempo de finalización y una frecuencia representadas como [expresión cron](https://en.wikipedia.org/wiki/Cron). Las programaciones se pueden definir cuando [creación de un MLService](#create-an-mlservice) o aplicado por [actualización de un servicio MLS existente](#update-an-mlservice).

## Creación de un servicio MLS {#create-an-mlservice}

Puede crear un MLService realizando una solicitud de POST y una carga útil que proporcione un nombre para el servicio y un ID de instancia MLI válido. La instancia MLI utilizada para crear un MLService no es necesaria para tener experimentos de formación existentes, pero puede elegir crear el MLService con un modelo entrenado existente proporcionando el ID del experimento y el ID de ejecución de formación correspondientes.

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
| `name` | El nombre deseado para MLService. El servicio correspondiente a este MLService heredará este valor que se mostrará en la interfaz de usuario de la Galería de servicios como nombre del servicio. |
| `description` | Una descripción opcional del MLService. El servicio correspondiente a este MLService heredará este valor que se mostrará en la interfaz de usuario de la Galería de servicios como descripción del servicio. |
| `mlInstanceId` | Un ID de instancia MLI válido. |
| `trainingDataSetId` | Un ID de conjunto de datos de formación que, si se proporciona, anulará el ID predeterminado del conjunto de datos de MLInposition. Si la instancia MLI utilizada para crear el MLService no define un conjunto de datos de capacitación, debe proporcionar un ID de conjunto de datos de capacitación adecuado. |
| `trainingExperimentId` | ID de experimento que puede proporcionar de forma opcional. Si no se proporciona este valor, la creación de MLService también creará un nuevo Experimento usando las configuraciones predeterminadas de MLInposition. |
| `trainingExperimentRunId` | ID de ejecución de formación que puede proporcionar de forma opcional. Si no se proporciona este valor, la creación del MLService también creará y ejecutará una ejecución de capacitación utilizando los parámetros de capacitación predeterminados de MLInposition. |
| `trainingSchedule` | Se ejecuta un programa de capacitación automatizada. Si se define esta propiedad, MLService realizará automáticamente ejecuciones de capacitación programadas. |
| `trainingSchedule.startTime` | Marca de tiempo para la que se iniciarán las ejecuciones de capacitación programadas. |
| `trainingSchedule.endTime` | Marca de fecha y hora para la que finaliza la formación programada. |
| `trainingSchedule.cron` | Expresión cron que define la frecuencia de ejecución automatizada de formación. |
| `scoringSchedule` | Se ejecuta un programa para la puntuación automatizada. Si se define esta propiedad, MLService realizará automáticamente ejecuciones de puntuación programadas. |
| `scoringSchedule.startTime` | Marca de tiempo para la que se iniciarán las ejecuciones de puntuación programadas. |
| `scoringSchedule.endTime` | Marca de fecha y hora para la que finalizarán las ejecuciones de puntuación programadas. |
| `scoringSchedule.cron` | Expresión cron que define la frecuencia de ejecuciones de puntuación automatizada. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del MLService recién creado, incluido su identificador único (`id`), ID de experimento para formación (`trainingExperimentId`), ID de experimento para la puntuación (`scoringExperimentId`) y el ID del conjunto de datos de capacitación de entrada (`trainingDataSetId`).

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

Puede recuperar una lista de MLServices realizando una única solicitud de GET. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice de [parámetros de consulta para la recuperación de recursos](./appendix.md#query).

**Formato de API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno de los [parámetros de consulta disponibles](./appendix.md#query) se utiliza para filtrar los resultados. |
| `{VALUE}` | El valor del parámetro de consulta anterior. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de MLServices que comparten el mismo ID de instancia MLI (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de MLServices y sus detalles, incluido su ID de MLService (`{MLSERVICE_ID}`), ID de experimento para formación (`{TRAINING_ID}`), ID de experimento para la puntuación (`{SCORING_ID}`) y el ID del conjunto de datos de capacitación de entrada (`{DATASET_ID}`).

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

* `{MLSERVICE_ID}`: Un ID de MLService válido.

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

Puede actualizar un MLService existente sobrescribiendo sus propiedades a través de una solicitud de PUT que incluya el ID del MLService de destinatario en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP]
>
>Para garantizar el éxito de esta solicitud del PUT, se sugiere que primero realice una solicitud de GET a [recuperar el MLService por ID](#retrieve-a-specific-mlservice). A continuación, modifique y actualice el objeto JSON devuelto y aplique todo el objeto JSON modificado como carga útil para la solicitud del PUT.

**Formato de API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Un ID de MLService válido.

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

## Eliminación de un MLService

Puede eliminar un único MLService realizando una solicitud de DELETE que incluya el ID del MLService de destino en la ruta de solicitud.

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

## Eliminación de MLServices por MLInency ID

Puede eliminar todos los MLServices que pertenecen a una instancia MLI en particular realizando una solicitud de DELETE que especifica un ID de instancia MLI como parámetro de consulta.

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
