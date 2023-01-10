---
keywords: Experience Platform;publicar un modelo;Data Science Workspace;temas populares;api sensei de aprendizaje automático
solution: Experience Platform
title: Publicación de un modelo como servicio mediante la API de aprendizaje automático de Sensei
type: Tutorial
description: Este tutorial trata el proceso de publicación de un modelo como servicio mediante la API de aprendizaje automático de Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 2%

---

# Publicación de un modelo como servicio mediante el [!DNL Sensei Machine Learning API]

Este tutorial trata el proceso de publicación de un modelo como servicio mediante el uso de [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Primeros pasos

Este tutorial requiere una comprensión práctica de Adobe Experience Platform Data Science Workspace. Antes de comenzar este tutorial, revise la [Información general de Data Science Workspace](../home.md) para una introducción de alto nivel al servicio.

Para seguir este tutorial, debe tener un motor ML, una instancia ML y un experimento existentes. Para ver los pasos sobre cómo crearlos en la API, consulte el tutorial sobre [importación de una fórmula empaquetada](./import-packaged-recipe-api.md).

Finalmente, antes de iniciar este tutorial, revise la [introducción](../api/getting-started.md) de la guía para desarrolladores para obtener información importante que necesita conocer para realizar correctamente llamadas al [!DNL Sensei Machine Learning] API, incluidos los encabezados requeridos que se usan en este tutorial:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

### Términos clave

La siguiente tabla describe algunos términos comunes utilizados en este tutorial:

| Término | Definición |
| --- | --- |
| **Instancia de aprendizaje automático (instancia ML)** | Una instancia de un [!DNL Sensei] Motor de un inquilino en particular, que contiene datos, parámetros y [!DNL Sensei] código. |
| **Experimento** | Una entidad paraguas para la celebración de ejecuciones de experimentos de formación, la puntuación de ejecuciones de experimentos, o ambas. |
| **Experimento programado** | Término que describe la automatización de las ejecuciones de experimentos de capacitación o puntuación, regido por una programación definida por el usuario. |
| **Ejecución del experimento** | Un ejemplo particular de experimentos de capacitación o puntuación. Varias ejecuciones de experimento de un experimento en particular pueden diferir en los valores de conjuntos de datos utilizados para la formación o la puntuación. |
| **Modelo capacitado** | Modelo de aprendizaje automático creado por el proceso de experimentación y la ingeniería de funciones antes de llegar a un modelo validado, evaluado y finalizado. |
| **Modelo publicado** | Se llegó a un modelo finalizado y con versiones después de la formación, validación y evaluación. |
| **Servicio de aprendizaje automático (servicio ML)** | Instancia de ML implementada como servicio para admitir solicitudes de capacitación y puntuación bajo demanda mediante un punto final de API. También se puede crear un servicio ML utilizando las ejecuciones de experimento formadas existentes. |

## Crear un servicio ML con una ejecución de experimento de formación existente y una puntuación programada

Al publicar un Experimento de formación Ejecutar como un Servicio ML, puede programar la puntuación proporcionando detalles para el Experimento de puntuación Ejecute la carga útil de una solicitud de POST. Esto resulta en la creación de una entidad de experimento programada para la puntuación.

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
| `mlInstanceId` | La identificación existente de la instancia ML, la ejecución del experimento de formación utilizada para crear el servicio ML debe corresponder a esta instancia ML concreta. |
| `trainingExperimentId` | Identificación del experimento correspondiente a la identificación de la instancia ML. |
| `trainingExperimentRunId` | Una ejecución de experimento de formación específica que se utilizará para publicar el servicio ML. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para las ejecuciones de experimento de puntuación programada. |
| `scoringTimeframe` | Un valor de entero que representa los minutos en los que se filtrarán los datos que se utilizarán para puntuar las ejecuciones de experimento. Por ejemplo, un valor de `10080` significa que los datos de los últimos 10 080 minutos o 168 horas se utilizarán para cada ejecución programada del experimento de puntuación. Tenga en cuenta que un valor de `0` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `scoringSchedule` | Contiene detalles sobre la puntuación programada en Ejecuciones de experimento. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo se inicia la puntuación. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo se inicia la puntuación. |
| `scoringSchedule.cron` | Valor cron que indica el intervalo en el que se va a puntuar las ejecuciones de experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado, incluyendo su `id` y `scoringExperimentId` para su correspondiente experimento de puntuación.


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

## Creación de un servicio ML a partir de una instancia ML existente

Dependiendo de su caso de uso específico y de sus requisitos, la creación de un servicio ML con una instancia ML es flexible en términos de programación de las ejecuciones de experimento y puntuación. Este tutorial tratará casos específicos en los que:

- [No necesita formación programada, pero sí puntuación programada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Se requieren ejecuciones de experimento programadas para la formación y la puntuación.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Tenga en cuenta que se puede crear un servicio ML utilizando una instancia ML sin programar ningún experimento de formación o puntuación. Estos servicios ML crearán entidades de experimento comunes y un único programa de experimento para la formación y la puntuación.

### Servicio ML con experimento programado para obtener una puntuación {#ml-service-with-scheduled-experiment-for-scoring}

Puede crear un servicio ML publicando una instancia ML con ejecuciones de experimento programadas para la puntuación, lo que creará una entidad de experimento normal para la formación. Se genera una ejecución de experimento de formación que se utilizará para todas las ejecuciones de experimento de puntuación programadas. Asegúrese de que tiene la variable `mlInstanceId`, `trainingDataSetId`y `scoringDataSetId` necesario para la creación del servicio ML, y que existen y son valores válidos.

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
| `mlInstanceId` | Identificación de instancia ML existente, que representa la instancia ML utilizada para crear el servicio ML. |
| `trainingDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para el experimento de formación. |
| `trainingTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán en el experimento de formación. Por ejemplo, un valor de `"10080"` significa que los datos de los últimos 10 080 minutos o 168 horas se utilizarán para la ejecución del experimento de formación. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para formación. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para las ejecuciones de experimento de puntuación programada. |
| `scoringTimeframe` | Un valor de entero que representa los minutos en los que se filtrarán los datos que se utilizarán para puntuar las ejecuciones de experimento. Por ejemplo, un valor de `"10080"` significa que los datos de los últimos 10 080 minutos o 168 horas se utilizarán para cada ejecución programada del experimento de puntuación. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `scoringSchedule` | Contiene detalles sobre la puntuación programada en Ejecuciones de experimento. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo se inicia la puntuación. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo se inicia la puntuación. |
| `scoringSchedule.cron` | Valor cron que indica el intervalo en el que se va a puntuar las ejecuciones de experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado. Esto incluye la variable única del servicio `id`, así como el `trainingExperimentId` y `scoringExperimentId` para sus correspondientes experimentos de capacitación y puntuación, respectivamente.

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

Para publicar una instancia de ML existente como un servicio ML con ejecuciones de experimento programadas y de puntuación, debe proporcionar programas de formación y puntuación. Cuando se crea un servicio ML de esta configuración, también se crean entidades de experimento programadas tanto para la formación como para la puntuación. Tenga en cuenta que los programas de capacitación y puntuación no tienen por qué ser los mismos. Durante la ejecución de un trabajo de puntuación, se recuperará el último modelo entrenado producido por las ejecuciones de experimento de formación programada y se utilizará para la ejecución de puntuación programada.

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
| `mlInstanceId` | Identificación de instancia ML existente, que representa la instancia ML utilizada para crear el servicio ML. |
| `trainingDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para el experimento de formación. |
| `trainingTimeframe` | Un valor entero que representa los minutos para filtrar los datos que se utilizarán en el experimento de formación. Por ejemplo, un valor de `"10080"` significa que los datos de los últimos 10 080 minutos o 168 horas se utilizarán para la ejecución del experimento de formación. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para formación. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se utilizará para las ejecuciones de experimento de puntuación programada. |
| `scoringTimeframe` | Un valor de entero que representa los minutos en los que se filtrarán los datos que se utilizarán para puntuar las ejecuciones de experimento. Por ejemplo, un valor de `"10080"` significa que los datos de los últimos 10 080 minutos o 168 horas se utilizarán para cada ejecución programada del experimento de puntuación. Tenga en cuenta que un valor de `"0"` no filtrará los datos, todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `trainingSchedule` | Contiene detalles sobre las ejecuciones de experimentos de formación programadas. |
| `scoringSchedule` | Contiene detalles sobre la puntuación programada en Ejecuciones de experimento. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo se inicia la puntuación. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo se inicia la puntuación. |
| `scoringSchedule.cron` | Valor cron que indica el intervalo en el que se va a puntuar las ejecuciones de experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado. Esto incluye la variable única del servicio `id`, así como el `trainingExperimentId` y `scoringExperimentId` de sus correspondientes experimentos de formación y puntuación, respectivamente. En la respuesta de ejemplo siguiente, la presencia de `trainingSchedule` y `scoringSchedule` sugiere que las entidades Experimento para la formación y la puntuación sean experimentos programados.

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

## Buscar un servicio ML {#retrieving-ml-services}

Puede buscar un servicio ML existente realizando una `GET` solicitar a `/mlServices` y proporcionando el `id` del servicio ML en la ruta.

**Formato de API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SERVICE_ID}` | El único `id` del servicio ML que está buscando. |

**Solicitud**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML.

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
>La recuperación de diferentes servicios ML puede devolver una respuesta con más o menos pares clave-valor. La respuesta anterior es una representación de un [Servicio ML con la formación programada y la puntuación de las ejecuciones de experimento](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Programar capacitación o puntuación

Si desea programar la puntuación y la formación en un servicio ML que ya se ha publicado, puede hacerlo actualizando el servicio ML existente con un `PUT` solicitar en `/mlServices`.

**Formato de API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SERVICE_ID}` | El único `id` del servicio ML que está actualizando. |

**Solicitud**

La siguiente solicitud programa la formación y la puntuación para un servicio ML existente añadiendo la variable `trainingSchedule` y `scoringSchedule` claves con sus respectivas `startTime`, `endTime`y `cron` teclas.

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
>No intente modificar la variable `startTime` sobre los trabajos de formación y puntuación programados existentes. Si la variable `startTime` debe modificarse, considere la posibilidad de publicar el mismo modelo y de reprogramar los trabajos de formación y puntuación.

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML actualizado.

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
