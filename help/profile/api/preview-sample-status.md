---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;vista previa;ejemplo
title: Vista previa del punto final de la API de estado de muestra (vista previa del perfil)
description: Mediante el extremo de estado de muestra de vista previa, que forma parte de la API de perfil de cliente en tiempo real, puede obtener una vista previa de la muestra de éxito más reciente de los datos de perfil, mostrar la distribución de perfiles por conjunto de datos y por identidad, y generar un informe de superposición de conjuntos de datos.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 459eb626101b7382b8fe497835cc19f7d7adc6b2
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 1%

---

# Vista previa del punto final del estado de muestra (vista previa del perfil)

Adobe Experience Platform le permite introducir datos de clientes de varias fuentes para crear un perfil unificado y robusto para cada uno de sus clientes. A medida que los datos se incorporan en Platform, se ejecuta un trabajo de ejemplo para actualizar el recuento de perfiles y otras métricas relacionadas con perfiles.

Los resultados de este trabajo de muestra se pueden ver mediante el extremo `/previewsamplestatus` de la API de perfil del cliente en tiempo real. Este extremo también se puede usar para enumerar distribuciones de perfiles por conjunto de datos y área de nombres de identidad, así como para generar un informe de superposición de conjuntos de datos para ganar visibilidad en la composición del almacén de perfiles de su organización. Esta guía explica los pasos necesarios para ver estas métricas usando el extremo `/previewsamplestatus` de la API.

>[!NOTE]
>
>Hay extremos de estimación y vista previa disponibles como parte de la API del servicio de segmentación de Adobe Experience Platform que le permiten ver información de resumen sobre las definiciones de segmentos para asegurarse de que está aislando la audiencia esperada. Para encontrar pasos detallados para trabajar con la vista previa del segmento y los extremos de estimación, visite la [guía de puntos de conexión de vista previa y estimación](../../segmentation/api/previews-and-estimates.md), parte de la guía para desarrolladores de API [!DNL Segmentation].

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte la [guía de introducción](getting-started.md) para ver los vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas correctamente a cualquier API [!DNL Experience Platform].

## Fragmentos de perfil frente a perfiles combinados

Esta guía hace referencia tanto a &quot;fragmentos de perfil&quot; como a &quot;perfiles combinados&quot;. Es importante comprender la diferencia entre estos términos antes de continuar.

Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con la marca a través de varios canales, es probable que su organización tenga varios fragmentos de perfil relacionados con ese único cliente que aparecen en varios conjuntos de datos.

Cuando los fragmentos de perfil se incorporan en Platform, se combinan (según una política de combinación) para crear un único perfil para ese cliente. Por lo tanto, es probable que el número total de fragmentos de perfil sea siempre mayor que el número total de perfiles combinados, ya que cada perfil está compuesto por varios fragmentos.

Para obtener más información sobre los perfiles y su función en el Experience Platform, comience por leer la [Descripción general del perfil del cliente en tiempo real](../home.md).

## Activación del trabajo de muestra

Como los datos habilitados para el perfil del cliente en tiempo real se incorporan en [!DNL Platform], se almacenan en el almacén de datos del perfil. Cuando la ingesta de registros en el almacén de perfiles aumenta o disminuye el recuento total de perfiles en más del 5 %, se activa un trabajo de muestreo para actualizar el recuento. La forma en que se activa la muestra depende del tipo de ingesta que se utilice:

* Para **flujos de trabajo de datos de flujo continuo**, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o disminución del 5 %. Si lo ha hecho, se activa automáticamente un trabajo de muestra para actualizar el recuento.
* Para la **ingesta por lotes**, en los 15 minutos siguientes a la ingesta correcta de un lote en el almacén de perfiles, si se cumple el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento. Con la API de perfil puede obtener una vista previa del trabajo de muestra más reciente que se ha realizado correctamente, así como la distribución de perfiles de lista por conjunto de datos y por área de nombres de identidad.

El recuento de perfiles y los perfiles por métricas de espacio de nombres también están disponibles en la sección [!UICONTROL Perfiles] de la interfaz de usuario del Experience Platform. Para obtener información sobre cómo acceder a los datos de perfil mediante la interfaz de usuario, visite la [[!DNL Profile] guía de la interfaz de usuario](../ui/user-guide.md).

## Ver el último estado de muestra {#view-last-sample-status}

Puede realizar una solicitud de GET al extremo `/previewsamplestatus` para ver los detalles del último trabajo de muestra exitoso que se ejecutó para su organización IMS. Esto incluye el número total de perfiles de la muestra, así como la métrica de recuento de perfiles o el número total de perfiles que su organización tiene en Experience Platform.

El recuento de perfiles se genera después de combinar los fragmentos de perfil para formar un solo perfil para cada cliente individual. En otras palabras, cuando los fragmentos de perfil se combinan, devuelven un recuento de &quot;1&quot; perfil porque todos están relacionados con el mismo individuo.

