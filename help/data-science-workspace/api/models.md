---
keywords: Experience Platform;guía para desarrolladores;punto final;Área de trabajo de ciencias de datos;temas populares;modelos;API de aprendizaje automático sensei
solution: Experience Platform
title: Extremo de la API de modelos
topic: Developer guide
description: Un modelo es una instancia de una fórmula de aprendizaje automático que se capacita mediante datos históricos y configuraciones para resolver un caso de uso comercial.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---


# Extremo de modelos

Un modelo es una instancia de una fórmula de aprendizaje automático que se capacita mediante datos históricos y configuraciones para resolver un caso de uso comercial.

## Recuperar una lista de modelos

Puede recuperar una lista de detalles del modelo que pertenezca a todos los modelos realizando una sola solicitud de GET a /models. De forma predeterminada, esta lista se ordenará a sí misma del modelo creado más antiguo y limitará los resultados a 25. Puede elegir filtrar los resultados especificando algunos parámetros de consulta. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de activos](./appendix.md#query).

**Formato API**

```http
GET /models
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles de los modelos, incluido el identificador único de cada modelo (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID correspondiente al modelo. |
| `modelArtifactUri` | URI que indica dónde se almacena el modelo. El URI termina con el valor `name` del modelo. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |

## Recuperar un modelo específico

Puede recuperar una lista de los detalles del modelo que pertenezcan a un modelo concreto realizando una sola solicitud de GET y proporcionando un ID de modelo válido en la ruta de solicitud. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de activos](./appendix.md#query).

**Formato de API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MODEL_ID}` | Identificador del modelo preparado o publicado. |
| `{EXPERIMENT_RUN_ID}` | Identificador de la ejecución del experimento. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una lista de modelos formados que comparten el mismo valor de experienceRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del modelo, incluido el identificador único de modelos (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID correspondiente al modelo. |
| `modelArtifactUri` | URI que indica dónde se almacena el modelo. El URI termina con el valor `name` del modelo. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |

## Registrar un modelo pregenerado {#register-a-model}

Puede registrar un modelo pregenerado realizando una solicitud de POST al extremo `/models`. Para registrar el modelo, es necesario incluir el archivo `modelArtifact` y los valores de propiedad `model` en el cuerpo de la solicitud.

**Formato de API**

```http
POST /models
```

**Solicitud**

El siguiente POST contiene los valores de propiedades `modelArtifact` y `model` que son necesarios. Consulte la tabla siguiente para obtener más información sobre estos valores.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parámetro | Descripción |
| --- | --- |
| `modelArtifact` | Ubicación del artefacto de modelo completo que desea incluir. |
| `model` | Datos de formulario del objeto Model que se debe crear. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del modelo, incluido el identificador único de modelos (`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID correspondiente al modelo. |
| `modelArtifactUri` | URI que indica dónde se almacena el modelo. El URI termina con el valor `id` del modelo. |

## Actualizar un modelo por ID

Puede actualizar un modelo existente sobrescribiendo sus propiedades mediante una solicitud de PUT que incluya el ID del modelo de destinatario en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP]
>
>Para garantizar el éxito de esta solicitud de PUT, se sugiere que primero realice una solicitud de GET para recuperar el modelo por ID. A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud de PUT.

**Formato de API**

```http
PUT /models/{MODEL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MODEL_ID}` | Identificador del modelo preparado o publicado. |

**Solicitud**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles actualizados del experimento.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Eliminar un modelo por ID

Puede eliminar un solo modelo realizando una solicitud de DELETE que incluya el ID del modelo de destinatario en la ruta de solicitud.

**Formato de API**

```http
DELETE /models/{MODEL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MODEL_ID}` | Identificador del modelo preparado o publicado. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un estado de 200 que confirma la eliminación del modelo.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Crear una nueva transcodificación para un modelo {#create-transcoded-model}

La transcodificación es la conversión directa de digital a digital de una codificación a otra. Puede crear una nueva transcodificación para un modelo proporcionando el `{MODEL_ID}` y un `targetFormat` en el que desea que se muestre el nuevo resultado.

**Formato de API**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parámetro | Descripción |
| --- | --- |
| `{MODEL_ID}` | Identificador del modelo preparado o publicado. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto JSON con la información de la transcodificación. Esto incluye el identificador único de transcodificaciones (`id`) utilizado en [recuperación de un modelo transcodificado específico](#retrieve-transcoded-model).

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Recuperar una lista de transcodificaciones para un modelo {#retrieve-transcoded-model-list}

Puede recuperar una lista de transcodificaciones que se han realizado en un modelo realizando una solicitud de GET con su `{MODEL_ID}`.

**Formato de API**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parámetro | Descripción |
| --- | --- |
| `{MODEL_ID}` | Identificador del modelo preparado o publicado. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto json con una lista de cada transcodificación realizada en el Modelo. Cada modelo transcodificado recibe un identificador único (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Recuperar un modelo transcodificado específico {#retrieve-transcoded-model}

Puede recuperar un modelo transcodificado específico realizando una solicitud de GET con su `{MODEL_ID}` y la identificación de un modelo transcodificado.

**Formato de API**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MODEL_ID}` | Identificador único de un modelo con formación o publicado. |
| `{TRANSCODING_ID}` | Identificador único de un modelo transcodificado. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto JSON con los datos del Modelo transcodificado.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```


