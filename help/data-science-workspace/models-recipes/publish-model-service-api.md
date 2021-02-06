---
keywords: Experience Platform;publicar un modelo;Área de trabajo de ciencia de datos;temas populares;API de aprendizaje del equipo sensei
solution: Experience Platform
title: Publicación de un modelo como servicio mediante la API de aprendizaje automático de Sensei
topic: tutorial
type: Tutorial
description: Este tutorial trata el proceso de publicación de un modelo como servicio mediante la API de aprendizaje automático Sensei.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---


# Publique un modelo como servicio mediante [!DNL Sensei Machine Learning API]

Este tutorial trata el proceso de publicación de un modelo como servicio mediante el [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de Adobe Experience Platform Data Science Workspace. Antes de comenzar este tutorial, consulte la [información general de Área de trabajo de ciencia de datos](../home.md) para obtener una introducción de alto nivel al servicio.

Para seguir este tutorial, debe tener un motor ML, una instancia de ML y un experimento. Para ver los pasos para crearlos en la API, consulte el tutorial sobre [importación de una fórmula empaquetada](./import-packaged-recipe-api.md).

Por último, antes de iniciar este tutorial, consulte la sección [introducción](../api/getting-started.md) de la guía para desarrolladores para obtener información importante que necesita conocer a fin de realizar llamadas exitosas a la API [!DNL Sensei Machine Learning], incluidos los encabezados necesarios que se utilizan en este tutorial:

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

### Términos clave

En la tabla siguiente se describe una terminología común utilizada en este tutorial:

| Término | Definición |
--- | ---
| **Instancia de aprendizaje automático (instancia de ML)** | Instancia de un motor [!DNL Sensei] para un inquilino en particular, que contiene datos, parámetros y código [!DNL Sensei] específicos. |
| **Experimento** | Entidad que sirve de marco para la realización de ejecuciones de experimentos de formación, la puntuación de ejecuciones de experimentos o ambas. |
| **Experimento programado** | Término que describe la automatización de las ejecuciones de experimentos de prueba o de clasificación, regido por una programación definida por el usuario. |
| **Ejecución del experimento** | Un ejemplo particular de experimentos de capacitación o puntuación. Las ejecuciones de experimentos múltiples de un experimento en particular pueden diferir en los valores de conjuntos de datos utilizados para la formación o la puntuación. |
| **Modelo capacitado** | Modelo de aprendizaje automático creado por el proceso de experimentación y de ingeniería de funciones antes de llegar a un modelo validado, evaluado y finalizado. |
| **Modelo publicado** | Se llegó a un modelo finalizado y con versiones después de la capacitación, validación y evaluación. |
| **Servicio de aprendizaje automático (servicio ML)** | Instancia de ML implementada como servicio para admitir solicitudes de capacitación y puntuación bajo demanda mediante un punto final de API. También se puede crear un servicio ML mediante las ejecuciones de experimentos formadas existentes. |

## Crear un servicio ML con una ejecución de experimentos de formación existente y una puntuación programada

Al publicar un experimento de formación Ejecutar como un servicio ML, puede programar la puntuación proporcionando detalles para el experimento de puntuación Ejecutar la carga útil de una solicitud de POST. Esto resulta en la creación de una entidad de Experimento programada para la puntuación.

**Formato API**

```http
POST /mlServices
```

**Solicitud**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
--- | ---
| `mlInstanceId` | La identificación de instancia de ML existente, la ejecución del experimento de formación utilizado para crear el servicio ML, debe corresponder a esta instancia de ML concreta. |
| `trainingExperimentId` | Identificación del experimento correspondiente a la identificación de la instancia ML. |
| `trainingExperimentRunId` | Una ejecución de experimento de formación concreta que se utilizará para publicar el servicio ML. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se va a utilizar para las ejecuciones de experimentos de puntuación programadas. |
| `scoringTimeframe` | Un valor de entero que representa los minutos para filtrar los datos que se van a utilizar en las ejecuciones de experimentos de puntuación. Por ejemplo, un valor de `10080` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para cada ejecución programada del experimento de puntuación. Tenga en cuenta que un valor de `0` no filtrará los datos; todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `scoringSchedule` | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo se va a realizar una puntuación de inicio. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo se va a realizar una puntuación de inicio. |
| `scoringSchedule.cron` | Valor cron que indica el intervalo por el que se puntúa la ejecución del experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado, incluyendo su `id` único y el `scoringExperimentId` para su correspondiente experimento de puntuación.


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

Según el caso de uso y los requisitos específicos, la creación de un servicio ML con una instancia de ML es flexible en cuanto a la programación de las ejecuciones de experimentos y la puntuación. Este tutorial analizará casos específicos en los que:

- [No se requiere una formación programada, pero sí una puntuación programada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Se requieren ejecuciones de experimento programadas para la formación y la puntuación.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Tenga en cuenta que se puede crear un servicio ML con una instancia ML sin programar ningún experimento de formación o puntuación. Estos servicios de ML crearán entidades experimentales ordinarias y un solo programa experimental para la formación y la puntuación.

### Servicio ML con experimento programado para la puntuación {#ml-service-with-scheduled-experiment-for-scoring}

Puede crear un servicio ML mediante la publicación de una instancia de ML con ejecuciones de experimentos programadas para la puntuación, que creará una entidad de experimento común para la formación. Se genera una ejecución de experimento de formación que se utilizará en todas las ejecuciones de experimento de puntuación programadas. Asegúrese de que tiene los `mlInstanceId`, `trainingDataSetId` y `scoringDataSetId` requeridos para la creación del servicio ML, y de que existen y son valores válidos.

**Formato API**

```http
POST /mlServices
```

**Solicitud**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `trainingTimeframe` | Un valor entero que representa los minutos para filtrar datos que se utilizarán en el experimento de formación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para la ejecución del experimento de formación. Tenga en cuenta que un valor de `"0"` no filtrará los datos; todos los datos del conjunto de datos se utilizan para la capacitación. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se va a utilizar para las ejecuciones de experimentos de puntuación programadas. |
| `scoringTimeframe` | Un valor de entero que representa los minutos para filtrar los datos que se van a utilizar en las ejecuciones de experimentos de puntuación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para cada ejecución programada del experimento de puntuación. Tenga en cuenta que un valor de `"0"` no filtrará los datos; todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `scoringSchedule` | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo se va a realizar una puntuación de inicio. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo se va a realizar una puntuación de inicio. |
| `scoringSchedule.cron` | Valor cron que indica el intervalo por el que se puntúa la ejecución del experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado. Esto incluye los `id` únicos del servicio, así como los `trainingExperimentId` y `scoringExperimentId` para sus correspondientes experimentos de capacitación y puntuación, respectivamente.

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

### Servicio ML con experimentos programados para entrenamiento y puntuación {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Para publicar una instancia de ML existente como un servicio ML con ejecuciones de experimentos de puntuación y formación programadas, debe proporcionar programas de formación y de puntuación. Cuando se crea un servicio ML de esta configuración, también se crean las entidades programadas de Experimento para la formación y la puntuación. Tenga en cuenta que los programas de capacitación y puntuación no tienen por qué ser los mismos. Durante la ejecución de un trabajo de puntuación, se buscará el último modelo capacitado producido por las ejecuciones de experimentos de formación programadas y se utilizará para la ejecución de puntuación programada.

**Formato API**

```http
POST /mlServices
```

**Solicitud**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `trainingTimeframe` | Un valor entero que representa los minutos para filtrar datos que se utilizarán en el experimento de formación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para la ejecución del experimento de formación. Tenga en cuenta que un valor de `"0"` no filtrará los datos; todos los datos del conjunto de datos se utilizan para la capacitación. |
| `scoringDataSetId` | Identificación que hace referencia al conjunto de datos específico que se va a utilizar para las ejecuciones de experimentos de puntuación programadas. |
| `scoringTimeframe` | Un valor de entero que representa los minutos para filtrar los datos que se van a utilizar en las ejecuciones de experimentos de puntuación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para cada ejecución programada del experimento de puntuación. Tenga en cuenta que un valor de `"0"` no filtrará los datos; todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| `trainingSchedule` | Contiene detalles sobre las ejecuciones de experimentos de formación programadas. |
| `scoringSchedule` | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |
| `scoringSchedule.startTime` | Fecha y hora que indica cuándo se va a realizar una puntuación de inicio. |
| `scoringSchedule.endTime` | Fecha y hora que indica cuándo se va a realizar una puntuación de inicio. |
| `scoringSchedule.cron` | Valor cron que indica el intervalo por el que se puntúa la ejecución del experimento. |

**Respuesta**

Una respuesta correcta devuelve los detalles del servicio ML recién creado. Esto incluye el `id` único del servicio, así como los `trainingExperimentId` y `scoringExperimentId` de los experimentos de capacitación y puntuación correspondientes, respectivamente. En la respuesta de ejemplo siguiente, la presencia de `trainingSchedule` y `scoringSchedule` sugiere que las entidades de Experimento para la capacitación y la puntuación son experimentos programados.

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

Puede buscar un servicio ML existente haciendo una solicitud `GET` a `/mlServices` y proporcionando el `id` único del servicio ML en la ruta.

**Formato API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SERVICE_ID}` | El `id` único del servicio ML que está buscando. |

**Solicitud**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>Recuperar diferentes servicios ML puede devolver una respuesta con más o menos pares de clave-valor. La respuesta anterior es una representación de un [servicio ML con la capacitación programada y las ejecuciones de experimentos de puntuación](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Programar formación o puntuación

Si desea programar la puntuación y la formación en un servicio ML que ya se ha publicado, puede hacerlo actualizando el servicio ML existente con una solicitud `PUT` en `/mlServices`.

**Formato API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SERVICE_ID}` | El `id` único del servicio ML que está actualizando. |

**Solicitud**

La siguiente solicitud programa la capacitación y la puntuación de un servicio ML existente agregando las claves `trainingSchedule` y `scoringSchedule` con sus respectivas claves `startTime`, `endTime` y `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>No intente modificar el `startTime` en los trabajos de puntuación y formación programados existentes. Si se debe modificar `startTime`, considere la posibilidad de publicar el mismo modelo y reprogramar los trabajos de formación y puntuación.

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