El recuento de perfiles también incluye perfiles con atributos (datos de registro) y perfiles que solo contienen datos de series temporales (eventos), como perfiles de Adobe Analytics. El trabajo de ejemplo se actualiza regularmente a medida que se incorporan los datos de perfil para proporcionar un número total actualizado de perfiles dentro de Platform.

**Formato de API**

```http
GET /previewsamplestatus
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye los detalles del último trabajo de muestra exitoso que se ejecutó para la organización.

>[!NOTE]
>
>En esta respuesta de ejemplo, `numRowsToRead` y `totalRows` son iguales entre sí. En función del número de perfiles que tenga la organización en Experience Platform, este puede ser el caso. Sin embargo, generalmente estos dos números son diferentes, siendo `numRowsToRead` el número menor porque representa la muestra como un subconjunto del número total de perfiles (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
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
|---|---|
| `numRowsToRead` | Número total de perfiles combinados en la muestra. |
| `sampleJobRunning` | Un valor booleano que devuelve `true` cuando un trabajo de muestra está en curso. Proporciona transparencia a la latencia que se produce desde el momento en que se carga un archivo por lotes a cuando realmente se agrega al Almacenamiento de perfiles. |
| `cosmosDocCount` | Recuento total de documentos en Cosmos. |
| `totalFragmentCount` | Número total de fragmentos de perfil en el almacén de perfiles. |
| `lastSuccessfulBatchTimestamp` | Última marca de tiempo de ingesta por lotes correcta. |
| `streamingDriven` | *Este campo ha quedado obsoleto y no contiene significado para la respuesta.* |
| `totalRows` | Número total de perfiles combinados en Experience Platform, también conocidos como &quot;recuento de perfiles&quot;. |
| `lastBatchId` | Último ID de ingesta por lotes. |
| `status` | Estado de la última muestra. |
| `samplingRatio` | Proporción de perfiles combinados muestreados (`numRowsToRead`) con el total de perfiles combinados (`totalRows`), expresada como porcentaje en formato decimal. |
| `mergeStrategy` | Estrategia de combinación utilizada en el ejemplo. |
| `lastSampledTimestamp` | Última marca de tiempo de muestra correcta. |

## Enumerar la distribución de perfiles por conjunto de datos

Para ver la distribución de perfiles por conjunto de datos, puede realizar una solicitud de GET al extremo `/previewsamplestatus/report/dataset` .

**Formato de API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe a devolver. Si se ejecutaron varios informes en la fecha, se devolverá el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se devuelve un error 404. Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud utiliza el parámetro `date` para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una matriz `data`, que contiene una lista de objetos de conjunto de datos. La respuesta mostrada se ha truncado para mostrar tres conjuntos de datos.

>[!NOTE]
>
>Si existen varios informes para la fecha, solo se devuelve el informe más reciente. Si no existe un informe de conjunto de datos para la fecha proporcionada, se devuelve el estado HTTP 404 (no encontrado).

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
|---|---|
| `sampleCount` | Número total de perfiles combinados con muestra con este ID de conjunto de datos. |
| `samplePercentage` | El `sampleCount` como porcentaje del número total de perfiles combinados incluidos en la muestra (el valor `numRowsToRead` tal como se devuelve en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `fullIDsCount` | Número total de perfiles combinados con este ID de conjunto de datos. |
| `fullIDsPercentage` | El `fullIDsCount` como porcentaje del número total de perfiles combinados (el valor `totalRows` tal como se devuelve en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `name` | Nombre del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `description` | Descripción del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `value` | ID del conjunto de datos. |
| `streamingIngestionEnabled` | Indica si el conjunto de datos está habilitado para la transmisión por secuencias. |
| `createdUser` | El ID de usuario del usuario que creó el conjunto de datos. |
| `reportTimestamp` | Marca de tiempo del informe. Si se proporcionó un parámetro `date` durante la solicitud, el informe devuelto corresponde a la fecha proporcionada. Si no se proporciona ningún parámetro `date`, se devuelve el informe más reciente. |

## Enumerar la distribución de perfiles por espacio de nombres

Puede realizar una solicitud de GET al extremo `/previewsamplestatus/report/namespace` para ver el desglose por área de nombres de identidad en todos los perfiles combinados del almacén de perfiles.

Las áreas de nombres de identidad son un componente importante del servicio de identidad de Adobe Experience Platform que sirve como indicadores del contexto con el que se relacionan los datos del cliente. Para obtener más información, comience por leer la [descripción general del área de nombres de identidad](../../identity-service/namespaces.md).

>[!NOTE]
>
>El número total de perfiles por área de nombres (sumando los valores mostrados para cada área de nombres) siempre será mayor que la métrica de recuento de perfiles porque un perfil podría asociarse con varias áreas de nombres. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual.

**Formato de API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe a devolver. Si se ejecutaron varios informes en la fecha, se devolverá el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se devuelve un error 404. Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud no especifica un parámetro `date` y, por lo tanto, devuelve el informe más reciente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una matriz `data`, con objetos individuales que contienen los detalles de cada área de nombres. La respuesta mostrada se ha truncado para mostrar cuatro áreas de nombres.

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
|---|---|
| `sampleCount` | Número total de perfiles combinados muestreados en el espacio de nombres. |
| `samplePercentage` | El `sampleCount` como porcentaje de perfiles combinados muestreados (el valor `numRowsToRead` tal como se devuelve en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `reportTimestamp` | Marca de tiempo del informe. Si se proporcionó un parámetro `date` durante la solicitud, el informe devuelto corresponde a la fecha proporcionada. Si no se proporciona ningún parámetro `date`, se devuelve el informe más reciente. |
| `fullIDsFragmentCount` | El número total de fragmentos de perfil en el espacio de nombres. |
| `fullIDsCount` | Número total de perfiles combinados en el espacio de nombres. |
| `fullIDsPercentage` | El `fullIDsCount` como porcentaje del total de perfiles combinados (el valor `totalRows` tal como se devuelve en el [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `code` | El `code` del espacio de nombres. Esto se puede encontrar al trabajar con áreas de nombres mediante la [API del servicio de identidad de Adobe Experience Platform](../../identity-service/api/list-namespaces.md) y también se denomina [!UICONTROL Símbolo de identidad] en la interfaz de usuario del Experience Platform. Para obtener más información, visite [identity namespace overview](../../identity-service/namespaces.md). |
| `value` | El valor `id` del área de nombres. Esto se puede encontrar al trabajar con áreas de nombres mediante la [API del servicio de identidad](../../identity-service/api/list-namespaces.md). |

## Generar informe de superposición de conjuntos de datos

El informe de superposición de conjuntos de datos proporciona visibilidad sobre la composición del almacén de perfiles de su organización al exponer los conjuntos de datos que contribuyen más a la audiencia a la que se puede dirigir (perfiles). Además de proporcionar perspectivas sobre los datos, este informe puede ayudarle a realizar acciones para optimizar el uso de licencias, como configurar un TTL para determinados conjuntos de datos.

Puede generar el informe de superposición de conjuntos de datos realizando una solicitud de GET al extremo `/previewsamplestatus/report/dataset/overlap` .

Para obtener instrucciones paso a paso que describen cómo generar el informe de superposición de conjuntos de datos mediante la línea de comandos o la interfaz de usuario de Postman, consulte el tutorial [Generación del informe de superposición de conjuntos de datos](../tutorials/dataset-overlap-report.md).

**Formato de API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe a devolver. Si se ejecutaron varios informes en la misma fecha, se devuelve el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se devuelve un error 404 (No encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud utiliza el parámetro `date` para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una solicitud correcta devuelve Estado HTTP 200 (OK) y el informe de superposición de conjuntos de datos.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Propiedad | Descripción |
|---|---|
| `data` | El objeto `data` contiene listas de conjuntos de datos separados por coma y sus respectivos recuentos de perfiles. |
| `reportTimestamp` | Marca de tiempo del informe. Si se proporcionó un parámetro `date` durante la solicitud, el informe devuelto corresponde a la fecha proporcionada. Si no se proporciona ningún parámetro `date`, se devuelve el informe más reciente. |

Los resultados del informe se pueden interpretar desde los conjuntos de datos y recuentos de perfiles de la respuesta. Consideremos el siguiente objeto de informe de ejemplo `data`:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Este informe proporciona la siguiente información:
* Hay 123 perfiles compuestos de datos procedentes de los siguientes conjuntos de datos: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Hay 454.412 perfiles compuestos de datos procedentes de estos dos conjuntos de datos: `5d92921872831c163452edc8` y `5eb2cdc6fa3f9a18a7592a98`.
* Hay 107 perfiles que están compuestos solamente de datos del conjunto de datos `5eeda0032af7bb19162172a7`.
* Hay un total de 454.642 perfiles en la organización.

## Pasos siguientes

Ahora que sabe cómo obtener una vista previa de los datos de ejemplo en el Almacenamiento de perfiles y ejecutar el informe de superposición de conjuntos de datos, también puede utilizar los extremos de estimación y vista previa de la API del servicio de segmentación para ver información de resumen sobre las definiciones de segmentos. Esta información ayuda a garantizar que está aislando la audiencia esperada en el segmento. Para obtener más información sobre cómo trabajar con vistas previas y estimaciones de segmentos mediante la API de segmentación, visite la [guía de vista previa y estimación de extremos](../../segmentation/api/previews-and-estimates.md).

