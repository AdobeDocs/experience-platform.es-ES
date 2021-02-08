---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;previsualizaciones;estimaciones;previsualizaciones y estimaciones;estimaciones y previsualizaciones;api;API;
solution: Experience Platform
title: Previsualizaciones y estimaciones de extremos de API
topic: developer guide
description: A medida que se desarrollan las definiciones de segmentos, puede utilizar las herramientas de estimación y previsualización de Adobe Experience Platform para obtener información de nivel de resumen de vista y así asegurarse de aislar la audiencia esperada.
translation-type: tm+mt
source-git-commit: eba6de210dcbc12b829b09ba6e7083d342517ba2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Definiciones de previsualizaciones y estimaciones

A medida que desarrolla una definición de segmento, puede utilizar las herramientas de estimación y previsualización de Adobe Experience Platform para obtener información de nivel de resumen de vista y así asegurarse de aislar la audiencia que espera.

* **Las** vistas previas proporcionan listas paginadas de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

* **Las** estimaciones proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error.

>[!NOTE]
>
>Para acceder a métricas similares relacionadas con los datos de Perfil del cliente en tiempo real, como el número total de fragmentos de perfil y perfiles combinados dentro de Áreas de nombres específicas o el almacén de datos de Perfil en su conjunto, consulte la [guía de extremo de previsualización de perfil (estado de muestra de previsualización)](../../profile/api/preview-sample-status.md), parte de la guía para desarrolladores de la API de Perfil.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer a fin de realizar llamadas exitosas a la API, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Cómo se generan las estimaciones

Cuando la ingestión de registros en el almacén de Perfiles aumenta o disminuye el recuento total de perfiles en más de un 5 %, se activa un trabajo de muestra para actualizar el recuento. La manera en que se activa el muestreo de datos depende del método de ingestión:

* **Ingesta por lotes:** para la ingestión por lotes, en un plazo de 15 minutos a partir de la correcta ingestión de un lote en el almacén de Perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento.
* **Transmisión de flujo continuo:** para flujos de trabajo de datos de flujo continuo, se realiza una comprobación por hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento.

El tamaño de muestra del análisis depende del número total de entidades del almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades de la tienda de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

>[!NOTE]
>
>Las estimaciones generalmente tardan entre 10 y 15 segundos en ejecutarse, comenzando con una estimación aproximada y refinándose a medida que se leen más registros.

## Crear una nueva previsualización {#create-preview}

Puede crear una nueva previsualización haciendo una solicitud de POST al extremo `/preview`.

>[!NOTE]
>
>Cuando se crea un trabajo de previsualización, se crea automáticamente un trabajo de estimación. Estos dos trabajos compartirán el mismo ID.

**Formato API**

```http
POST /preview
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `predicateExpression` | Expresión de PQL para la consulta de los datos. |
| `predicateType` | El tipo de predicado para la expresión de consulta en `predicateExpression`. Actualmente, el único valor aceptado para esta propiedad es `pql/text`. |
| `predicateModel` | Nombre de la clase de esquema [!DNL Experience Data Model] (XDM) en la que se basan los datos de perfil. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) con detalles de la previsualización recién creada.

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
| `state` | Estado actual del trabajo de previsualización. Cuando se cree inicialmente, estará en el estado &quot;NUEVO&quot;. Posteriormente, estará en el estado &quot;EN EJECUCIÓN&quot; hasta que se complete el procesamiento, en cuyo momento se convertirá en &quot;RESULT_READY&quot; o &quot;FALLADO&quot;. |
| `previewId` | ID del trabajo de previsualización, que se utilizará con fines de búsqueda al ver una estimación o previsualización, como se describe en la siguiente sección. |

## Recuperar los resultados de una previsualización específica {#get-preview}

Puede recuperar información detallada sobre una previsualización específica haciendo una solicitud de GET al extremo `/preview` y proporcionando el ID de previsualización en la ruta de la solicitud.

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{PREVIEW_ID}` | El valor `previewId` de la previsualización que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la previsualización especificada.

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
| `results` | Una lista de los ID de entidad, junto con sus identidades relacionadas. Los vínculos proporcionados se pueden utilizar para buscar las entidades especificadas, utilizando el extremo [API de acceso a perfil](../../profile/api/entities.md). |

## Recuperar los resultados de un trabajo de estimación específico {#get-estimate}

Una vez creado un trabajo de previsualización, puede utilizar su `previewId` en la ruta de una solicitud de GET al extremo `/estimate` para obtener información estadística de vista sobre la definición del segmento, incluido el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un trabajo de estimación solo se activa cuando se crea un trabajo de previsualización y los dos trabajos comparten el mismo valor de ID para fines de búsqueda. Específicamente, este es el valor `previewId` devuelto cuando se creó el trabajo de previsualización. |

**Solicitud**

La siguiente solicitud recupera los resultados de un trabajo de estimación específico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `estimatedNamespaceDistribution` | Matriz de objetos que muestra el número de perfiles dentro del segmento desglosado por Área de nombres de identidad. El número total de perfiles por Área de nombres (sumando los valores mostrados para cada Área de nombres) puede ser mayor que la métrica de recuento de perfiles porque un perfil podría estar asociado con varias Áreas de nombres. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias Áreas de nombres con ese cliente individual. |
| `state` | Estado actual del trabajo de previsualización. El estado será &quot;EJECUTANDO&quot; hasta que se complete el procesamiento, momento en el cual se convierte en &quot;RESULT_READY&quot; o &quot;FALLADO&quot;. |
| `_links.preview` | Cuando `state` es &quot;RESULT_READY&quot;, este campo proporciona una dirección URL para la vista de la estimación. |

## Pasos siguientes

Después de leer esta guía, debe comprender mejor cómo trabajar con previsualizaciones y estimaciones mediante la API de segmentación. Para obtener información sobre cómo acceder a las métricas relacionadas con los datos de Perfil del cliente en tiempo real, como el número total de fragmentos de perfil y perfiles combinados dentro de Áreas de nombres específicas o el almacén de datos de Perfil en su conjunto, visite la [guía de extremo de previsualización de perfil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).