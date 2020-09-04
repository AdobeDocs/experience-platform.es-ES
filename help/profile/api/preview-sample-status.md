---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
solution: Adobe Experience Platform
title: 'Previsualización de perfiles: API de Perfil de clientes en tiempo real'
description: Adobe Experience Platform le permite ingestar datos de clientes desde múltiples fuentes para crear perfiles unificados sólidos para clientes individuales. Como los datos habilitados para el Perfil del cliente en tiempo real se ingieren en la plataforma, se almacenan en el almacén de datos de Perfil. A medida que aumenta o disminuye el número de registros en el almacén de Perfiles, se ejecuta un trabajo de muestra que incluye información sobre cuántos fragmentos de perfil y perfiles combinados hay en el almacén de datos. Mediante la API de Perfil puede realizar previsualizaciones de la muestra más reciente de éxito, así como de la distribución de perfiles de lista por conjunto de datos y por Área de nombres de identidad.
topic: guide
translation-type: tm+mt
source-git-commit: 2edba7cba4892f5c8dd41b15219bf45597bd5219
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---


# Extremo de estado de muestra de previsualización (previsualización de Perfil)

Adobe Experience Platform le permite ingestar datos de clientes desde múltiples fuentes para crear perfiles unificados sólidos para clientes individuales. Como los datos habilitados para el Perfil del cliente en tiempo real se ingieren en [!DNL Platform], se almacenan en el almacén de datos de Perfil.

Cuando la ingestión de registros en el almacén de Perfiles aumenta o disminuye el recuento total de perfiles en más de un 5 %, se activa un trabajo para actualizar el recuento. Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación por hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento. Para la ingestión por lotes, dentro de los 15 minutos siguientes a la correcta ingestión de un lote en el almacén de Perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento. Mediante la API de Perfil puede realizar la previsualización del último trabajo de muestra exitoso, así como la distribución de perfiles de lista por conjunto de datos y por Área de nombres de identidad.

Estas métricas también están disponibles en la sección de [!UICONTROL Perfiles] de la interfaz de usuario del Experience Platform. Para obtener información sobre cómo acceder a los datos de Perfil mediante la interfaz de usuario, visite la guía del [[!DNL Profile] usuario](../ui/user-guide.md).

## Primeros pasos

