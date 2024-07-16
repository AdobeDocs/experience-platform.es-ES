---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Punto final de API de métricas
description: Aprenda a recuperar métricas de observabilidad en Experience Platform mediante la API de Observability Insights.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 3%

---

# Extremo de métricas

Las métricas de observabilidad proporcionan perspectivas sobre las estadísticas de uso, las tendencias históricas y los indicadores de rendimiento de varias funciones de Adobe Experience Platform. El extremo `/metrics` en [!DNL Observability Insights API] le permite recuperar mediante programación datos de métricas para la actividad de su organización en [!DNL Platform].

>[!NOTE]
>
>La versión anterior del extremo de métricas (V1) ha quedado obsoleta. Este documento se centra exclusivamente en la versión actual (V2). Para obtener más información sobre el extremo V1 para implementaciones heredadas, consulte la [referencia de API](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Introducción

El extremo de API utilizado en esta guía forma parte de la [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de [!DNL Experience Platform].

## Recuperar métricas de observabilidad

Puede recuperar datos de métricas realizando una solicitud de POST al extremo `/metrics`, especificando las métricas que desea recuperar en la carga útil.

**Formato de API**

```http
POST /metrics
```

**Solicitud**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `start` | La primera fecha y hora a partir de la cual se recuperarán los datos de la métrica. |
| `end` | La última fecha y hora a partir de la cual se recuperarán los datos de la métrica. |
| `granularity` | Campo opcional que indica el intervalo de tiempo por el que se dividen los datos de la métrica. Por ejemplo, un valor de `DAY` devuelve métricas para cada día entre las fechas `start` y `end`, mientras que un valor de `MONTH` agruparía los resultados de las métricas por mes en su lugar. Al utilizar este campo, también se debe proporcionar una propiedad `downsample` correspondiente para indicar la función de agregación mediante la cual se van a agrupar los datos. |
| `metrics` | Una matriz de objetos, uno para cada métrica que desee recuperar. |
| `name` | El nombre de una métrica reconocida por Observability Insights. Consulte el [apéndice](#available-metrics) para obtener una lista completa de los nombres de métricas aceptados. |
| `filters` | Campo opcional que le permite filtrar métricas por conjuntos de datos específicos. El campo es una matriz de objetos (uno para cada filtro), cada uno de los cuales contiene las siguientes propiedades: <ul><li>`name`: tipo de entidad con la que filtrar las métricas. Actualmente, solo se admite `dataSets`.</li><li>`value`: ID de uno o más conjuntos de datos. Se pueden proporcionar varios ID de conjunto de datos como una sola cadena, con cada ID separado por caracteres de barra vertical (`\|`).</li><li>`groupBy`: cuando se establece en true, indica que el `value` correspondiente representa varios conjuntos de datos cuyos resultados de métricas deben devolverse por separado. Si se establece en false, los resultados de las métricas de esos conjuntos de datos se agrupan.</li></ul> |
| `aggregator` | Especifica la función de agregación que debe utilizarse para agrupar varios registros de series temporales en resultados únicos. Para obtener información detallada sobre los agregadores disponibles, consulte la [documentación de OpenTSDB](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |
| `downsample` | Campo opcional que permite especificar una función de agregación para reducir la tasa de muestreo de los datos de métricas ordenando los campos en intervalos (o &quot;contenedores&quot;). El intervalo para la disminución de resolución viene determinado por la propiedad `granularity`. Para obtener información detallada sobre la disminución de resolución, consulte la [documentación de OpenTSDB](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los puntos de datos resultantes para las métricas y filtros especificados en la solicitud.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `metricResponses` | Una matriz cuyos objetos representen cada una de las métricas especificadas en la solicitud. Cada objeto contiene información sobre la configuración del filtro y los datos de métricas devueltos. |
| `metric` | El nombre de una de las métricas proporcionadas en la solicitud. |
| `filters` | La configuración del filtro para la métrica especificada. |
| `datapoints` | Matriz cuyos objetos representan los resultados de la métrica y los filtros especificados. El número de objetos de la matriz depende de las opciones de filtro proporcionadas en la solicitud. Si no se proporcionó ningún filtro, la matriz solo contendrá un único objeto que representa todos los conjuntos de datos. |
| `groupBy` | Si se especificaron varios conjuntos de datos en la propiedad `filter` para una métrica y la opción `groupBy` se estableció en true en la solicitud, este objeto contendrá el ID del conjunto de datos al que se aplica la propiedad `dps` correspondiente.<br><br>Si este objeto aparece vacío en la respuesta, la propiedad `dps` correspondiente se aplica a todos los conjuntos de datos proporcionados en la matriz `filters` (o a todos los conjuntos de datos de [!DNL Platform] si no se proporcionaron filtros). |
| `dps` | Los datos devueltos para la métrica, el filtro y el intervalo de tiempo dados. Cada clave de este objeto representa una marca de tiempo con un valor correspondiente para la métrica especificada. El período de tiempo entre cada punto de datos depende del valor `granularity` especificado en la solicitud. |

{style="table-layout:auto"}

## Apéndice

La siguiente sección contiene información adicional sobre cómo trabajar con el extremo `/metrics`.

### Métricas disponibles {#available-metrics}

Las tablas siguientes enumeran todas las métricas expuestas por [!DNL Observability Insights], desglosadas por el servicio [!DNL Platform]. Cada métrica incluye una descripción y un parámetro de consulta de ID aceptado.

>[!NOTE]
>
>Todos los parámetros de consulta de ID enumerados son opcionales a menos que se indique lo contrario.

#### [!DNL Data Ingestion] {#ingestion}

En la tabla siguiente se describen las métricas de Adobe Experience Platform [!DNL Data Ingestion]. Las métricas de **bold** son métricas de ingesta de transmisión.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Tamaño acumulado de todos los datos introducidos para un conjunto de datos para o todos los conjuntos de datos. | ID de conjunto de datos |
| timeseries.ingestion.dataset.dailysize | Tamaño de los datos introducidos diariamente para un conjunto de datos o para todos. | ID de conjunto de datos |
| timeseries.ingestion.dataset.batchfailed.count | Error en el número de lotes para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes introducidos para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros ingeridos para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| **series de tiempo.data.collection.validation.category.presence.count** | Número total de mensajes de &quot;presencia&quot; no válidos para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| **series de tiempo.data.collection.inlet.total.messages.received** | Número total de mensajes recibidos para una entrada de datos o para todas. | ID de entrada |
| **series de tiempo.data.collection.inlet.total.messages.size.received** | Tamaño total de los datos recibidos para una entrada de datos o para todas. | ID de entrada |
| **series de tiempo.data.collection.inlet.success** | Número total de llamadas HTTP correctas a una entrada o a todas las entradas de datos. | ID de entrada |
| **series de tiempo.data.collection.inlet.failure** | Número total de llamadas HTTP fallidas a una entrada de datos o a todas las entradas de datos. | ID de entrada |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

En la tabla siguiente se describen las métricas de Adobe Experience Platform [!DNL Identity Service].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros escritos en su origen de datos por [!DNL Identity Service], para un conjunto de datos o todos ellos. | ID de conjunto de datos |
| timeseries.identity.dataset.recordfailed.count | Número de registros con error de [!DNL Identity Service], para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidad erróneos por un área de nombres. | Id. de área de nombres (**Requerido**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidad omitidos por un área de nombres. | Id. de área de nombres (**Requerido**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidades de su organización. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de un área de nombres. | Id. de área de nombres (**Requerido**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de su organización para una intensidad de gráfico determinada (&quot;desconocida&quot;, &quot;débil&quot; o &quot;fuerte&quot;). | Intensidad del gráfico (**Requerido**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

La tabla siguiente describe las métricas de [!DNL Real-Time Customer Profile].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros leídos de [!DNL Data Lake] por [!DNL Profile], para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros escritos en su origen de datos por [!DNL Profile], para un conjunto de datos o para todos ellos. | ID de conjunto de datos |
| timeseries.profiles.dataset.batchsuccess.count | Número de [!DNL Profile] lotes ingeridos para un conjunto de datos o para todos ellos. | ID de conjunto de datos |

{style="table-layout:auto"}

### Mensajes de error

Las respuestas del extremo `/metrics` pueden devolver mensajes de error en ciertas condiciones. Estos mensajes de error se devuelven en el siguiente formato:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `title` | Una cadena que contiene el mensaje de error y el motivo potencial por el que puede haberse producido. |
| `report` | Contiene información contextual sobre el error, incluida la zona protegida y la organización que se está utilizando en la operación que lo activó. |

{style="table-layout:auto"}

En la tabla siguiente se enumeran los diferentes códigos de error que puede devolver la API:

| Código de error | Título | Descripción |
| --- | --- | --- |
| `INSGHT-1000-400` | Carga útil de solicitud incorrecta | Error en la carga útil de la solicitud. Asegúrese de que coincide con el formato de la carga útil exactamente como se muestra [arriba](#v2). Cualquiera de las posibles razones puede almacenar en déclencheur este error:<ul><li>Faltan campos obligatorios como `aggregator`</li><li>Métricas no válidas</li><li>La solicitud contiene un acumulador no válido</li><li>La fecha de inicio es posterior a la de finalización</li></ul> |
| `INSGHT-1001-400` | Error de consulta de métricas | Se ha producido un error al intentar consultar la base de datos de métricas debido a una solicitud incorrecta o a que la consulta en sí no se puede analizar. Asegúrese de que la solicitud tenga el formato correcto antes de intentarlo de nuevo. |
| `INSGHT-1001-500` | Error de consulta de métricas | Se ha producido un error al intentar consultar la base de datos de métricas, debido a un error del servidor. Vuelva a intentar la solicitud y, si el problema persiste, póngase en contacto con el servicio de soporte técnico del Adobe. |
| `INSGHT-1002-500` | Error de servicio | La solicitud no se ha podido procesar debido a un error interno. Vuelva a intentar la solicitud y, si el problema persiste, póngase en contacto con el servicio de soporte técnico del Adobe. |
| `INSGHT-1003-401` | Error de validación de zona protegida | La solicitud no se ha podido procesar debido a un error de validación de zona protegida. Asegúrese de que el nombre de la zona protegida que ha proporcionado en el encabezado `x-sandbox-name` represente una zona protegida válida y habilitada para su organización antes de volver a intentar la solicitud. |

{style="table-layout:auto"}
