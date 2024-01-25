---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API;vista previa;muestra
title: Punto final de API de previsualización de estado de muestra (previsualización de perfil)
description: El punto final de vista previa del estado de muestra de la API de Perfil del cliente en tiempo real le permite obtener una vista previa de la última muestra correcta de los datos de perfil, mostrar la distribución de perfiles por conjunto de datos y por identidad, y generar informes que muestren la superposición de conjuntos de datos, la superposición de identidades y perfiles no enlazados.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2906'
ht-degree: 1%

---

# Previsualizar extremo de estado de muestra (vista previa del perfil)

Adobe Experience Platform le permite introducir datos de clientes de varias fuentes para crear un perfil sólido y unificado para cada uno de sus clientes individuales. A medida que los datos se incorporan a Platform, se ejecuta un trabajo de muestra para actualizar el recuento de perfiles y otras métricas relacionadas con los datos del perfil del cliente en tiempo real.

Los resultados de este trabajo de muestra se pueden ver mediante el `/previewsamplestatus` punto de conexión, parte de la API del perfil del cliente en tiempo real. Este extremo también se puede utilizar para enumerar distribuciones de perfil por conjunto de datos y área de nombres de identidad, así como para generar varios informes con el fin de obtener visibilidad sobre la composición del almacén de perfiles de su organización. En esta guía se explican los pasos necesarios para ver estas métricas con la variable `/previewsamplestatus` Extremo de API.

>[!NOTE]
>
>Hay puntos finales de estimación y previsualización disponibles como parte de la API del servicio de segmentación de Adobe Experience Platform que le permiten ver información de resumen con respecto a las definiciones de segmentos para asegurarse de aislar la audiencia esperada. Para encontrar los pasos detallados para trabajar con los extremos de vista previa y estimación, visite la [guía de extremos de previsualizaciones y estimaciones](../../segmentation/api/previews-and-estimates.md), parte de [!DNL Segmentation] Guía para desarrolladores de API.

## Introducción

