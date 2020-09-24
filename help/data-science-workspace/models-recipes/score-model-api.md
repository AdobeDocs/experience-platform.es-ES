---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: Puntuación de un modelo (API)
topic: tutorial
type: Tutorial
description: Este tutorial le mostrará cómo aprovechar las API de aprendizaje automático de Sensei para crear un experimento y una ejecución de experimentos.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---


# Puntuación de un modelo (API)

Este tutorial le mostrará cómo aprovechar las API para crear un experimento y una ejecución de experimento. Para obtener una lista detallada de la documentación de la API, consulte [este documento](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Crear un experimento programado para la puntuación

De forma similar a los experimentos programados para la formación, la creación de un experimento programado para la puntuación también se realiza mediante la inclusión de una `template` sección en el parámetro body. Además, el `name` campo debajo `tasks` del cuerpo se establece como `score`.

El siguiente es un ejemplo de creación de un experimento que se ejecutará cada 20 minutos a partir de `startTime` y se ejecutará hasta `endTime`.

**Solicitud**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`:: Objeto de ejecución del experimento que se va a enviar. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`:: ID que representa la instancia MLI.\
`{MODEL_ID}`:: ID que representa el modelo formado.

La siguiente es la respuesta después de crear el experimento programado.

**Respuesta**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`:: ID que representa el experimento.\
`{INSTANCE_ID}`:: ID que representa la instancia MLI.


### Crear una ejecución de experimento para la puntuación

Ahora con el modelo entrenado, podemos crear una Carrera de Experimentos para la puntuación. El valor del `modelId` parámetro es el `id` parámetro devuelto en la solicitud del modelo de GET anterior.

**Solicitud**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.\
`{EXPERIMENT_ID}`:: ID correspondiente al experimento que desea destinatario. Esto se encuentra en la respuesta al crear el experimento.\
`{JSON_PAYLOAD}`:: Datos que se van a publicar. El ejemplo que utilizamos en nuestro tutorial está aquí:

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`:: ID correspondiente al modelo.

La respuesta de la creación de la ejecución de experimentos se muestra a continuación:

**Respuesta**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`::  ID correspondiente al experimento en el que se encuentra la ejecución.\
`{EXPERIMENT_RUN_ID}`:: ID correspondiente a la ejecución del experimento que acaba de crear.


### Recuperar el estado de ejecución de experimentos para la ejecución programada de experimentos

Para obtener ejecuciones de experimentos para experimentos programados, la consulta se muestra a continuación:

**Solicitud**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`::  ID correspondiente al experimento en el que se encuentra la ejecución.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.

Dado que existen varias ejecuciones de experimento para un experimento específico, la respuesta devuelta tendrá una matriz de ID de ejecución.

**Respuesta**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:: ID correspondiente a la ejecución del experimento.\
`{EXPERIMENT_ID}`::  ID correspondiente al experimento en el que se encuentra la ejecución.

### Detener y eliminar un experimento programado

Si desea detener la ejecución de un experimento programado antes de su ejecución `endTime`, esto se puede hacer consultando una solicitud de DELETE al `{EXPERIMENT_ID}`

**Solicitud**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`::  ID correspondiente al experimento.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.

>[!NOTE]
>
>La llamada de API deshabilitará la creación de nuevas ejecuciones de Experimento. Sin embargo, no detendrá la ejecución de ejecuciones de experimentos que ya se estén ejecutando.

A continuación se muestra la respuesta que notifica que el experimento se ha eliminado correctamente.

**Respuesta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
