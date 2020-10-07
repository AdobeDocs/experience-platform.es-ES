---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics;Sensei Machine Learning API
solution: Experience Platform
title: Formación y evaluación de un modelo (API)
topic: tutorial
type: Tutorial
description: Este tutorial le mostrará cómo crear, entrenar y evaluar un modelo mediante llamadas a la API de aprendizaje automático Sensei.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 1%

---


# Formación y evaluación de un modelo (API)


Este tutorial le mostrará cómo crear, entrenar y evaluar un modelo mediante llamadas de API. Consulte [este documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para obtener una lista detallada de la documentación de API.

## Requisitos previos

Siga la sección [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md) para crear un motor, que es necesario para entrenar y evaluar un modelo mediante la API.

Siga este [tutorial](../../tutorials/authentication.md) para obtener autorización para realizar llamadas de API a inicio.

En el tutorial ahora debe tener los siguientes valores:

- `{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.
- `{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.
- `{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.

- Vínculo a una imagen de Docker de un servicio inteligente

## Flujo de trabajo de API

Usaremos las API para crear una ejecución de experimentos para formación. Para este tutorial, nos centraremos en los extremos de motores, instancias MLI y experimentos. El siguiente gráfico describe la relación entre los tres y también introduce la idea de una ejecución y un modelo.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Los términos &quot;Motor&quot;, &quot;MLInsistance&quot;, &quot;MLService&quot;, &quot;Experiment&quot; y &quot;Modelo&quot; se conocen como términos diferentes en la interfaz de usuario. Si viene de la interfaz de usuario, la siguiente tabla asignará las diferencias.
> 
> | Término de interfaz de usuario | Término de API |
> --- | ---
> | Fórmula | Motor |
> | Modelo | MLInance |
> | Ejecuciones de formación | Experimento |
> | Service | MLService |



### Crear una instancia MLI

La creación de una instancia MLI se puede realizar mediante la siguiente solicitud. Utilizará el `{ENGINE_ID}` que se devolvió al crear un motor a partir del tutorial de API [](./import-packaged-recipe-ui.md) Importar una fórmula empaquetada.

**Solicitud**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`:: La configuración de nuestra instancia MLI. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

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
>En la `{JSON_PAYLOAD}`, definimos los parámetros utilizados para la formación y la puntuación en la `tasks` matriz. El `{ENGINE_ID}` es el ID del motor que desea utilizar y el `tag` campo es un parámetro opcional utilizado para identificar la instancia.

La respuesta contendrá la `{INSTANCE_ID}` cual representa la instancia MLI que se crea. Se pueden crear varias instancias MLI de modelo con diferentes configuraciones.

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

`{ENGINE_ID}`:: Este ID representa el motor en el que se crea la instancia MLI.\
`{INSTANCE_ID}`:: ID que representa la instancia MLI.

### Crear un experimento

Un experto en ciencia de datos utiliza un experimento para llegar a un modelo de alto rendimiento durante la formación. Varios experimentos incluyen el cambio de conjuntos de datos, características, parámetros de aprendizaje y hardware. El siguiente es un ejemplo de creación de un experimento.

**Solicitud**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`:: Objeto de experimento que se crea. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`:: ID que representa la instancia MLI.

La respuesta de la creación del experimento es así.

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

`{EXPERIMENT_ID}`:: ID que representa el experimento que acaba de crear.
`{INSTANCE_ID}`:: ID que representa la instancia MLI.

### Crear un experimento programado para formación

Los experimentos programados se utilizan para que no sea necesario crear cada ejecución de experimento mediante una llamada de API. En su lugar, proporcionamos todos los parámetros necesarios durante la creación del experimento y cada ejecución se creará periódicamente.

Para indicar la creación de un experimento programado, debemos agregar una `template` sección en el cuerpo de la solicitud. En `template`, se incluyen todos los parámetros necesarios para programar las ejecuciones, como `tasks`, que indican qué acción y `schedule`, que indica el tiempo de ejecución programada.

**Solicitud**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`:: Conjunto de datos que se va a publicar. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

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

Cuando creamos un experimento, el cuerpo, `{JSON_PAYLOAD}`, debe contener el `mlInstanceId` o el parámetro `mlInstanceQuery` . En este ejemplo, un experimento programado invocará una ejecución cada 20 minutos, definida en el `cron` parámetro, comenzando desde el `startTime` hasta el `endTime`.

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

`{EXPERIMENT_ID}`:: ID que representa el experimento.\
`{INSTANCE_ID}`:: ID que representa la instancia MLI.


### Crear una ejecución de experimento para formación

Con la creación de una entidad Experimento, se puede crear y ejecutar una ejecución de formación mediante la llamada siguiente. Necesitará el estado `{EXPERIMENT_ID}` y lo que `mode` desea activar en el cuerpo de la solicitud.

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

`{EXPERIMENT_ID}`:: ID correspondiente al experimento que desea destinatario. Esto se encuentra en la respuesta al crear el experimento.\
`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`:: Para crear una ejecución de formación, deberá incluir lo siguiente en el cuerpo:

```JSON
{
    "mode":"Train"
}
```

También puede anular los parámetros de configuración incluyendo una `tasks` matriz:

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

Recibirá la siguiente respuesta que le permitirá conocer el `{EXPERIMENT_RUN_ID}` y la configuración en `tasks`.

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

`{EXPERIMENT_RUN_ID}`::  ID que representa la ejecución del experimento.\
`{EXPERIMENT_ID}`:: ID que representa el experimento en el que se encuentra la ejecución del experimento.

### Recuperar el estado de ejecución de un experimento

El estado de la ejecución del experimento se puede consultar con el `{EXPERIMENT_RUN_ID}`.

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:: ID que representa el experimento.\
`{EXPERIMENT_RUN_ID}`:: ID que representa la ejecución del experimento.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.\
`{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.

**Respuesta**

La llamada de GET proporcionará el estado en el `state` parámetro como se muestra a continuación:

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

`{EXPERIMENT_RUN_ID}`::  ID que representa la ejecución del experimento.\
`{EXPERIMENT_ID}`:: ID que representa el experimento en el que se encuentra la ejecución del experimento.

Además del `DONE` estado, otros estados incluyen:
- `PENDING`
- `RUNNING`
- `FAILED`

Para obtener más información, los registros detallados se pueden encontrar bajo el `tasklogs` parámetro .

### Recuperar el modelo entrenado

Para obtener el modelo capacitado creado anteriormente durante la formación, realizamos la siguiente solicitud:

**Solicitud**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`:: ID correspondiente a la ejecución del experimento que desea destinatario. Esto se encuentra en la respuesta al crear la ejecución del experimento.\
`{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.\
`{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.

La respuesta representa el modelo capacitado que se creó.

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

`{MODEL_ID}`:: ID correspondiente al modelo.\
`{EXPERIMENT_ID}`::  ID correspondiente al experimento en el que se encuentra la ejecución del experimento.\
`{EXPERIMENT_RUN_ID}`:: ID correspondiente a la ejecución del experimento.

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

## Pasos siguientes

En este tutorial se explica cómo utilizar las API para crear un motor, un experimento, ejecuciones de experimentos programadas y modelos formados. En el [próximo ejercicio](./score-model-api.md), realizará predicciones mediante la puntuación de un nuevo conjunto de datos con el modelo capacitado de mayor rendimiento.