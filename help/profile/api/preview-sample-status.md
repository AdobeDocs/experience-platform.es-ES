---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API;vista previa;muestra
title: Punto final de API de previsualización de estado de muestra (previsualización de perfil)
description: El punto final de vista previa del estado de muestra de la API de Perfil del cliente en tiempo real le permite obtener una vista previa de la última muestra correcta de los datos de perfil, mostrar la distribución de perfiles por conjunto de datos y por identidad, y generar informes que muestren la superposición de conjuntos de datos, la superposición de identidades y perfiles no enlazados.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: bb2cfb479031f9e204006ba489281b389e6c6c04
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 1%

---

# Previsualizar extremo de estado de muestra (vista previa del perfil)

Adobe Experience Platform le permite introducir datos de clientes de varias fuentes para crear un perfil sólido y unificado para cada uno de sus clientes individuales. A medida que los datos se incorporan a Experience Platform, se ejecuta un trabajo de ejemplo para actualizar el recuento de perfiles y otras métricas relacionadas con los datos del perfil del cliente en tiempo real.

Los resultados de este trabajo de ejemplo se pueden ver mediante el extremo `/previewsamplestatus`, parte de la API del perfil del cliente en tiempo real. Este extremo también se puede utilizar para enumerar distribuciones de perfil por conjunto de datos y área de nombres de identidad, así como para generar varios informes con el fin de obtener visibilidad sobre la composición del almacén de perfiles de su organización. Esta guía muestra los pasos necesarios para ver estas métricas mediante el extremo de API `/previewsamplestatus`.

>[!NOTE]
>
>Hay puntos finales de estimación y previsualización disponibles como parte de la API del servicio de segmentación de Adobe Experience Platform que le permiten ver información de resumen con respecto a las definiciones de segmentos para asegurarse de aislar la audiencia esperada. Para ver los pasos detallados para trabajar con los extremos de vista previa y estimación, visite la [guía de extremos de vistas previas y estimaciones](../../segmentation/api/previews-and-estimates.md), que forma parte de la guía para desarrolladores de API [!DNL Segmentation].

## Introducción

