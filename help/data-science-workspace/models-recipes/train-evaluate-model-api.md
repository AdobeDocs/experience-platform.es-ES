---
keywords: Experience Platform;entrenar y evaluar;Data Science Workspace;temas populares;API de aprendizaje automático de Sensei
solution: Experience Platform
title: Capacitar y evaluar un modelo mediante la API de aprendizaje automático de Sensei
type: Tutorial
description: Este tutorial le muestra cómo crear, entrenar y evaluar un modelo mediante llamadas a la API de aprendizaje automático de Sensei.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# Capacite y evalúe un modelo utilizando la variable [!DNL Sensei Machine Learning] API


Este tutorial le muestra cómo crear, entrenar y evaluar un modelo mediante llamadas API. Consulte [este documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para obtener una lista detallada de la documentación de API.

## Requisitos previos

Siga las [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md) para crear un motor, que es necesario para entrenar y evaluar un modelo mediante la API.

Siga las [Tutorial de autenticación de API de Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para empezar a realizar llamadas de API.

Desde el tutorial, debería tener los siguientes valores:

- `{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.
- `{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.
- `{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.

- Enlace a una imagen de Docker de un servicio inteligente

## Flujo de trabajo de API

Vamos a consumir las API para crear un Experimento para formación. Para este tutorial, nos centraremos en los extremos de Motores, Instancias MLI y Experimentos. El siguiente gráfico describe la relación entre los tres y también presenta la idea de una ejecución y un modelo.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Los términos &quot;Motor&quot;, &quot;MLInposition&quot;, &quot;MLService&quot;, &quot;Experimento&quot; y &quot;Modelo&quot; se denominan en la IU como términos diferentes. Si proviene de la interfaz de usuario, la siguiente tabla asigna las diferencias.

| Término de interfaz de usuario | Término de API |
| --- | --- |
| Fórmula | Motor |
| Modelo | Instancia MLI |
| Ejecuciones de formación | Experimento |
| Service | MLService |

### Crear una instancia MLI

La creación de una instancia MLI se puede realizar utilizando la siguiente solicitud. Utilizará la variable `{ENGINE_ID}` que se devolvió al crear un motor desde el [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-ui.md) tutorial.

**Solicitud**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: La configuración de nuestra instancia MLI. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>En el `{JSON_PAYLOAD}`, definimos los parámetros utilizados para la formación y la puntuación en la variable `tasks` matriz. La variable `{ENGINE_ID}` es el ID del motor que desea utilizar y la variable `tag` field es un parámetro opcional utilizado para identificar la instancia.

La respuesta contiene el `{INSTANCE_ID}` que representa la instancia MLI que se crea. Se pueden crear varias instancias MLI de modelo con diferentes configuraciones.

**Respuesta**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Este ID representa el motor en el que se crea la instancia MLI.\
`{INSTANCE_ID}`: ID que representa la instancia MLI.

### Crear un experimento

Un Experimento es utilizado por un científico de datos para llegar a un modelo de alto rendimiento durante la formación. Varios experimentos incluyen el cambio de conjuntos de datos, características, parámetros de aprendizaje y hardware. A continuación se muestra un ejemplo de creación de un experimento.

**Solicitud**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objeto de experimento creado. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: ID que representa la instancia MLI.

La respuesta de la creación del experimento tiene este aspecto.

**Respuesta**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: El ID que representa el experimento que acaba de crear.
`{INSTANCE_ID}`: ID que representa la instancia MLI.

### Creación de un experimento programado para formación

Los experimentos programados se utilizan para que no sea necesario crear cada ejecución de experimento individual mediante una llamada de API. En su lugar, proporcionamos todos los parámetros necesarios durante la creación del experimento y cada ejecución se creará periódicamente.

Para indicar la creación de un experimento programado, debemos agregar un `template` en el cuerpo de la solicitud. En `template`, se incluyen todos los parámetros necesarios para programar ejecuciones como `tasks`, que indican qué acción y `schedule`, que indica el tiempo de ejecución programada.

**Solicitud**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Conjunto de datos a publicar. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
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
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

Cuando creamos un experimento, el cuerpo, `{JSON_PAYLOAD}`, debe contener `mlInstanceId` o `mlInstanceQuery` parámetro. En este ejemplo, un Experimento programado invocará una ejecución cada 20 minutos y se establecerá en la variable `cron` , empezando por el `startTime` hasta que `endTime`.

**Respuesta**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: El ID que representa el experimento.\
`{INSTANCE_ID}`: ID que representa la instancia MLI.


### Creación de una ejecución de experimento para formación

Con la entidad Experimento creada, se puede crear una ejecución de formación y ejecutarla con la llamada siguiente. Necesitará la variable `{EXPERIMENT_ID}` y establezca qué `mode` desea realizar el déclencheur en el cuerpo de la solicitud.

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

`{EXPERIMENT_ID}`: El ID correspondiente al experimento al que desea dirigirse. Esto se encuentra en la respuesta al crear el experimento.\
`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Para crear una ejecución de formación, debe incluir lo siguiente en el cuerpo:

```JSON
{
    "mode":"Train"
}
```

También puede anular los parámetros de configuración incluyendo un `tasks` matriz:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

Recibirá la siguiente respuesta, que le informará de la `{EXPERIMENT_RUN_ID}` y la configuración en `tasks`.

**Respuesta**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: El ID que representa la ejecución del experimento.\
`{EXPERIMENT_ID}`: El ID que representa el experimento en el que se encuentra la ejecución del experimento.

### Recuperar el estado de ejecución de un experimento

Se puede consultar el estado de la ejecución del experimento con la variable `{EXPERIMENT_RUN_ID}`.

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: El ID que representa el experimento.\
`{EXPERIMENT_RUN_ID}`: El ID que representa la ejecución del experimento.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{API_KEY}`: El valor clave de API específico que se encuentra en su integración única de Adobe Experience Platform.

**Respuesta**

La llamada de GET proporcionará el estado en la variable `state` como se muestra a continuación:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`: El ID que representa la ejecución del experimento.\
`{EXPERIMENT_ID}`: El ID que representa el experimento en el que se encuentra la ejecución del experimento.

Además del `DONE` , otros estados incluyen:
- `PENDING`
- `RUNNING`
- `FAILED`

Para obtener más información, los registros detallados se pueden encontrar en la sección `tasklogs` parámetro.

### Recuperar el modelo entrenado

Para obtener el modelo entrenado creado anteriormente durante la formación, realizamos la siguiente solicitud:

**Solicitud**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: El ID correspondiente a la ejecución del experimento que desea dirigir. Esto se puede encontrar en la respuesta al crear la ejecución del experimento.\
`{ACCESS_TOKEN}`: Su valor de token al portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.

La respuesta representa el modelo entrenado que se creó.

**Respuesta**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: ID correspondiente al modelo.\
`{EXPERIMENT_ID}`: El ID correspondiente al experimento en el que se encuentra la ejecución del experimento.\
`{EXPERIMENT_RUN_ID}`: ID correspondiente a la ejecución del experimento.

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

## Pasos siguientes

Este tutorial trata sobre cómo utilizar las API para crear un motor, un experimento, ejecuciones de experimentos programadas y modelos formados. En el [ejercicio siguiente](./score-model-api.md), hará predicciones mediante la puntuación de un nuevo conjunto de datos usando el modelo entrenado de mayor rendimiento.