El extremo de API utilizado en esta guía forma parte del [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte la [guía de introducción](getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier [!DNL Experience Platform] API.

## Fragmentos de perfil frente a perfiles combinados

Esta guía hace referencia a &quot;fragmentos de perfil&quot; y a &quot;perfiles combinados&quot;. Es importante comprender la diferencia entre estos términos antes de continuar.

Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con su marca en varios canales, es probable que su organización tenga varios fragmentos de perfil relacionados con ese único cliente que aparecen en varios conjuntos de datos.

Cuando los fragmentos de perfil se incorporan en Platform, se combinan (según una política de combinación) para crear un único perfil para ese cliente. Por lo tanto, es probable que el número total de fragmentos de perfil siempre sea mayor que el número total de perfiles combinados, ya que cada perfil está compuesto por varios fragmentos.

Para obtener más información sobre los perfiles y su función dentro del Experience Platform, comience por leer el [Resumen del perfil del cliente en tiempo real](../home.md).

## Activación del trabajo de muestra

A medida que los datos habilitados para Perfil del cliente en tiempo real se incorporan en [!DNL Platform], se almacena en el almacén de datos de perfil. Cuando la ingesta de registros en el Almacenamiento de perfiles aumenta o disminuye el recuento total de perfiles en más del 5 %, se activa un trabajo de muestreo para actualizar el recuento. La forma en que se activa la muestra depende del tipo de ingesta que se utilice:

* Para **flujos de trabajo de datos**, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o disminución del 5 %. Si es así, se activa automáticamente un trabajo de muestra para actualizar el recuento.
* Para **ingesta por lotes**, en los 15 minutos siguientes a la ingesta correcta de un lote en el almacén de perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento. Con la API de perfil puede obtener una vista previa del último trabajo de ejemplo correcto, así como una distribución de perfiles de lista por conjunto de datos y por área de nombres de identidad.

El recuento de perfiles y los perfiles por métricas de área de nombres también están disponibles en la variable [!UICONTROL Perfiles] de la interfaz de usuario de Experience Platform. Para obtener información sobre cómo acceder a los datos de perfil mediante la interfaz de usuario de, visite [[!DNL Profile] Guía de IU](../ui/user-guide.md).

## Ver el último estado de muestra {#view-last-sample-status}

Puede realizar una solicitud de GET a `/previewsamplestatus` extremo para ver los detalles del último trabajo de muestra correcto que se ejecutó para su organización. Esto incluye el número total de perfiles en la muestra, así como la métrica de recuento de perfiles o el número total de perfiles que su organización tiene dentro del Experience Platform.

El recuento de perfiles se genera después de combinar fragmentos de perfil para formar un único perfil para cada cliente individual. En otras palabras, cuando los fragmentos de perfil se combinan, devuelven un recuento de &quot;1&quot; perfiles porque todos están relacionados con el mismo individuo.

El recuento de perfiles también incluye perfiles con atributos (datos de registro), así como perfiles que solo contienen datos de series temporales (eventos), como perfiles de Adobe Analytics. El trabajo de muestra se actualiza regularmente a medida que se incorporan los datos del perfil para proporcionar un número total actualizado de perfiles dentro de Platform.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye los detalles del último trabajo de muestra correcto que se ejecutó para la organización.

>[!NOTE]
>
>En esta respuesta de ejemplo, `numRowsToRead` y `totalRows` son iguales entre sí. Según el número de perfiles que tenga su organización en Experience Platform, este puede ser el caso. Sin embargo, generalmente estos dos números son diferentes, con `numRowsToRead` siendo el número menor porque representa la muestra como un subconjunto del número total de perfiles (`totalRows`).

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
| `sampleJobRunning` | Un valor booleano que devuelve `true` cuando hay un trabajo de muestra en curso. Proporciona transparencia sobre la latencia que se produce cuando se carga un archivo por lotes en, cuando se agrega realmente al Almacenamiento de perfiles. |
| `cosmosDocCount` | Recuento total de documentos en Cosmos. |
| `totalFragmentCount` | Número total de fragmentos de perfil en el almacén de perfiles. |
| `lastSuccessfulBatchTimestamp` | Marca de tiempo de la última ingesta correcta por lotes. |
| `streamingDriven` | *Este campo ha quedado obsoleto y no contiene ningún significado para la respuesta.* |
| `totalRows` | Número total de perfiles combinados en Experience Platform, también conocidos como &quot;recuento de perfiles&quot;. |
| `lastBatchId` | ID de la última ingesta por lotes. |
| `status` | Estado de la última muestra. |
| `samplingRatio` | Proporción de perfiles combinados muestreados (`numRowsToRead`) al total de perfiles combinados (`totalRows`), expresado como porcentaje en formato decimal. |
| `mergeStrategy` | Estrategia de combinación utilizada en el ejemplo. |
| `lastSampledTimestamp` | Última marca de tiempo de muestra correcta. |

## Enumerar la distribución de perfiles por conjunto de datos

Para ver la distribución de perfiles por conjunto de datos, puede realizar una solicitud de GET al `/previewsamplestatus/report/dataset` punto final.

**Formato de API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la fecha, se devuelve el informe más reciente de esa fecha. Si no existe ningún informe para la fecha especificada, se devuelve el error 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud utiliza el `date` para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una `data` matriz, que contiene una lista de objetos del conjunto de datos. La respuesta mostrada se ha truncado para mostrar tres conjuntos de datos.

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
| `sampleCount` | Número total de perfiles combinados muestreados con este ID de conjunto de datos. |
| `samplePercentage` | El `sampleCount` como porcentaje del número total de perfiles combinados muestreados (la variable `numRowsToRead` como se devuelve en la variable [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `fullIDsCount` | Número total de perfiles combinados con este ID de conjunto de datos. |
| `fullIDsPercentage` | El `fullIDsCount` como porcentaje del número total de perfiles combinados (la variable `totalRows` como se devuelve en la variable [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `name` | El nombre del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `description` | La descripción del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `value` | El ID del conjunto de datos. |
| `streamingIngestionEnabled` | Si el conjunto de datos está habilitado para la ingesta de transmisión. |
| `createdUser` | El ID del usuario que creó el conjunto de datos. |
| `reportTimestamp` | La marca de tiempo del informe. Si un `date` se ha proporcionado durante la solicitud, el informe devuelto es para la fecha proporcionada. Si no `date` Si se proporciona el parámetro, se devuelve el informe más reciente. |

## Enumerar la distribución de perfiles por área de nombres de identidad

Puede realizar una solicitud de GET a `/previewsamplestatus/report/namespace` punto de conexión para ver el desglose por área de nombres de identidad en todos los perfiles combinados del almacén de perfiles. Esto incluye tanto las identidades estándar proporcionadas por Adobe como las identidades personalizadas definidas por su organización.

Las áreas de nombres de identidad son un componente importante de Adobe Experience Platform Identity Service, y sirven de indicadores del contexto al que se relacionan los datos de los clientes. Para obtener más información, comience por leer el [información general del área de nombres de identidad](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>El número total de perfiles por área de nombres (sumando los valores mostrados para cada área de nombres) puede ser mayor que la métrica de recuento de perfiles, ya que un perfil se puede asociar con varias áreas de nombres. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias áreas de nombres a ese cliente individual.

**Formato de API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la fecha, se devuelve el informe más reciente de esa fecha. Si no existe ningún informe para la fecha especificada, se devuelve el error 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud no especifica un `date` y, por lo tanto, devuelve el informe más reciente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una `data` , con objetos individuales que contienen los detalles de cada área de nombres. La respuesta mostrada se ha truncado para mostrar cuatro áreas de nombres.

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
| `sampleCount` | Número total de perfiles combinados muestreados en el área de nombres. |
| `samplePercentage` | El `sampleCount` como porcentaje de perfiles combinados muestreados (la variable `numRowsToRead` como se devuelve en la variable [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `reportTimestamp` | La marca de tiempo del informe. Si un `date` se ha proporcionado durante la solicitud, el informe devuelto es para la fecha proporcionada. Si no `date` Si se proporciona el parámetro, se devuelve el informe más reciente. |
| `fullIDsFragmentCount` | Número total de fragmentos de perfil en el área de nombres. |
| `fullIDsCount` | Número total de perfiles combinados en el área de nombres. |
| `fullIDsPercentage` | El `fullIDsCount` como porcentaje del total de perfiles combinados (la variable `totalRows` como se devuelve en la variable [último estado de muestra](#view-last-sample-status)), expresado en formato decimal. |
| `code` | El `code` para el área de nombres. Esto se puede encontrar al trabajar con áreas de nombres utilizando [API del servicio de identidad de Adobe Experience Platform](../../identity-service/api/list-namespaces.md) y también se denomina la variable [!UICONTROL Símbolo de identidad] en la interfaz de usuario de Experience Platform. Para obtener más información, visite la [información general del área de nombres de identidad](../../identity-service/features/namespaces.md). |
| `value` | El `id` valor del área de nombres. Esto se puede encontrar al trabajar con áreas de nombres utilizando [API del servicio de identidad](../../identity-service/api/list-namespaces.md). |

## Generar el informe de superposición de conjuntos de datos

El informe de superposición de conjuntos de datos proporciona visibilidad de la composición del Almacenamiento de perfiles de su organización al exponer los conjuntos de datos que más contribuyen a su audiencia direccionable (perfiles combinados). Además de proporcionar perspectivas sobre sus datos, este informe puede ayudarle a realizar acciones para optimizar el uso de las licencias, como configurar las caducidades de ciertos conjuntos de datos.

GET Puede generar el informe de superposición de conjuntos de datos realizando una solicitud al `/previewsamplestatus/report/dataset/overlap` punto final.

Para obtener instrucciones paso a paso sobre cómo generar el informe de superposición de conjuntos de datos mediante la línea de comandos o la interfaz de usuario de Postman, consulte la [tutorial generación del informe de superposición de conjuntos de datos](../tutorials/dataset-overlap-report.md).

**Formato de API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la misma fecha, se devuelve el informe más reciente de esa fecha. Si no existe ningún informe para la fecha especificada, se devuelve el error 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud utiliza el `date` para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una solicitud correcta devuelve el estado HTTP 200 (OK) y el informe de superposición de conjuntos de datos.

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
| `data` | El `data` contiene listas de conjuntos de datos separados por comas y sus respectivos recuentos de perfiles. |
| `reportTimestamp` | La marca de tiempo del informe. Si un `date` se ha proporcionado durante la solicitud, el informe devuelto es para la fecha proporcionada. Si no `date` Si se proporciona el parámetro, se devuelve el informe más reciente. |

### Interpretación del informe de superposición de conjuntos de datos

Los resultados del informe se pueden interpretar a partir de los conjuntos de datos y los recuentos de perfiles de la respuesta. Consideremos el siguiente informe de ejemplo `data` objeto:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Este informe proporciona la siguiente información:

* Hay 123 perfiles compuestos de datos procedentes de los siguientes conjuntos de datos: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Hay 454 412 perfiles compuestos de datos procedentes de estos dos conjuntos de datos: `5d92921872831c163452edc8` y `5eb2cdc6fa3f9a18a7592a98`.
* Hay 107 perfiles que solo están compuestos por datos de conjuntos de datos `5eeda0032af7bb19162172a7`.
* Hay un total de 454.642 perfiles en la organización.

## Generar el informe de superposición del área de nombres de identidad {#identity-overlap-report}

El informe de superposición de áreas de nombres de identidad proporciona visibilidad sobre la composición del Almacenamiento de perfiles de su organización al exponer las áreas de nombres de identidad que más contribuyen a su audiencia a la que se puede dirigir (perfiles combinados). Esto incluye tanto las áreas de nombres de identidad estándar proporcionadas por Adobe, como las áreas de nombres de identidad personalizadas definidas por su organización.

GET Puede generar el informe de superposición de área de nombres de identidad realizando una solicitud a la variable `/previewsamplestatus/report/namespace/overlap` punto final.

**Formato de API**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la misma fecha, se devuelve el informe más reciente de esa fecha. Si no existe ningún informe para la fecha especificada, se devuelve el error 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud utiliza el `date` para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una solicitud correcta devuelve el estado HTTP 200 (OK) y el informe de superposición de área de nombres de identidad.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Propiedad | Descripción |
|---|---|
| `data` | El `data` contiene listas separadas por comas con combinaciones únicas de códigos de área de nombres de identidad y sus respectivos recuentos de perfiles. |
| Códigos de área de nombres | El `code` es una forma abreviada para cada nombre de área de nombres de identidad. Una asignación de cada `code` a su `name` se puede encontrar utilizando la variable [API del servicio de identidad de Adobe Experience Platform](../../identity-service/api/list-namespaces.md). El `code` también se denomina la variable [!UICONTROL Símbolo de identidad] en la interfaz de usuario de Experience Platform. Para obtener más información, visite la [información general del área de nombres de identidad](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | La marca de tiempo del informe. Si un `date` se ha proporcionado durante la solicitud, el informe devuelto es para la fecha proporcionada. Si no `date` Si se proporciona el parámetro, se devuelve el informe más reciente. |

### Interpretación del informe de superposición de área de nombres de identidad

Los resultados del informe se pueden interpretar a partir de las identidades y los recuentos de perfiles de la respuesta. El valor numérico de cada fila indica cuántos perfiles están compuestos de esa combinación exacta de áreas de nombres de identidad estándar y personalizadas.

Consideremos el siguiente extracto de la `data` objeto:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Este informe proporciona la siguiente información:

* Hay 142 perfiles compuestos por `AAID`, `ECID`, y `Email` identidades estándar, así como de una lista personalizada `crmid` área de nombres de identidad.
* Hay 24 perfiles compuestos por `AAID` y `ECID` áreas de nombres de identidad.
* Hay 6565 perfiles que solo incluyen un `ECID` identidad.

## Generación del informe de perfiles no enlazados

Puede obtener más visibilidad sobre la composición del Almacenamiento de perfiles de su organización a través del informe de perfiles no enlazados. Un perfil &quot;no identificado&quot; es un perfil que contiene solo un fragmento de perfil. Un perfil &quot;desconocido&quot; es un perfil asociado a áreas de nombres de identidad seudónimas como `ECID` y `AAID`. Los perfiles desconocidos están inactivos, lo que significa que no han agregado nuevos eventos para el período de tiempo especificado. El informe de perfiles no enlazados proporciona un desglose de perfiles para un periodo de 7, 30, 60, 90 y 120 días.

GET Puede generar el informe de perfiles no enlazados realizando una solicitud a la variable `/previewsamplestatus/report/unstitchedProfiles` punto final.

**Formato de API**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Solicitud**

La siguiente solicitud devuelve el informe de perfiles no enlazados.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una solicitud correcta devuelve el estado HTTP 200 (OK) y el informe de perfiles no enlazados.

>[!NOTE]
>
>A los efectos de esta guía, el informe se ha truncado para incluir solo `"120days"` y &quot;`7days`&quot; periodos de tiempo. El informe completo de perfiles no enlazados proporciona un desglose de perfiles para un periodo de 7, 30, 60, 90 y 120 días.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Propiedad | Descripción |
|---|---|
| `data` | El `data` contiene la información devuelta para el informe de perfiles no enlazados. |
| `totalNumberOfProfiles` | Recuento total de perfiles únicos en el almacén de perfiles. Es equivalente al recuento de audiencias a las que se puede dirigir. Incluye perfiles conocidos y no enlazados. |
| `totalNumberOfEvents` | Número total de ExperienceEvents en el almacén de perfiles. |
| `unstitchedProfiles` | Un objeto que contiene un desglose de perfiles no enlazados por periodo de tiempo. El informe de perfiles no enlazados proporciona un desglose de perfiles para los períodos de tiempo de 7, 30, 60, 90 y 120 días. |
| `countOfProfiles` | El recuento de perfiles no enlazados para el periodo de tiempo o el recuento de perfiles no enlazados para el área de nombres. |
| `eventsAssociated` | El número de ExperienceEvents para el intervalo de tiempo o el número de eventos para el área de nombres. |
| `nsDistribution` | Un objeto que contiene áreas de nombres de identidad individuales con la distribución de perfiles y eventos no enlazados para cada área de nombres. Nota: Sumando el total `countOfProfiles` para cada área de nombres de identidad en `nsDistribution` objeto es igual a `countOfProfiles` para el periodo de tiempo. Lo mismo se aplica a `eventsAssociated` por área de nombres y el total `eventsAssociated` por período de tiempo. |
| `reportTimestamp` | La marca de tiempo del informe. |

### Interpretación del informe de perfiles no enlazados

Los resultados del informe pueden proporcionar una perspectiva de cuántos perfiles no enlazados e inactivos tiene su organización dentro de su almacén de perfiles.

Consideremos el siguiente extracto de la `data` objeto:

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Este informe proporciona la siguiente información:

* Hay 1782 perfiles que contienen solo un fragmento de perfil y no tienen eventos nuevos en los últimos siete días.
* Existen 29 151 ExperienceEvents asociados a los 1782 perfiles no enlazados.
* Hay 1734 perfiles no enlazados que contienen un solo fragmento de perfil del área de nombres de identidad de ECID.
* Hay 28 591 eventos asociados con los 1734 perfiles no enlazados que contienen un solo fragmento de perfil del área de nombres de identidad de ECID.

## Pasos siguientes

Ahora que sabe cómo obtener una vista previa de los datos de ejemplo en el almacén de perfiles y ejecutar varios informes sobre los datos, también puede utilizar los extremos de estimación y vista previa de la API del servicio de segmentación para ver información de resumen sobre sus definiciones de segmento. Esta información le ayuda a aislar la audiencia esperada. Para obtener más información sobre cómo trabajar con vistas previas y estimaciones mediante la API de segmentación, visite la [guía de vista previa y estimación de extremos](../../segmentation/api/previews-and-estimates.md).

