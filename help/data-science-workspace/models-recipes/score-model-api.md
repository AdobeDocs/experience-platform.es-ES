---
keywords: Experience Platform;Puntuación de un modelo;Data Science Workspace;temas populares;api sensei de aprendizaje automático
solution: Experience Platform
title: Puntuación de un modelo mediante la API de aprendizaje automático de Sensei
type: Tutorial
description: Este tutorial le muestra cómo aprovechar las API de aprendizaje automático de Sensei para crear un experimento y una ejecución de experimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# Puntuación de un modelo mediante la variable [!DNL Sensei Machine Learning API]

Este tutorial le muestra cómo aprovechar las API para crear un experimento y una ejecución de experimento. Para obtener una lista de todos los extremos de la API de aprendizaje automático de Sensei, consulte [este documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Crear un experimento programado para la puntuación

De forma similar a los experimentos programados para formación, la creación de un experimento programado para la puntuación también se realiza incluyendo un `template` al parámetro body. Además, la variable `name` campo bajo `tasks` en el cuerpo se establece como `score`.

A continuación se muestra un ejemplo de creación de un experimento que se ejecutará cada 20 minutos a partir de `startTime` y se ejecutará hasta `endTime`.

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

`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objeto de ejecución del experimento que se va a enviar. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

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

`{INSTANCE_ID}`: ID que representa la instancia MLI.\
`{MODEL_ID}`: El ID que representa el modelo entrenado.

A continuación se muestra la respuesta después de crear el experimento programado.

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

`{EXPERIMENT_ID}`: El ID que representa el experimento.\
`{INSTANCE_ID}`: ID que representa la instancia MLI.


### Crear una ejecución de experimento para la puntuación

Ahora, con el modelo entrenado, podemos crear una Carrera de Experimento para la puntuación. El valor de la variable `modelId` es el parámetro `id` parámetro devuelto en la solicitud del modelo de GET anterior.

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

`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.\
`{EXPERIMENT_ID}`: El ID correspondiente al experimento al que desea dirigirse. Esto se encuentra en la respuesta al crear el experimento.\
`{JSON_PAYLOAD}`: Datos que se van a publicar. El ejemplo que utilizamos en nuestro tutorial es este:

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

La respuesta de la creación de la ejecución del experimento se muestra a continuación:

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

`{EXPERIMENT_ID}`: El ID correspondiente al experimento en el que se encuentra la ejecución.\
`{EXPERIMENT_RUN_ID}`: El ID correspondiente a la ejecución del experimento que acaba de crear.


### Recuperar el estado de ejecución de un experimento para la ejecución programada de un experimento

Para obtener ejecuciones de experimento para experimentos programados, la consulta se muestra a continuación:

**Solicitud**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: El ID correspondiente al experimento en el que se encuentra la ejecución.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.

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
`{EXPERIMENT_ID}`: El ID correspondiente al experimento en el que se encuentra la ejecución.

### Detener y eliminar un experimento programado

Si desea detener la ejecución de un experimento programado antes de su `endTime`, esto se puede hacer consultando una solicitud del DELETE al `{EXPERIMENT_ID}`

**Solicitud**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: ID correspondiente al experimento.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.

>[!NOTE]
>
>La llamada de API deshabilitará la creación de nuevas ejecuciones de Experimento. Sin embargo, no detendrá la ejecución de ejecuciones de experimento que ya se estén ejecutando.

A continuación se muestra la respuesta que notifica que el experimento se ha eliminado correctamente.

**Respuesta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
