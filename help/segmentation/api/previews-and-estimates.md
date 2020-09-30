---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;previews;estimates;previews and estimates;estimates and previews;api;API;
solution: Experience Platform
title: Definiciones de previsualizaciones y estimaciones
topic: developer guide
description: A medida que desarrolla la definición del segmento, puede utilizar las herramientas de previsualización y estimación de Adobe Experience Platform para obtener información de nivel de resumen de vista y así asegurarse de aislar la audiencia esperada.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 2%

---


# Definiciones de previsualizaciones y estimaciones

A medida que desarrolla la definición del segmento, puede utilizar las herramientas de previsualización y estimación dentro de [!DNL Adobe Experience Platform] la información de nivel de resumen de vista para asegurarse de aislar la audiencia esperada. **Las previsualizaciones** proporcionan listas paginadas de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera. **Las estimaciones** proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte la guía [de](./getting-started.md) introducción para obtener información importante que debe conocer a fin de realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Cómo se generan las estimaciones

La manera en que se activa el muestreo de datos depende del método de ingestión.

Para la ingestión por lotes, el almacén de perfiles se escanea automáticamente cada quince minutos para ver si un nuevo lote se ha ingerido correctamente desde la ejecución del último trabajo de muestra. Si ese es el caso, el almacén de perfiles se escanea posteriormente para ver si ha habido al menos un cambio del 5% en el número de registros. Si se cumplen estas condiciones, se activa un nuevo trabajo de muestra.

Para la transmisión de transmisiones, el almacén de perfiles se escanea automáticamente cada hora para ver si ha habido al menos un cambio del 5 % en el número de registros. Si se cumple esta condición, se activa un nuevo trabajo de muestra.

El tamaño de muestra del análisis depende del número total de entidades del almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades de la tienda de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

>[!NOTE]
>
>Las estimaciones generalmente tardan entre 10 y 15 segundos en ejecutarse, comenzando con una estimación aproximada y refinándose a medida que se leen más registros.

## Create a new preview {#create-preview}

Puede crear una nueva previsualización haciendo una solicitud de POST al `/preview` extremo.

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
| `predicateType` | Tipo de predicado de la expresión de consulta en `predicateExpression`. Actualmente, el único valor aceptado para esta propiedad es `pql/text`. |
| `predicateModel` | Nombre del esquema [!DNL Experience Data Model] (XDM) en el que se basan los datos de perfil. |

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

Puede recuperar información detallada sobre una previsualización específica realizando una solicitud de GET al extremo y proporcionando el ID de previsualización en la ruta de la solicitud. `/preview`

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{PREVIEW_ID}` | El `previewId` valor de la previsualización que desea recuperar. |

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
| `results` | Una lista de los ID de entidad, junto con sus identidades relacionadas. Los vínculos proporcionados se pueden utilizar para buscar las entidades especificadas mediante la [[!DNL API de acceso a Perfil]](../../profile/api/entities.md). |

## Recuperar los resultados de un trabajo de estimación específico {#get-estimate}

Una vez creado un trabajo de previsualización, puede utilizarlo `previewId` en la ruta de una solicitud de GET al `/estimate` extremo para vista de información estadística sobre la definición del segmento, incluido el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un trabajo de estimación solo se activa cuando se crea un trabajo de previsualización y los dos trabajos comparten el mismo valor de ID para fines de búsqueda. Concretamente, este es el `previewId` valor devuelto cuando se creó el trabajo de previsualización. |

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
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `state` | Estado actual del trabajo de previsualización. Se &quot;EJECUTARÁ&quot; hasta que se complete el procesamiento, momento en el que se convierte en &quot;RESULT_READY&quot; o &quot;FALLADO&quot;. |
| `_links.preview` | Cuando el estado actual del trabajo de previsualización es &quot;RESULT_READY&quot;, este atributo proporciona una URL para la vista de la estimación. |

## Pasos siguientes

Después de leer esta guía ahora tiene una mejor comprensión de cómo trabajar con previsualizaciones y estimaciones. Para obtener más información sobre los otros extremos de la [!DNL Segmentation Service] API, lea la guía para desarrolladores del servicio de [segmentación](./overview.md).