El punto final de API utilizado en esta guía forma parte de la [[!DNL Real-time Customer Profile] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Estado de la última muestra de vista {#view-last-sample-status}

Puede realizar una solicitud de GET al extremo para realizar una vista de los detalles del último trabajo de muestra exitoso que se ejecutó para su organización de IMS. `/previewsamplestatus` Esto incluye el número total de perfiles en el ejemplo, así como la métrica de recuento de perfiles o el número total de perfiles que su organización tiene dentro del Experience Platform. El recuento de perfiles se genera después de combinar fragmentos de perfil para formar un único perfil para cada cliente individual. En otras palabras, su organización puede tener varios fragmentos de perfil relacionados con un único cliente que interactúa con su marca en diferentes canales, pero estos fragmentos se combinarán (según la política de combinación predeterminada) y devolverá un recuento de perfiles &quot;1&quot; porque todos están relacionados con el mismo individuo.

El recuento de perfiles también incluye tanto perfiles con atributos (datos de registros) como perfiles que contienen únicamente datos de series temporales (eventos), como perfiles Adobe Analytics. El trabajo de muestra se actualiza regularmente a medida que se ingieren datos de Perfil para proporcionar un número total actualizado de perfiles dentro de la plataforma.

**Formato API**

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

La respuesta incluye los detalles del último trabajo de muestra exitoso que se ejecutó para la organización de IMS.

>[!NOTE]
>
>En esta respuesta de ejemplo `numRowsToRead` , y son iguales `totalRows` entre sí. Según el número de perfiles que su organización tenga en Experience Platform, este puede ser el caso. Sin embargo, por lo general estos dos números son diferentes, siendo `numRowsToRead` el número más pequeño porque representa la muestra como un subconjunto del número total de perfiles (`totalRows`).

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
| `sampleJobRunning` | Valor booleano que se devuelve `true` cuando un trabajo de muestra está en curso. Proporciona transparencia en la latencia que se produce cuando se carga un archivo por lotes cuando se agrega al almacén de Perfiles. |
| `cosmosDocCount` | Recuento total de documentos en Cosmos. |
| `totalFragmentCount` | Número total de fragmentos de perfil en el almacén de Perfiles. |
| `lastSuccessfulBatchTimestamp` | Última marca de tiempo de ingestión por lotes correcta. |
| `streamingDriven` | *Este campo ha quedado obsoleto y no tiene relevancia para la respuesta.* |
| `totalRows` | Número total de perfiles combinados en la plataforma de Experience, también conocida como &#39;recuento de perfiles&#39;. |
| `lastBatchId` | Id. de la última ingesta por lotes. |
| `status` | Estado de la última muestra. |
| `samplingRatio` | Proporción de perfiles fusionados muestreados (`numRowsToRead`) con respecto al total de perfiles fusionados (`totalRows`), expresada como porcentaje en formato decimal. |
| `mergeStrategy` | Estrategia de combinación utilizada en el ejemplo. |
| `lastSampledTimestamp` | Última marca de tiempo de muestra correcta. |

## Distribución del perfil de lista por conjunto de datos

Para ver la distribución de perfiles por conjunto de datos, puede realizar una solicitud de GET al `/previewsamplestatus/report/dataset` extremo.

**Formato API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que se va a devolver. Si se ejecutaron varios informes en la fecha, se devolverá el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se mostrará un error 404. Si no se especifica ninguna fecha, se devolverá el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud utiliza el `date` parámetro para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una `data` matriz que contiene una lista de objetos de conjunto de datos. La respuesta mostrada se ha truncado para mostrar tres conjuntos de datos.

>[!NOTE]
>
>Si existieran varios informes para la fecha, solo se devolverá el último. Si no existe un informe de conjunto de datos para la fecha proporcionada, se devolverá el estado HTTP 404 (no encontrado).

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
| `sampleCount` | El número total de perfiles combinados muestreados con este ID de conjunto de datos. |
| `samplePercentage` | El `sampleCount` porcentaje del número total de perfiles combinados incluidos en la muestra (el `numRowsToRead` valor devuelto en el estado [de la](#view-last-sample-status)última muestra), expresado en formato decimal. |
| `fullIDsCount` | Número total de perfiles combinados con este ID de conjunto de datos. |
| `fullIDsPercentage` | El `fullIDsCount` como porcentaje del número total de perfiles combinados (el `totalRows` valor devuelto en el estado [de la](#view-last-sample-status)última muestra), expresado en formato decimal. |
| `name` | Nombre del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `description` | Descripción del conjunto de datos, tal como se proporciona durante la creación del conjunto de datos. |
| `value` | ID del conjunto de datos. |
| `streamingIngestionEnabled` | Indica si el conjunto de datos está habilitado para la transmisión por flujo continuo de ingesta. |
| `createdUser` | ID de usuario del usuario que creó el conjunto de datos. |
| `reportTimestamp` | Marca de hora del informe. Si se proporcionó un `date` parámetro durante la solicitud, el informe devuelto corresponde a la fecha proporcionada. Si no se proporciona ningún `date` parámetro, se devuelve el informe más reciente. |



## Distribución de perfiles de lista por Área de nombres

Puede realizar una solicitud de GET al extremo para realizar una vista del desglose por Área de nombres de identidad en todos los perfiles combinados del almacén de Perfiles. `/previewsamplestatus/report/namespace` Las Áreas de nombres de identidad son un componente importante de Adobe Experience Platform Identity Service que sirve como indicadores del contexto con el que se relacionan los datos del cliente. Para obtener más información, visite la descripción general [de la Área de nombres de](../../identity-service/namespaces.md)identidad.

>[!NOTE]
>
>El número total de perfiles por Área de nombres (sumando los valores mostrados para cada Área de nombres) siempre será mayor que la métrica de recuento de perfiles porque un perfil podría estar asociado con varias Áreas de nombres. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias Áreas de nombres con ese cliente individual.

**Formato API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que se va a devolver. Si se ejecutaron varios informes en la fecha, se devolverá el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se mostrará un error 404. Si no se especifica ninguna fecha, se devolverá el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Solicitud**

La siguiente solicitud no especifica ningún `date` parámetro y, por lo tanto, devuelve el informe más reciente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una `data` matriz, con objetos individuales que contienen los detalles de cada Área de nombres. La respuesta mostrada se ha truncado para mostrar cuatro Áreas de nombres.

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
| `sampleCount` | El número total de perfiles combinados de muestra en la Área de nombres. |
| `samplePercentage` | El `sampleCount` porcentaje de perfiles combinados muestreados (el `numRowsToRead` valor devuelto en el estado [de la](#view-last-sample-status)última muestra), expresado en formato decimal. |
| `reportTimestamp` | Marca de hora del informe. Si se proporcionó un `date` parámetro durante la solicitud, el informe devuelto corresponde a la fecha proporcionada. Si no se proporciona ningún `date` parámetro, se devuelve el informe más reciente. |
| `fullIDsFragmentCount` | Número total de fragmentos de perfil en la Área de nombres. |
| `fullIDsCount` | Número total de perfiles combinados en la Área de nombres. |
| `fullIDsPercentage` | El `fullIDsCount` porcentaje del total de perfiles combinados (el `totalRows` valor devuelto en el estado [de la](#view-last-sample-status)última muestra), expresado en formato decimal. |
| `code` | El `code` de la Área de nombres. Esto se puede encontrar al trabajar con Áreas de nombres mediante la API [de](../../identity-service/api/list-namespaces.md) Adobe Experience Platform Identity Service y también se denomina símbolo [!UICONTROL de] identidad en la interfaz de usuario de Experience Platform. Para obtener más información, visite la descripción general [de la Área de nombres de](../../identity-service/namespaces.md)identidad. |
| `value` | El `id` valor de la Área de nombres. Esto se puede encontrar al trabajar con Áreas de nombres mediante la API [de servicio de](../../identity-service/api/list-namespaces.md)identidad. |

## Pasos siguientes

También puede utilizar estimaciones y previsualizaciones similares para la información de nivel de resumen de la vista con respecto a las definiciones de los segmentos a fin de asegurarse de aislar la audiencia esperada. Para encontrar pasos detallados para trabajar con previsualizaciones de segmentos y estimaciones usando la [!DNL Adobe Experience Platform Segmentation Service] API, visite la guía [de puntos finales de](../../segmentation/api/previews-and-estimates.md)previsualizaciones y estimaciones, que forma parte de la guía para desarrolladores de la [!DNL Segmentation] API.

