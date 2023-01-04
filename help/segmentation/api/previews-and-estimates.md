---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;previsualizaciones;estimaciones;previsualizaciones y estimaciones;estimaciones y previsualizaciones;api;API;
solution: Experience Platform
title: Vistas previas y estimaciones de puntos de conexión de API
topic-legacy: developer guide
description: A medida que se desarrolla la definición del segmento, puede utilizar las herramientas de estimación y vista previa de Adobe Experience Platform para ver la información de resumen y garantizar que está aislando la audiencia esperada.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# Puntos finales de vista previa y estimación

A medida que desarrolla una definición de segmento, puede utilizar las herramientas de estimación y vista previa de Adobe Experience Platform para ver información de resumen que le ayude a garantizar que está aislando la audiencia que espera.

* **Vistas previas** proporciona listas paginadas de perfiles aptos para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

* **Estimaciones** proporciona información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error.

>[!NOTE]
>
>Para acceder a métricas similares relacionadas con los datos del perfil del cliente en tiempo real, como el número total de fragmentos de perfil y perfiles combinados dentro de áreas de nombres específicas o el almacén de datos del perfil en su conjunto, consulte la [guía de extremo de vista previa de perfil (vista previa del estado de muestra)](../../profile/api/preview-sample-status.md), parte de la guía para desarrolladores de API de perfil.

## Primeros pasos

Los extremos utilizados en esta guía forman parte del [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Cómo se generan las estimaciones

Cuando la ingesta de registros en el almacén de perfiles aumenta o disminuye el recuento total de perfiles en más del 5 %, se activa un trabajo de muestreo para actualizar el recuento. La forma en que se activa el muestreo de datos depende del método de ingesta:

* **Ingesta por lotes:** Para la ingesta por lotes, en los 15 minutos siguientes a la ingesta correcta de un lote en el Almacenamiento de perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento.
* **Ingesta de flujo continuo:** Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento.

El tamaño de la muestra depende del número total de entidades en el almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades en el almacén de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| de 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

>[!NOTE]
>
>Las estimaciones generalmente tardan entre 10 y 15 segundos en ejecutarse, comenzando con una estimación aproximada y refinándose a medida que se leen más registros.

## Crear una vista previa nueva {#create-preview}

Puede crear una nueva vista previa realizando una solicitud de POST al `/preview` punto final.

>[!NOTE]
>
>Se crea automáticamente un trabajo de estimación cuando se crea un trabajo de vista previa. Estos dos trabajos compartirán el mismo ID.

**Formato de API**

```http
POST /preview
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `predicateExpression` | La expresión PQL por la que se consultan los datos. |
| `predicateType` | El tipo de predicado de la expresión de consulta en `predicateExpression`. Actualmente, el único valor aceptado para esta propiedad es `pql/text`. |
| `predicateModel` | El nombre del [!DNL Experience Data Model] (XDM) clase de esquema en la que se basan los datos de perfil. |
| `graphType` | El tipo de gráfico desde el que desea obtener el clúster. Los valores admitidos son `none` (no realiza vinculación de identidad) y `pdg` (realiza la vinculación de identidad en función del gráfico de identidad privada). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) con detalles de la vista previa recién creada.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `state` | Estado actual del trabajo de vista previa. Cuando se crea por primera vez, aparece en el estado &quot;NUEVO&quot;. Posteriormente, estará en el estado &quot;EJECUTANDO&quot; hasta que se complete el procesamiento, momento en el que se convierte en &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `previewId` | El ID del trabajo de vista previa, que se utilizará con fines de búsqueda al ver una estimación o vista previa, tal como se describe en la siguiente sección. |

## Recuperar los resultados de una vista previa específica {#get-preview}

Puede recuperar información detallada sobre una vista previa específica realizando una solicitud de GET al `/preview` y proporcionando el ID de vista previa en la ruta de solicitud.

**Formato de API**

```http
GET /preview/{PREVIEW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{PREVIEW_ID}` | La variable `previewId` de la vista previa que desee recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la vista previa especificada.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `results` | Una lista de ID de entidad, junto con sus identidades relacionadas. Los vínculos proporcionados se pueden utilizar para buscar las entidades especificadas, utilizando la variable [extremo de API de acceso a perfiles](../../profile/api/entities.md). |

## Recuperar los resultados de un trabajo de estimación específico {#get-estimate}

Una vez que haya creado un trabajo de vista previa, puede utilizar su `previewId` en la ruta de una solicitud de GET al `/estimate` para ver información estadística sobre la definición del segmento, incluido el tamaño de audiencia previsto, el intervalo de confianza y la desviación estándar de errores.

**Formato de API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un trabajo de estimación solo se activa cuando se crea un trabajo de vista previa, y los dos trabajos comparten el mismo valor de ID con fines de búsqueda. Específicamente, esta es la variable `previewId` valor devuelto cuando se creó el trabajo de vista previa. |

**Solicitud**

La siguiente solicitud recupera los resultados de un trabajo de estimación específico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del trabajo de estimación.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Matriz de objetos que muestra el número de perfiles del segmento desglosado por área de nombres de identidad. El número total de perfiles por área de nombres (sumando los valores mostrados para cada área de nombres) puede ser mayor que la métrica de recuento de perfiles porque un perfil podría asociarse con varias áreas de nombres. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual. |
| `state` | Estado actual del trabajo de vista previa. El estado será &quot;EJECUTANDO&quot; hasta que se complete el procesamiento, momento en el que se convierte en &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `_links.preview` | Cuando la variable `state` es &quot;RESULT_READY&quot;, este campo proporciona una dirección URL para ver la estimación. |

## Pasos siguientes

Después de leer esta guía, debe comprender mejor cómo trabajar con vistas previas y estimaciones mediante la API de segmentación. Para obtener información sobre cómo acceder a las métricas relacionadas con los datos del perfil del cliente en tiempo real, como el número total de fragmentos de perfil y perfiles combinados dentro de áreas de nombres específicas o el almacén de datos de perfil en su conjunto, visite [vista previa de perfil (`/previewsamplestatus`) guía del extremo](../../profile/api/preview-sample-status.md).
