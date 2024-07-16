---
keywords: Experience Platform;publicar un modelo;Workspace de ciencia de datos;temas populares;api de aprendizaje automático de sensei
solution: Experience Platform
title: 'Publish: un modelo como servicio mediante la API de aprendizaje automático de Sensei'
type: Tutorial
description: Este tutorial cubre el proceso de publicación de un modelo como servicio mediante la API de aprendizaje automático de Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 2%

---

# Publish creó un modelo como servicio utilizando [!DNL Sensei Machine Learning API]

Este tutorial cubre el proceso de publicación de un modelo como servicio mediante [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introducción

Este tutorial requiere una comprensión práctica de Adobe Experience Platform Data Science Workspace. Antes de comenzar este tutorial, revise la [descripción general de Data Science Workspace](../home.md) para obtener una introducción de alto nivel al servicio.

Para seguir este tutorial, debe tener un motor ML, una instancia ML y un experimento existentes. Para ver los pasos sobre cómo crearlos en la API, consulta el tutorial sobre [importación de una fórmula empaquetada](./import-packaged-recipe-api.md).

Por último, antes de iniciar este tutorial, consulte la sección [introducción](../api/getting-started.md) de la guía para desarrolladores para obtener información importante que necesita conocer para realizar correctamente llamadas a la API [!DNL Sensei Machine Learning], incluidos los encabezados necesarios utilizados en este tutorial:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

### Términos clave

En la tabla siguiente se describen algunos términos comunes utilizados en este tutorial:

| Término | Definición |
| --- | --- |
| **Instancia de aprendizaje automático (instancia ML)** | Instancia de un motor [!DNL Sensei] para un inquilino concreto, que contiene datos, parámetros y código [!DNL Sensei] específicos. |
| **Experimento** | Una entidad paraguas para albergar ejecuciones de experimentos de formación, ejecuciones de experimentos de puntuación o ambas. |
| **Experimento programado** | Término para describir la automatización de la formación o la puntuación de las ejecuciones de experimentos, regidas por una programación definida por el usuario. |
| **Ejecución de experimento** | Una instancia concreta de experimentos de formación o puntuación. Varias ejecuciones de experimentos de un experimento concreto pueden diferir en los valores del conjunto de datos utilizados para el aprendizaje o la puntuación. |
| **Modelo entrenado** | Un modelo de aprendizaje automático creado mediante el proceso de experimentación e ingeniería de funciones antes de llegar a un modelo validado, evaluado y finalizado. |
| **Modelo publicado** | Se llegó a un modelo finalizado y con versiones después del entrenamiento, la validación y la evaluación. |
| **Servicio de aprendizaje automático (servicio ML)** | Instancia de ML implementada como servicio para admitir solicitudes bajo demanda de formación y puntuación mediante un extremo de API. También se puede crear un servicio XML utilizando ejecuciones de experimento formadas existentes. |

## Crear un servicio ML con una ejecución de experimento de formación existente y una puntuación programada.

Al publicar un experimento de formación Ejecutar como servicio ML, puede programar la puntuación proporcionando detalles para la puntuación del experimento Ejecutar la carga útil de una solicitud de POST. Esto resulta en la creación de una entidad de Experimento programada para la puntuación.

**Formato de API**

```http
POST /mlServices
```

**Solicitud**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `mlInstanceId` | Identificación de instancia ML existente, la ejecución de experimento de formación utilizada para crear el servicio ML debe corresponder a esta instancia ML concreta. |
| `trainingExperimentId` | Identificación del experimento correspondiente a la identificación de la instancia de ML. |
| `trainingExperimentRunId` | Se utilizará una ejecución de experimento de formación concreta para publicar el servicio XML. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para la puntuación programada en Ejecuciones de experimento. |
| `scoringTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán para puntuar las ejecuciones de experimento. Por ejemplo, un valor de `10080` significa que se usarán datos de los últimos 10080 minutos o 168 horas para cada ejecución de experimento de puntuación programada. Tenga en cuenta que un valor de `0` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `scoringSchedule` | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo iniciar la puntuación. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo iniciar la puntuación. |
| `scoringSchedule.cron` | Valor Cron que indica el intervalo con el que se va a puntuar la ejecución del experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado, incluido su `id` único y el `scoringExperimentId` para su experimento de puntuación correspondiente.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Creación de un servicio XML a partir de una instancia XML existente

Según el caso de uso y los requisitos específicos, la creación de un servicio XML con una instancia XML es flexible en términos de programación de la formación y la puntuación de las ejecuciones de experimentos. Este tutorial analizará los casos específicos en los que:

- [No necesita una formación programada, pero necesita una puntuación programada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Se requieren ejecuciones de experimento programadas tanto para formación como para puntuación.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Tenga en cuenta que se puede crear un servicio XML con una instancia XML sin programar ningún experimento de formación o puntuación. Estos servicios XML crearán entidades de experimento normales y una única ejecución de experimento para formación y puntuación.

### Servicio ML con experimento programado para puntuación {#ml-service-with-scheduled-experiment-for-scoring}

Puede crear un servicio XML publicando una instancia XML con ejecuciones de experimento programadas para puntuación, lo que creará una entidad de experimento normal para formación. Se genera una ejecución de experimento de formación que se utilizará en todas las ejecuciones de experimento de puntuación programadas. Asegúrese de que dispone de los `mlInstanceId`, `trainingDataSetId` y `scoringDataSetId` necesarios para la creación del servicio XML y de que existen y son valores válidos.

**Formato de API**

```http
POST /mlServices
```

**Solicitud**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Clave JSON | Descripción |
| --- | --- |
| `mlInstanceId` | Identificación de instancia de ML existente, que representa la instancia de ML utilizada para crear el servicio ML. |
| `trainingDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para el experimento de formación. |
| `trainingTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán para el experimento de formación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10080 minutos o 168 horas para la ejecución del experimento de formación. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para aprendizaje. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para la puntuación programada en Ejecuciones de experimento. |
| `scoringTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán para puntuar las ejecuciones de experimento. Por ejemplo, un valor de `"10080"` significa que se usarán datos de los últimos 10080 minutos o 168 horas para cada ejecución de experimento de puntuación programada. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `scoringSchedule` | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo iniciar la puntuación. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo iniciar la puntuación. |
| `scoringSchedule.cron` | Valor Cron que indica el intervalo con el que se va a puntuar la ejecución del experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio XML recién creado. Esto incluye el(la) único(a) `id` del servicio, así como `trainingExperimentId` y `scoringExperimentId` para sus correspondientes experimentos de entrenamiento y puntuación, respectivamente.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### Servicio ML con experimentos programados para formación y puntuación {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Para publicar una instancia de ML existente como servicio ML con formación programada y ejecuciones de experimento de puntuación, debe proporcionar programaciones de formación y puntuación. Cuando se crea un servicio XML de esta configuración, también se crean entidades de experimento programadas tanto para formación como para puntuación. Tenga en cuenta que los horarios de formación y puntuación no tienen que ser los mismos. Durante la ejecución de un trabajo de puntuación, se recuperará el modelo formado más reciente producido por las ejecuciones de experimento de formación programadas y se utilizará en la ejecución de puntuación programada.

**Formato de API**

```http
POST /mlServices
```

**Solicitud**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Clave JSON | Descripción |
| --- | --- |
| `mlInstanceId` | Identificación de instancia de ML existente, que representa la instancia de ML utilizada para crear el servicio ML. |
| `trainingDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para el experimento de formación. |
| `trainingTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán para el experimento de formación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10080 minutos o 168 horas para la ejecución del experimento de formación. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para aprendizaje. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para la puntuación programada en Ejecuciones de experimento. |
| `scoringTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán para puntuar las ejecuciones de experimento. Por ejemplo, un valor de `"10080"` significa que se usarán datos de los últimos 10080 minutos o 168 horas para cada ejecución de experimento de puntuación programada. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `trainingSchedule` | Contiene detalles sobre las ejecuciones de experimentos de formación programadas. |
| `scoringSchedule` | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo iniciar la puntuación. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo iniciar la puntuación. |
| `scoringSchedule.cron` | Valor Cron que indica el intervalo con el que se va a puntuar la ejecución del experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio XML recién creado. Esto incluye el(la) único(a) `id` del servicio, así como `trainingExperimentId` y `scoringExperimentId` de sus correspondientes experimentos de entrenamiento y puntuación, respectivamente. En la respuesta de ejemplo siguiente, la presencia de `trainingSchedule` y `scoringSchedule` sugiere que las entidades Experimento para formación y puntuación son Experimentos programados.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## Buscar un servicio XML {#retrieving-ml-services}

Puede buscar un servicio XML existente realizando una solicitud `GET` a `/mlServices` y proporcionando el `id` único del servicio XML en la ruta.

**Formato de API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SERVICE_ID}` | El único `id` del servicio XML que está buscando. |

**Solicitud**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio XML.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>La recuperación de diferentes servicios XML puede devolver una respuesta con más o menos pares clave-valor. La respuesta anterior es una representación de un servicio [ML con entrenamiento programado y ejecuciones de experimento de puntuación](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Programar formación o puntuación

Si desea programar la puntuación y la formación en un servicio XML que ya se ha publicado, puede hacerlo actualizando el servicio XML existente con una solicitud `PUT` en `/mlServices`.

**Formato de API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SERVICE_ID}` | El único `id` del servicio XML que está actualizando. |

**Solicitud**

La siguiente solicitud programa la formación y la puntuación de un servicio XML existente agregando las claves `trainingSchedule` y `scoringSchedule` con sus respectivas claves `startTime`, `endTime` y `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>No intente modificar `startTime` en los trabajos de entrenamiento y puntuación programados existentes. Si se debe modificar `startTime`, considere la posibilidad de publicar el mismo modelo y reprogramar los trabajos de formación y puntuación.

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio XML actualizado.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
