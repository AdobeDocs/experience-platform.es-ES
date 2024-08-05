---
keywords: Experience Platform;entrenar y evaluar;Workspace de ciencia de datos;temas populares;API de aprendizaje automático de Sensei
solution: Experience Platform
title: Entrenar y evaluar un modelo con la API de aprendizaje automático de Sensei
type: Tutorial
description: Este tutorial muestra cómo crear, entrenar y evaluar un modelo mediante llamadas a la API de aprendizaje automático de Sensei.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# Entrenar y evaluar un modelo con la [!DNL Sensei Machine Learning] API

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

Este tutorial le mostrará cómo crear, entrenar y evaluar un modelo mediante llamadas a la API. Consulte [este documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para obtener una lista detallada de la documentación de la API.

## Requisitos previos

Siga la [Importar una receta empaquetada utilizando la API](./import-packaged-recipe-api.md) para crear un motor, que es necesaria para entrenar y evaluar un modelo mediante la API.

Siga el tutorial de autenticación de API de Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para inicio realizar llamadas a la [API.

Desde la tutorial ahora debería tener los siguientes valores:

- `{ACCESS_TOKEN}`: El valor específico del token al portador proporcionado después de la autenticación.
- `{ORG_ID}`: las credenciales de su organización se encuentran en su integración de Adobe Experience Platform única.
- `{API_KEY}`: se encontró el valor de clave de API específico en la integración de Adobe Experience Platform única.

- Vínculo a una imagen Docker de un servicio inteligente

## Flujo de trabajo API

Vamos a consumir las API para crear una ejecución de experimento para formación. Para este tutorial, nos centraremos en los extremos de Motores, Instancias MLI y Experimentos. El siguiente gráfico describe la relación entre los tres y también introduce la idea de una ejecución y un modelo.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Los términos &quot;Engine&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experimento&quot; y &quot;Model&quot; se denominan términos diferentes en el IU. Si viene de la interfaz de usuario de, la siguiente tabla muestra las diferencias.

| Término de IU | Término de API |
| --- | --- |
| Fórmula | Motor |
| Modelo | MLInstance |
| Ejecuciones de formación | Experimento |
| Servicio | MLService |

### Crear una instancia de MLI

La creación de una MLInstance se puede realizar mediante la siguiente solicitud. Utilizará el `{ENGINE_ID}` que se devolvió al crear un motor desde el tutorial [Importar una fórmula empaquetada mediante API](./import-packaged-recipe-ui.md).

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

`{ACCESS_TOKEN}`: El valor específico del token al portador proporcionado después de la autenticación.\
`{ORG_ID}`: las credenciales de su organización se encuentran en su integración de Adobe Experience Platform única.\
`{API_KEY}`: se encontró el valor de clave de API específico en la integración de Adobe Experience Platform única.\
`{JSON_PAYLOAD}`: la configuración de nuestra MLInstance. El ejemplo que utilizamos en nuestro tutorial se muestra aquí:

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
>En `{JSON_PAYLOAD}`, definimos los parámetros utilizados para el aprendizaje y la puntuación en la matriz `tasks`. `{ENGINE_ID}` es el identificador del motor que desea utilizar y el campo `tag` es un parámetro opcional utilizado para identificar la instancia.

La respuesta contiene `{INSTANCE_ID}`, que representa la MLInstance creada. Se pueden crear varias instancias XML de modelo con diferentes configuraciones.

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

`{ENGINE_ID}`: este ID que representa el motor en el que se crea la instancia MLI.\
`{INSTANCE_ID}`: ID que representa la instancia de MLI.

### Crear un experimento

Un científico de datos utiliza un experimento para llegar a un modelo de alto rendimiento durante la formación. Varios experimentos incluyen el cambio de conjuntos de datos, funciones, parámetros de aprendizaje y hardware. El siguiente es un ejemplo de creación de un experimento.

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

`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`: el valor específico de la clave de API que se encuentra en la integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Experimento objeto que se crea. El ejemplo que usamos en nuestro tutorial se muestra aquí:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: ID que representa la instancia de MLI.

La respuesta de la creación Experimento tiene este aspecto.

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

`{EXPERIMENT_ID}`: el ID que representa el experimento que acaba de crear.
`{INSTANCE_ID}`: ID que representa la instancia de MLI.

### Crear un experimento programado para aprendizaje

Los experimentos programados se utilizan para que no tengamos que crear cada Experimento se ejecuta a través de una llamada a la API. En su lugar, proporcionamos todos los parámetros necesarios durante Experimento creación y cada ejecución se creará periódicamente.

Para indicar la creación de un experimento programado, debemos agregar una sección `template` en el cuerpo de la solicitud. En `template`, se incluyen todos los parámetros necesarios para programar ejecuciones, como `tasks`, que indica qué acción, y `schedule`, que indica el tiempo de las ejecuciones programadas.

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

`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.\
`{ACCESS_TOKEN}`: El valor específico del token al portador proporcionado después de la autenticación.\
`{API_KEY}`: el valor específico de la clave de API que se encuentra en la integración única de Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Conjunto de datos que se publicará. El ejemplo que usamos en nuestro tutorial se muestra aquí:

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

Cuando creamos un Experimento, el cuerpo, `{JSON_PAYLOAD}`, debe contener el `mlInstanceId` o el `mlInstanceQuery` parámetro. En este ejemplo, una Experimento programada invocará una ejecución cada 20 minutos, establecida en el `cron` parámetro, comenzando desde la `startTime` función hasta .`endTime`

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

`{EXPERIMENT_ID}`: el ID que representa el Experimento.\
`{INSTANCE_ID}`: El ID que representa a MLInstance.


### Crear un Experimento Run for aprendizaje

Con una entidad Experimento creada, se puede crear y ejecutar una ejecución aprendizaje utilizando la siguiente llamada. Necesitará el `{EXPERIMENT_ID}` e indicar lo que `mode` desea activar en el cuerpo solicitud.

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

`{EXPERIMENT_ID}`: el ID correspondiente al experimento al que desea destinarlo. Esto se puede encontrar en la respuesta al crear el experimento.\
`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{API_KEY}`: se encontró el valor de clave de API específico en la integración de Adobe Experience Platform única.\
`{JSON_PAYLOAD}`: Para crear una ejecución aprendizaje, deberá incluir lo siguiente en el cuerpo:

```JSON
{
    "mode":"Train"
}
```

También puede anular los parámetros de configuración incluyendo una matriz `tasks`:

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

Recibirá la siguiente respuesta que le informará sobre `{EXPERIMENT_RUN_ID}` y la configuración en `tasks`.

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

`{EXPERIMENT_RUN_ID}`: ID que representa la ejecución del experimento.\
`{EXPERIMENT_ID}`: ID que representa el experimento en el que se encuentra la ejecución del experimento.

### Recuperar un estado de ejecución de experimento

El estado de la ejecución del experimento se puede consultar con `{EXPERIMENT_RUN_ID}`.

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: ID que representa el experimento.\
`{EXPERIMENT_RUN_ID}`: ID que representa la ejecución del experimento.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.\
`{API_KEY}`: el valor específico de la clave de API que se encuentra en la integración única de Adobe Experience Platform.

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

`{EXPERIMENT_RUN_ID}`: el ID que representa la Experimento Ejecutar.\
`{EXPERIMENT_ID}`: ID que representa el experimento en el que se encuentra la ejecución del experimento.

Además del estado `DONE`, otros estados incluyen:
- `PENDING`
- `RUNNING`
- `FAILED`

Para obtener más información, se pueden encontrar los registros detallados en el parámetro `tasklogs`.

### Recuperar el modelo entrenado

Para obtener el modelo entrenado creado anteriormente durante el aprendizaje, realizamos la siguiente solicitud:

**Solicitud**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: el ID correspondiente a la ejecución del experimento que desea segmentar. Esto se puede encontrar en la respuesta al crear la ejecución del experimento.\
`{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.\
`{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.

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
`{EXPERIMENT_ID}`: el ID correspondiente al experimento en el que se ejecuta el experimento.\
`{EXPERIMENT_RUN_ID}`: el ID correspondiente a la Experimento Ejecutar.

### Parada y eliminar un Experimento programado

Si desea detener la ejecución de un Experimento programado antes de su `endTime`, puede hacerlo consultando un petición DELETE al `{EXPERIMENT_ID}`

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

La siguiente es la respuesta que notifica que el Experimento se ha eliminado correctamente.

**Respuesta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Pasos siguientes

Este tutorial trata sobre cómo consumir las API para crear un motor, un experimento, ejecuciones de experimentos programadas y modelos formados. En el [próximo ejercicio](./score-model-api.md), hará predicciones al puntuar un nuevo conjunto de datos usando el modelo entrenado de mayor rendimiento.
