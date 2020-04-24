---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicación de un modelo como servicio (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Publicación de un modelo como servicio (API)

## Requisitos previos

- Siga este [tutorial](../../tutorials/authentication.md) para obtener autorización para realizar llamadas de API a inicio.
En el tutorial debería tener la siguiente información:
   - `{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.
   - `{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.
   - `{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.
- Este tutorial requiere entidades existentes de motor ML, instancia ML y experimento. Consulte este [tutorial](./import-packaged-recipe-api.md) sobre la creación de entidades de motor ML, instancia ML o experimento.
- Para obtener información sobre los extremos de API y las solicitudes mencionadas en este tutorial, consulte la API [de aprendizaje automático](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei completa.

## Términos clave

Algunos términos comunes utilizados en este tutorial:

| Término | Definición |
--- | ---
| **Instancia de aprendizaje automático (instancia de ML)** | Entidad conceptual que es una instancia de un motor Sensei para un inquilino determinado compuesta de datos, parámetros y código Sensei específicos. |
| **Experimento** | Entidad que sirve de marco para la realización de ejecuciones de experimentos de formación, la puntuación de ejecuciones de experimentos o ambas. |
| **Experimento programado** | Término que describe la automatización de las ejecuciones de experimentos de prueba o de clasificación, regido por una programación definida por el usuario. |
| **Ejecución del experimento** | Un ejemplo particular de experimentos de capacitación o puntuación. Las ejecuciones de experimentos múltiples de un experimento en particular pueden diferir en los valores de conjuntos de datos utilizados para la formación o la puntuación. |
| **Modelo capacitado** | Modelo de aprendizaje automático creado por el proceso de experimentación y de ingeniería de funciones antes de llegar a un modelo validado, evaluado y finalizado. |
| **Modelo publicado** | Se llegó a un modelo finalizado y con versiones después de la capacitación, validación y evaluación. |
| **Servicio de aprendizaje automático (servicio ML)** | Instancia de ML implementada como servicio para admitir una solicitud de capacitación y puntuación a petición mediante un punto final. Tenga en cuenta que también se puede crear un servicio ML mediante ejecuciones de experimentos formados existentes. |


## Flujo de trabajo de API

Este tutorial pasará a crear, recuperar y actualizar un servicio ML.

## Creación de un servicio ML con una ejecución de experimentos de formación existente y una puntuación programada

Cuando publique un experimento de formación Ejecutar como un servicio ML, puede programar la puntuación proporcionando detalles para la ejecución del experimento de puntuación en `scoringSchedule` el {JSON_PAYLOAD}. Esto resulta en la creación de una entidad de Experimento programada para la puntuación. Asegúrese de que tiene los valores `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`, y de que existen y son valores válidos.

Para inicio, haga una `POST` solicitud a `/mlServices`. A continuación se muestra un comando de curva de muestra:

**Solicitud**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.
- `{IMS_ORG}` ::  El ID de organización de IMS se encuentra en los detalles de integración en la consola de Adobe I/O.
- `{ACCESS_TOKEN}` :: Su valor de token de portador específico proporcionado después de la autenticación.
- `{JSON_PAYLOAD}` :: A continuación se muestra un ejemplo de formato de carga útil JSON:

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` :: La identificación de instancia de ML existente, la ejecución del experimento de formación utilizado para crear el servicio ML, debe corresponder a esta instancia de ML concreta.
- `trainingExperimentId` :: Identificación del experimento correspondiente a la identificación de la instancia ML.
- `trainingExperimentRunId` :: Una ejecución de experimento de formación concreta que se utilizará para publicar el servicio ML.
- `scoringDataSetId` :: Identificación que hace referencia al conjunto de datos específico que se va a utilizar para las ejecuciones de experimentos de puntuación programadas.
- `scoringTimeframe` :: Un valor de entero que representa los minutos para filtrar los datos que se van a utilizar en las ejecuciones de experimentos de puntuación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para cada ejecución programada de experimentos de puntuación. Tenga en cuenta que un valor de no `"0"` filtrará los datos; todos los datos dentro del conjunto de datos se utilizan para la puntuación.
- `scoringSchedule` :: Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas.
- `startTime` :: definición.
- `endTime` :: definición.
- `cron` :: definición.

**Respuesta**

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

A partir de la respuesta JSON, la clave `scoringExperimentId` con su valor correspondiente sugiere que se ha creado un nuevo experimento de puntuación, junto con la programación del experimento proporcionada en la `POST` solicitud. La `id` clave de la respuesta identifica de forma exclusiva el servicio ML que se creó.

## Creación de un servicio ML a partir de una instancia de ML existente

Según el caso de uso y los requisitos específicos, la creación de un servicio ML con una instancia de ML es flexible en cuanto a la programación de las ejecuciones de experimentos y la puntuación. Este tutorial analizará casos específicos en los que:

- [No se requiere una formación programada, pero sí una puntuación programada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Se requieren ejecuciones de experimento programadas para la formación y la puntuación.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Tenga en cuenta que se puede crear un servicio ML con una instancia ML sin programar ningún experimento de formación o puntuación. Este servicio ML creará entidades experimentales ordinarias y un solo programa experimental para la formación y la puntuación.

### Servicio ML con experimento programado para la puntuación {#ml-service-with-scheduled-experiment-for-scoring}

La creación de un servicio ML mediante la publicación de una instancia ML con ejecuciones de experimento programadas para la puntuación dará como resultado la creación de una entidad de experimento común para la formación. La ejecución del experimento de formación resultante que se genera se utilizará para todas las ejecuciones del experimento de puntuación programadas. Asegúrese de que dispone de los `mlInstanceId`, `trainingDataSetId`y `scoringDataSetId` requeridos para la creación del servicio ML, y de que existen y son valores válidos.

Para inicio, haga una `POST` solicitud a `/mlServices`. A continuación se muestra un comando de curva de muestra:

**Solicitud**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.
- `{IMS_ORG}` ::  El ID de organización de IMS se encuentra en los detalles de integración en la consola de Adobe I/O.
- `{ACCESS_TOKEN}` :: Su valor de token de portador específico proporcionado después de la autenticación.
- `{JSON_PAYLOAD}` :: A continuación se muestra un ejemplo de formato de carga útil JSON:

```JSON
{
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
}
```

| Clave JSON | Descripción |
| --- | --- |
| **`mlInstanceId`** | Identificación de instancia de ML existente, que representa la instancia de ML utilizada para crear el servicio ML. |
| **`trainingDataSetId`** | Identificación que hace referencia al conjunto de datos específico que se utilizará para el experimento de formación. |
| **`trainingTimeframe`** | Un valor entero que representa los minutos para filtrar datos que se utilizarán en el experimento de formación. Por ejemplo, un valor de `"10080"` significa que los datos de los últimos 10.080 minutos o 168 horas se utilizarán para la ejecución del experimento de formación. Tenga en cuenta que un valor de no `"0"` filtrará los datos; todos los datos del conjunto de datos se utilizan para la formación. |
| **`scoringDataSetId`** | Identificación que hace referencia al conjunto de datos específico que se va a utilizar para las ejecuciones de experimentos de puntuación programadas. |
| **`scoringTimeframe`** | Un valor de entero que representa los minutos para filtrar los datos que se van a utilizar en las ejecuciones de experimentos de puntuación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para cada ejecución programada de experimentos de puntuación. Tenga en cuenta que un valor de no `"0"` filtrará los datos; todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| **`scoringSchedule`** | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |

**Respuesta**

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

A partir de la `JSON` respuesta, las claves `trainingExperimentId` y `scoringExperimentId` sugiere que se creó una nueva entidad Experimento de calificación y formación para este servicio ML. La presencia del `scoringSchedule` objeto hace referencia a los detalles sobre la programación de la ejecución del experimento de puntuación. La `id` clave de la respuesta se refiere al servicio ML que acaba de crear.

### Servicio ML con experimentos programados para formación y puntuación {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Para publicar una instancia de ML existente como un servicio ML con ejecuciones de experimentos de puntuación y formación programadas, debe proporcionar programas de formación y de puntuación. Cuando se crea un servicio ML de esta configuración, también se crean las entidades programadas del experimento para la formación y la puntuación. Tenga en cuenta que los programas de capacitación y puntuación no tienen por qué ser los mismos. Durante la ejecución de un trabajo de puntuación, se buscará el último modelo capacitado producido por las ejecuciones de experimentos de formación programadas y se utilizará para la ejecución de puntuación programada.

Para crear el servicio ML, realice una `POST` solicitud a `/mlServices` con la `{JSON_PAYLOAD}` representación del objeto de servicio ML que se va a agregar. Asegúrese de que `mlInstanceId`, `trainingDataSetId`y `scoringDataSetId` existe y que son valores válidos.

**Solicitud**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` :: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.
- `{IMS_ORG}` ::  El ID de organización de IMS se encuentra en los detalles de integración en la consola de Adobe I/O.
- `{ACCESS_TOKEN}` :: Su valor de token de portador específico proporcionado después de la autenticación.
- `{JSON_PAYLOAD}` :: A continuación se muestra un ejemplo de formato de carga útil JSON:

```JSON
{
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
}
```

| Clave JSON | Descripción |
| --- | --- |
| **`mlInstanceId`** | Identificación de instancia de ML existente, que representa la instancia de ML utilizada para crear el servicio ML. |
| **`trainingDataSetId`** | Identificación que hace referencia al conjunto de datos específico que se utilizará para el experimento de formación. |
| **`trainingTimeframe`** | Un valor entero que representa los minutos para filtrar datos que se utilizarán en el experimento de formación. Por ejemplo, un valor de `"10080"` significa que los datos de los últimos 10.080 minutos o 168 horas se utilizarán para la ejecución del experimento de formación. Tenga en cuenta que un valor de no `"0"` filtrará los datos; todos los datos del conjunto de datos se utilizan para la formación. |
| **`scoringDataSetId`** | Identificación que hace referencia al conjunto de datos específico que se va a utilizar para las ejecuciones de experimentos de puntuación programadas. |
| **`scoringTimeframe`** | Un valor de entero que representa los minutos para filtrar los datos que se van a utilizar en las ejecuciones de experimentos de puntuación. Por ejemplo, un valor de `"10080"` significa que se utilizarán datos de los últimos 10.080 minutos o 168 horas para cada ejecución programada de experimentos de puntuación. Tenga en cuenta que un valor de no `"0"` filtrará los datos; todos los datos dentro del conjunto de datos se utilizan para la puntuación. |
| **`trainingSchedule`** | Contiene detalles sobre las ejecuciones de experimentos de formación programadas. |
| **`scoringSchedule`** | Contiene detalles sobre las ejecuciones de experimentos de puntuación programadas. |

**Respuesta**

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

La incorporación `trainingExperimentId` y `scoringExperimentId` en el órgano de respuesta sugiere la creación de entidades de Experimento para la capacitación y la puntuación. La presencia `trainingSchedule` y `scoringSchedule` sugiere que las entidades del Experimento antes mencionadas para capacitación y puntuación son experimentos programados. La `id` clave de la respuesta se refiere al servicio ML que acaba de crear.

## Recuperación de servicios ML {#retrieving-ml-services}

Recuperar un servicio ML existente es tan sencillo como hacer una `GET` solicitud al `/mlServices` extremo. Asegúrese de tener la identificación del servicio ML para el servicio ML específico que está intentando recuperar.

**Solicitud**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` :: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.
- `{IMS_ORG}` ::  El ID de organización de IMS se encuentra en los detalles de integración en la consola de Adobe I/O.
- `{ACCESS_TOKEN}` :: Su valor de token de portador específico proporcionado después de la autenticación.

**Respuesta**

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

La respuesta JSON representa el objeto de servicio ML. Este objeto es equivalente a la respuesta para cuando se crea el servicio ML. Tenga en cuenta que la recuperación de diferentes servicios ML puede devolver una respuesta con más o menos pares de clave-valor. La respuesta anterior es una representación de un servicio [ML con la formación programada y las ejecuciones de experimentos de puntuación](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Programar formación o puntuación

Supongamos que desea programar la puntuación y la formación en un servicio ML que ya se ha publicado, puede hacerlo actualizando el servicio ML existente con una `PUT` solicitud en `/mlServices`. Asegúrese de tener la identificación del servicio ML que desea actualizar. Para su referencia, [recuperar el servicio](#retrieving-ml-services) ML que desea actualizar puede ser un primer paso útil.

**Solicitud**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` :: Identificación única que hace referencia al servicio ML que desea actualizar.
- `{API_KEY}` :: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.
- `{IMS_ORG}` ::  El ID de organización de IMS se encuentra en los detalles de integración en la consola de Adobe I/O.
- `{ACCESS_TOKEN}` :: Su valor de token de portador específico proporcionado después de la autenticación.
- `{JSON_PAYLOAD}` :: A continuación se muestra un ejemplo de formato de carga útil JSON:

```JSON
{
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
}
```

La programación de la formación y la puntuación se puede realizar agregando la `trainingSchedule` clave y `scoringSchedule` con sus respectivas `startTime`, `endTime`y `cron` teclas.

>[!NOTE] que `PUT` solicita en `mlServices` le permite modificar Servicios con ejecuciones de experimentos programados existentes. Por favor, **no intente** modificar los trabajos `startTime` de formación y puntuación programados existentes. Si `startTime` debe modificarse, considere la posibilidad de publicar el mismo modelo y reprogramar los trabajos de formación y puntuación.

**Respuesta**

La respuesta será la `{JSON_PAYLOAD}` pero con las teclas extra `id`, `created`y `updated` en el objeto.

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
