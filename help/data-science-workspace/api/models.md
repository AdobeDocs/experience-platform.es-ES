---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelos
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Modelos

Un modelo es una instancia de una fórmula de aprendizaje automático que se capacita mediante datos históricos y configuraciones para resolver un caso de uso comercial.

## Recuperar una lista de modelos

Puede recuperar una lista de los detalles del modelo que pertenezcan a todos los modelos realizando una sola solicitud GET a /models. De forma predeterminada, esta lista se ordenará a sí misma del modelo creado más antiguo y limitará los resultados a 25. Puede elegir filtrar los resultados especificando algunos parámetros de consulta. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](./appendix.md#query)de recursos.

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

Una respuesta correcta devuelve una carga útil que contiene los detalles de los modelos, incluido el identificador único (`id`) de cada modelo.

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
| `modelArtifactUri` | URI que indica dónde se almacena el modelo. El URI termina con el `name` valor del modelo. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |

## Recuperar un modelo específico

Puede recuperar una lista de los detalles del modelo que pertenezcan a un modelo concreto realizando una única solicitud GET y proporcionando un ID de modelo válido en la ruta de solicitud. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de la solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](./appendix.md#query)de recursos.

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
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del modelo, incluido el identificador único (`id`) Modelos.

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
        "count": 1
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID correspondiente al modelo. |
| `modelArtifactUri` | URI que indica dónde se almacena el modelo. El URI termina con el `name` valor del modelo. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |

## Actualizar un modelo por ID

Puede actualizar un modelo existente sobrescribiendo sus propiedades mediante una solicitud PUT que incluya el ID del modelo de destinatario en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!TIP] Para garantizar el éxito de esta solicitud PUT, se sugiere que primero realice una solicitud GET para recuperar el modelo por ID. A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud PUT.

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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

Puede eliminar un solo modelo realizando una solicitud DELETE que incluya el ID del modelo de destinatario en la ruta de solicitud.

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
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
