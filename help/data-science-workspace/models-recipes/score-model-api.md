---
keywords: Experience Platform;Puntuar un modelo;Workspace de ciencia de datos;temas populares;api de aprendizaje automático de sensei
solution: Experience Platform
title: Puntuación de un modelo mediante la API de aprendizaje automático de Sensei
type: Tutorial
description: Este tutorial muestra cómo aprovechar las API de aprendizaje automático de Sensei para crear un experimento y una ejecución de experimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Puntuación de un modelo mediante [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Este tutorial muestra cómo aprovechar las API para crear un experimento y una ejecución de experimento. Para obtener una lista de todos los extremos de la API de aprendizaje automático de Sensei, consulte [este documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Crear un experimento programado para la puntuación

De forma similar a los Experimentos programados para formación, la creación de un Experimento programado para puntuación también se realiza incluyendo una sección `template` en el parámetro de cuerpo. Además, el campo `name` bajo `tasks` en el cuerpo está establecido como `score`.

A continuación se muestra un ejemplo de cómo crear un experimento que se ejecutará cada 20 minutos a partir de `startTime` y se ejecutará hasta `endTime`.

**Solicitud**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`: se encontró el valor de clave de API específico en la integración de Adobe Experience Platform única.\
`{JSON_PAYLOAD}`: objeto de ejecución de experimento que se enviará. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

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

`{INSTANCE_ID}`: ID que representa la instancia de MLI.\
`{MODEL_ID}`: ID que representa el modelo entrenado.

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

`{EXPERIMENT_ID}`: ID que representa el experimento.\
`{INSTANCE_ID}`: ID que representa la instancia de MLI.


### Crear una ejecución de experimento para puntuación

Ahora, con el modelo entrenado, podemos crear una Ejecución de experimento para la puntuación. El valor del parámetro `modelId` es el parámetro `id` devuelto en la solicitud del modelo de GET anterior.

**Solicitud**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`: se encontró el valor de clave de API específico en la integración de Adobe Experience Platform única.\
`{EXPERIMENT_ID}`: el ID correspondiente al experimento al que desea destinarlo. Esto se puede encontrar en la respuesta al crear el experimento.\
`{JSON_PAYLOAD}`: datos que se van a publicar. El ejemplo que utilizamos en nuestro tutorial es el siguiente:

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

`{MODEL_ID}`: ID correspondiente al modelo.

A continuación, se muestra la respuesta de la creación de la ejecución del experimento:

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

`{EXPERIMENT_ID}`: el ID correspondiente al experimento en el que se encuentra la ejecución.\
`{EXPERIMENT_RUN_ID}`: el ID correspondiente a la ejecución del experimento que acaba de crear.


### Recuperar un estado de ejecución de experimento para una ejecución de experimento programada

Para obtener las ejecuciones de experimentos para experimentos programados, la consulta se muestra a continuación:

**Solicitud**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: el ID correspondiente al experimento en el que se encuentra la ejecución.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.

Dado que hay varias ejecuciones de experimento para un experimento específico, la respuesta devuelta tendrá una matriz de ID de ejecución.

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

`{EXPERIMENT_RUN_ID}`: ID correspondiente a la ejecución del experimento.\
`{EXPERIMENT_ID}`: el ID correspondiente al experimento en el que se encuentra la ejecución.

### Detener y eliminar un experimento programado

Si desea detener la ejecución de un experimento programado antes de su `endTime`, se puede hacer consultando una solicitud del DELETE a `{EXPERIMENT_ID}`

**Solicitud**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: ID correspondiente al experimento.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.

>[!NOTE]
>
>La llamada de API deshabilita la creación de nuevas ejecuciones de experimentos. Sin embargo, no detendrá la ejecución de ejecuciones de experimentos que ya se estén ejecutando.

A continuación se muestra la respuesta que notifica que el experimento se ha eliminado correctamente.

**Respuesta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