El extremo de API utilizado en esta guía forma parte de la [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, revisa la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de [!DNL Experience Platform].

## Fragmentos de perfil frente a perfiles combinados

Esta guía hace referencia a &quot;fragmentos de perfil&quot; y a &quot;perfiles combinados&quot;. Es importante comprender la diferencia entre estos términos antes de continuar.

Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con su marca en varios canales, es probable que su organización tenga varios fragmentos de perfil relacionados con ese único cliente que aparecen en varios conjuntos de datos.

Cuando los fragmentos de perfil se incorporan en Experience Platform, se combinan (según una política de combinación) para crear un único perfil para ese cliente. Por lo tanto, es probable que el número total de fragmentos de perfil siempre sea mayor que el número total de perfiles combinados, ya que cada perfil está compuesto por varios fragmentos.

Para obtener más información sobre los perfiles y su función en Experience Platform, comience por leer la [descripción general del perfil del cliente en tiempo real](../home.md).

## Activación del trabajo de muestra

A medida que los datos habilitados para el perfil del cliente en tiempo real se incorporan en [!DNL Experience Platform], se almacenan dentro del almacén de datos del perfil. Cuando la ingesta de registros en el almacén de perfiles aumenta o disminuye el recuento total de perfiles en más del 3 %, se activa un trabajo de muestreo para actualizar el recuento. La forma en que se activa la muestra depende del tipo de ingesta que se utilice:

* Para **flujos de trabajo de datos de streaming**, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o disminución del 3 %. Si es así, se activa automáticamente un trabajo de muestra para actualizar el recuento.
* Para la **ingesta por lotes**, en los 15 minutos siguientes a la ingesta correcta de un lote en el almacén de perfiles, si se alcanza el umbral de aumento o disminución del 3 %, se ejecuta un trabajo para actualizar el recuento. Con la API de perfil puede obtener una vista previa del último trabajo de ejemplo correcto, así como una distribución de perfiles de lista por conjunto de datos y por área de nombres de identidad.

El recuento de perfiles y los perfiles por métricas de área de nombres también están disponibles en la sección [!UICONTROL Profiles] de la interfaz de usuario de Experience Platform. Para obtener información sobre cómo obtener acceso a los datos del perfil mediante la interfaz de usuario, visite la [[!DNL Profile] guía de la interfaz de usuario](../ui/user-guide.md).

## Ver el último estado de muestra {#view-last-sample-status}

Puede ver los detalles del último trabajo de ejemplo correcto que se ejecutó para su organización realizando una petición GET al extremo `/previewsamplestatus`. Este informe incluye el número total de perfiles de la muestra, así como la métrica de recuento de perfiles o el número total de perfiles que su organización tiene en Experience Platform.

El recuento de perfiles se genera después de combinar fragmentos de perfil para formar un único perfil para cada cliente individual. En otras palabras, cuando los fragmentos de perfil se combinan, devuelven un recuento de &quot;1&quot; perfiles porque todos están relacionados con el mismo individuo.

El recuento de perfiles también incluye perfiles con atributos (datos de registro), así como perfiles que solo contienen datos de series temporales (eventos), como perfiles de Adobe Analytics. El trabajo de ejemplo se actualiza regularmente a medida que se incorporan los datos del perfil para proporcionar un número total actualizado de perfiles dentro de Experience Platform.

**Formato de API**

```http
GET /previewsamplestatus
```

**Solicitud**

+++ Una solicitud de muestra para ver el último estado de muestra.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 e incluye los detalles del último trabajo de muestra correcto que se ejecutó para la organización.

+++ Una respuesta de muestra que contiene el último estado de muestra.

>[!NOTE]
>
>En esta respuesta de ejemplo, `numRowsToRead` y `totalRows` son iguales entre sí. Según el número de perfiles que tenga su organización en Experience Platform, este puede ser el caso. Sin embargo, generalmente estos dos números son diferentes, siendo `numRowsToRead` el número más pequeño porque representa la muestra como un subconjunto del número total de perfiles (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `numRowsToRead` | Número total de perfiles combinados en la muestra. |
| `sampleJobRunning` | Un valor booleano que devuelve `true` cuando un trabajo de muestra está en curso. Proporciona transparencia sobre la latencia que se produce cuando se carga un archivo por lotes en, cuando se agrega realmente al almacén de perfiles. |
| `docCount` | Recuento total de documentos en la base de datos. |
| `totalFragmentCount` | Número total de fragmentos de perfil en el almacén de perfiles. |
| `lastSuccessfulBatchTimestamp` | Marca de tiempo de la última ingesta correcta por lotes. |
| `streamingDriven` | *Este campo ha quedado obsoleto y no contiene ningún significado para la respuesta.* |
| `totalRows` | Número total de perfiles combinados en Experience Platform, también conocidos como recuento de perfiles. |
| `lastBatchId` | ID de la última ingesta por lotes. |
| `status` | Estado de la última muestra. |
| `samplingRatio` | Proporción de perfiles combinados muestreados (`numRowsToRead`) respecto al total de perfiles combinados (`totalRows`), expresada como porcentaje en formato decimal. |
| `mergeStrategy` | Estrategia de combinación utilizada en el ejemplo. |
| `lastSampledTimestamp` | Última marca de tiempo de muestra correcta. |

+++

## Enumerar la distribución de perfiles por conjunto de datos

Puede ver la distribución de perfiles por conjunto de datos realizando una petición GET al extremo `/previewsamplestatus/report/dataset`.

**Formato de API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parámetros de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la fecha, se devuelve el informe más reciente de esa fecha. Si no existe ningún informe para la fecha especificada, se devuelve el error 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. | `date=2024-12-31` |

**Solicitud**

La siguiente solicitud usa el parámetro `date` para devolver el informe más reciente para la fecha especificada.

+++ Una solicitud de ejemplo para recuperar la distribución de perfiles por conjunto de datos.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Respuesta**

>[!NOTE]
>
>Si existen varios informes para la fecha, solo se devuelve el informe más reciente. Si no existe un informe de conjunto de datos para la fecha proporcionada, se devuelve el estado HTTP 404 (no encontrado).

Una respuesta correcta devuelve el estado HTTP 200 e incluye una matriz `data`, que contiene una lista de objetos de conjunto de datos.

+++ Una respuesta de ejemplo que contiene los objetos del conjunto de datos más recientes.

>[!NOTE]
>
>La siguiente respuesta mostrada se ha truncado para mostrar tres conjuntos de datos.

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sampleCount` | Número total de perfiles combinados muestreados con este ID de conjunto de datos. |
| `samplePercentage` | `sampleCount` como porcentaje del número total de perfiles combinados muestreados (el valor `numRowsToRead` devuelto en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `fullIDsCount` | Número total de perfiles combinados con este ID de conjunto de datos. |
| `fullIDsPercentage` | `fullIDsCount` como porcentaje del número total de perfiles combinados (el valor `totalRows` devuelto en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `name` | El nombre del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `description` | La descripción del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `value` | El ID del conjunto de datos. |
| `streamingIngestionEnabled` | Si el conjunto de datos está habilitado para la ingesta de transmisión. |
| `createdUser` | El ID del usuario que creó el conjunto de datos. |
| `reportTimestamp` | La marca de tiempo del informe. Si se proporcionó un parámetro `date` durante la solicitud, el informe devuelto es para la fecha proporcionada. Si no se proporciona ningún parámetro `date`, se devuelve el informe más reciente. |

+++

## Enumerar la distribución de perfiles por área de nombres de identidad

Puede realizar una petición GET al extremo `/previewsamplestatus/report/namespace` para ver el desglose por área de nombres de identidad en todos los perfiles combinados del almacén de perfiles. Esto incluye tanto las identidades estándar proporcionadas por Adobe como las identidades personalizadas definidas por su organización.

Las áreas de nombres de identidad son un componente importante de Adobe Experience Platform Identity Service, y sirven de indicadores del contexto al que se relacionan los datos de los clientes. Para obtener más información, comience por leer la [descripción general del área de nombres de identidad](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>El número total de perfiles por área de nombres (sumando los valores mostrados para cada área de nombres) puede ser mayor que la métrica de recuento de perfiles, ya que un perfil se puede asociar con varias áreas de nombres. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias áreas de nombres a ese cliente individual.

**Formato de API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parámetros de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `date` | Especifica la fecha del informe que se va a devolver. Si se han ejecutado varios informes en la fecha, se devuelve el informe más reciente de esa fecha. Si no existe ningún informe para la fecha especificada, se devuelve el error 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: `YYYY-MM-DD`. | `date=2025-6-20` |

**Solicitud**

La siguiente solicitud no especifica un parámetro `date` y devolverá el informe más reciente.

+++ Una solicitud de ejemplo para devolver el informe más reciente para la distribución de perfiles por área de nombres. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 e incluye una matriz `data`, con objetos individuales que contienen los detalles de cada área de nombres. La respuesta mostrada se ha truncado para mostrar cuatro áreas de nombres.

+++ Una respuesta de ejemplo contiene información sobre la distribución de perfiles por área de nombres.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sampleCount` | Número total de perfiles combinados muestreados en el área de nombres. |
| `samplePercentage` | `sampleCount` como porcentaje de perfiles combinados muestreados (el valor `numRowsToRead` devuelto en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `reportTimestamp` | La marca de tiempo del informe. Si se proporcionó un parámetro `date` durante la solicitud, el informe devuelto es para la fecha proporcionada. Si no se proporciona ningún parámetro `date`, se devuelve el informe más reciente. |
| `fullIDsFragmentCount` | Número total de fragmentos de perfil en el área de nombres. |
| `fullIDsCount` | Número total de perfiles combinados en el área de nombres. |
| `fullIDsPercentage` | `fullIDsCount` como porcentaje del total de perfiles combinados (el valor `totalRows` devuelto en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `code` | El `code` del área de nombres. Esto se encuentra al trabajar con áreas de nombres mediante la [API del servicio de identidad de Adobe Experience Platform](../../identity-service/api/list-namespaces.md), y también se denomina [!UICONTROL Identity symbol] en la interfaz de usuario de Experience Platform. Para obtener más información, visite la [descripción general del área de nombres de identidad](../../identity-service/features/namespaces.md). |
| `value` | El valor `id` del área de nombres. Esto se puede encontrar al trabajar con áreas de nombres usando la [API del servicio de identidad](../../identity-service/api/list-namespaces.md). |

+++

## Enumeración de las estadísticas del conjunto de datos {#dataset-stats}

Puede generar un informe que proporcione estadísticas sobre el conjunto de datos realizando una petición GET al extremo `/previewsamplestatus/report/dataset_stats`.

**Formato de API**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Solicitud**

+++ Una solicitud de ejemplo para generar el informe de estadísticas del conjunto de datos.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre las estadísticas del conjunto de datos.

+++ Una respuesta de ejemplo que contiene información sobre las estadísticas del conjunto de datos.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para mostrar tres conjuntos de datos.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `120days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 120 días. |
| `14days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 14 días. |
| `30days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 30 días. |
| `365days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 365 días. |
| `60days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 60 días. |
| `7days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 7 días. |
| `90days` | El número de registros que permanecerán en el conjunto de datos después de una caducidad de datos de 90 días. |
| `datasetId` | El ID del conjunto de datos. |
| `datasetType` | El tipo de conjunto de datos. Este valor puede ser `Profiles` o `ExperienceEvents`. |
| `percentEvents` | El porcentaje de registros de eventos de experiencia que se encuentran dentro del conjunto de datos. |
| `percentProfiles` | El porcentaje de registros de perfil que están dentro del conjunto de datos. |
| `profileFragments` | Número total de fragmentos de perfil que existen en el conjunto de datos. |
| `records` | Número total de registros de perfil introducidos en el conjunto de datos. |
| `totalProfiles` | Número total de perfiles introducidos en el conjunto de datos. |

+++

## Obtener el tamaño del conjunto de datos {#character-count}

Puede utilizar este extremo para obtener el tamaño del conjunto de datos en bytes semana a semana.

**Formato de API**

```http
GET /previewsamplestatus/report/character_count
```

**Solicitud**

+++Una solicitud de ejemplo para generar el informe de recuento de caracteres.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/character_count \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el tamaño del conjunto de datos a lo largo de las semanas.

+++ Una respuesta de ejemplo que contiene información sobre el tamaño del conjunto de datos después de la caducidad de los datos.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para mostrar tres conjuntos de datos.

```json
{
    "data": [
        {
            "datasetIds": [
                {
                    "datasetId": "67aba91a453f7d298cd2a643",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 107773533894,
                            "week": "2025-10-26"
                        }
                    ]
                },
                {
                    "datasetId": "67aa6c867c3110298b017f0e",
                    "recordType": "timeseries",
                    "weeks": [
                        {
                            "size": 242902062440,
                            "week": "2025-10-26"
                        },
                        {
                            "size": 837539413062,
                            "week": "2025-10-19"
                        },
                        {
                            "size": 479253986484,
                            "week": "2025-10-12"
                        },
                        {
                            "size": 358911988990,
                            "week": "2025-10-05"
                        },
                        {
                            "size": 349701073042,
                            "week": "2025-09-28"
                        }
                    ]
                },
                {
                    "datasetId": "680c043667c0d7298c9ea275",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 18392459832,
                            "week": "2025-10-26"
                        }
                    ]
                }
            ],
            "modelName": "_xdm.context.profile",
            "reportTimestamp": "2025-10-30T00:28:30.069Z"
        }
    ],
    "reportTimestamp": "2025-10-30T00:28:30.069Z"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `datasetId` | El ID del conjunto de datos. |
| `recordType` | El tipo de datos dentro del conjunto de datos. El tipo de registro afecta al valor de la variable `weeks`. Los valores admitidos son `keyvalue` y `timeseries`. |
| `weeks` | Matriz que contiene la información de tamaño sobre el conjunto de datos. Para conjuntos de datos del tipo de registro `keyvalue`, contiene la semana más reciente, así como el tamaño total del conjunto de datos en bytes. Para conjuntos de datos del tipo de registro `timeseries`, contiene cada semana desde la ingesta del conjunto de datos hasta la semana más reciente y el tamaño total del conjunto de datos en bytes para cada una de esas semanas. |
| `modelName` | Nombre del modelo del conjunto de datos. Los valores posibles incluyen `_xdm.context.profile` y `_xdm.context.experienceevent`. |
| `reportTimestamp` | La fecha y la hora en que se generó el informe. |

+++

## Próximos pasos

Ahora que sabe cómo obtener una vista previa de los datos de ejemplo en el almacén de perfiles y ejecutar varios informes sobre los datos, también puede utilizar los extremos de estimación y vista previa de la API del servicio de segmentación para ver información de resumen sobre sus definiciones de segmento. Esta información le ayuda a aislar la audiencia esperada. Para obtener más información sobre cómo trabajar con vistas previas y estimaciones mediante la API de segmentación, visita la [guía de vista previa y estimación de extremos](../../segmentation/api/previews-and-estimates.md).

