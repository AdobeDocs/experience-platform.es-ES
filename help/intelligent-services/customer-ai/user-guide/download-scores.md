---
keywords: Experience Platform;puntuaciones de descarga;inteligencia artificial aplicada al cliente;temas populares;Exportar;exportar;descarga de inteligencia artificial aplicada al cliente;puntuaciones de inteligencia artificial aplicada al cliente
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Descargar puntuaciones en Customer AI
description: La inteligencia artificial aplicada al cliente le permite descargar puntuaciones en el formato de archivo Parquet.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 3%

---

# Puntuaciones de descarga en Customer AI

Este documento sirve como guía para descargar puntuaciones para la inteligencia artificial aplicada al cliente.

## Introducción

La inteligencia artificial aplicada al cliente le permite descargar puntuaciones en el formato de archivo Parquet. Este tutorial requiere que haya leído y terminado la sección de descarga de puntuaciones de inteligencia artificial aplicada al cliente en la guía de [introducción](../getting-started.md).

Además, para acceder a las puntuaciones de inteligencia artificial aplicada al cliente, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visita [Configuración de una instancia de inteligencia artificial aplicada al cliente](./configure.md). Si ha creado recientemente una instancia de servicio que aún se está entrenando y puntuando, espere 24 horas para que finalice la ejecución.

Actualmente, hay dos formas de descargar las puntuaciones de inteligencia artificial aplicada al cliente:

1. Si desea descargar las puntuaciones en el nivel individual o no tiene habilitado el perfil del cliente en tiempo real, comience por [encontrar su ID del conjunto de datos](#dataset-id).
2. Si tiene el perfil habilitado y desea descargar segmentos que haya configurado con la inteligencia artificial aplicada al cliente, vaya a [descargar un segmento configurado con la inteligencia artificial aplicada al cliente](#segment).

## Búsqueda del ID del conjunto de datos {#dataset-id}

En la instancia de servicio para la información de inteligencia artificial aplicada al cliente, haga clic en el menú desplegable *Más acciones* en la barra de navegación superior derecha y, a continuación, seleccione **[!UICONTROL Puntuaciones de acceso]**.

![más acciones](../images/insights/more-actions.png)

Aparece un nuevo cuadro de diálogo que contiene un vínculo a la documentación de descarga de puntuaciones y el ID del conjunto de datos de la instancia actual. Copie el ID del conjunto de datos en el portapapeles y continúe con el siguiente paso.

![ID de conjunto de datos](../images/download-scores/access-scores.png)

## Recupere su ID de lote {#retrieve-your-batch-id}

Con el ID del conjunto de datos del paso anterior, debe realizar una llamada a la API de catálogo para recuperar un ID de lote. Se utilizan parámetros de consulta adicionales para esta llamada de API a fin de devolver el último lote correcto en lugar de una lista de lotes pertenecientes a su organización. Para devolver lotes adicionales, aumente el número del parámetro de consulta limit a la cantidad deseada que desee que se devuelva. Para obtener más información sobre los tipos de parámetros de consulta disponibles, visite la guía sobre [filtrado de datos de catálogo mediante parámetros de consulta](../../../catalog/api/filter-data.md).

**Formato de API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos disponible en el cuadro de diálogo &quot;Puntuaciones de acceso&quot;. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto de ID de lote. En este ejemplo, el valor clave del objeto devuelto es el identificador de lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie su ID de lote para utilizarlo en la siguiente llamada de API.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## Recupere la siguiente llamada de API con su ID de lote {#retrieve-the-next-api-call-with-your-batch-id}

Una vez que tenga su ID de lote, podrá realizar una nueva solicitud de GET a `/batches`. La solicitud devuelve un vínculo que se utiliza como siguiente solicitud de API.

**Formato de API**

```http
GET batches/{BATCH_ID}/files
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El identificador de lote que se recuperó en el paso anterior [recuperó su identificador de lote](#retrieve-your-batch-id). |

**Solicitud**

Con su propio ID de lote, realice la siguiente solicitud.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto `_links`. Dentro del objeto `_links` hay un `href` con una nueva llamada API como valor. Copie este valor para continuar con el paso siguiente.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## Recuperación de archivos {#retrieving-your-files}

Utilizando el valor `href` que obtuvo en el paso anterior como una llamada de API, realice una nueva solicitud de GET para recuperar el directorio de archivos.

**Formato de API**

```http
GET files/{DATASETFILE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | Se devuelve el identificador dataSetFile en el valor `href` del [paso anterior](#retrieve-the-next-api-call-with-your-batch-id). También es accesible en la matriz `data` bajo el tipo de objeto `dataSetFileId`. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta contiene una matriz de datos que puede tener una sola entrada o una lista de archivos que pertenecen a ese directorio. El ejemplo siguiente contiene una lista de archivos y se ha condensado para facilitar la lectura. En este caso, debe seguir la dirección URL de cada archivo para acceder al archivo.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `_links.self.href` | La URL de solicitud de GET utilizada para descargar un archivo en su directorio. |


Copie el valor `href` de cualquier objeto de archivo de la matriz `data` y, a continuación, continúe con el paso siguiente.

## Descargar los datos del archivo

Para descargar los datos del archivo, realice una solicitud de GET al valor `"href"` que copió en el paso anterior [recuperar los archivos](#retrieving-your-files).

>[!NOTE]
>
>Si realiza esta solicitud directamente en la línea de comandos, es posible que se le pida que agregue un resultado después de los encabezados de solicitud. El siguiente ejemplo de solicitud utiliza `--output {FILENAME.FILETYPE}`.

**Formato de API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | Se devolvió el id. dataSetFile en el valor `href` de un [paso anterior](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Nombre del archivo. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Asegúrese de que está en el directorio o carpeta correctos en los que desea guardar el archivo antes de realizar la solicitud de GET.

**Respuesta**

La respuesta descarga el archivo solicitado en en el directorio actual. En este ejemplo, el nombre de archivo es &quot;filename.parquet&quot;.

![Terminal](../images/download-scores/response.png)

## Descargar un segmento configurado con Customer AI {#segment}

Una forma alternativa de descargar los datos de puntuación es exportar la audiencia a un conjunto de datos. Una vez que un trabajo de segmentación se haya completado correctamente (el valor del atributo `status` es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos al que se pueda acceder y sobre el que se pueda actuar. Para obtener más información acerca de la segmentación, visita la [descripción general de la segmentación](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Para utilizar este método de exportación, el perfil del cliente en tiempo real debe estar habilitado para el conjunto de datos.

La sección [exportar un segmento](../../../segmentation/tutorials/evaluate-a-segment.md) de la guía de evaluación de segmentos cubre los pasos necesarios para exportar un conjunto de datos de audiencia. La guía describe y proporciona ejemplos de lo siguiente:

- **Crear un conjunto de datos de destinatario:** Cree el conjunto de datos para albergar miembros de audiencia.
- **Generar perfiles de audiencia en el conjunto de datos:** Rellene el conjunto de datos con perfiles individuales XDM en función de los resultados de un trabajo de segmentación.
- **Supervisar progreso de exportación:** Compruebe el progreso actual del proceso de exportación.
- **Leer datos de audiencia:** Recupere los perfiles individuales XDM resultantes que representan a los miembros de su audiencia.

## Pasos siguientes

En este documento se describen los pasos necesarios para descargar las puntuaciones de inteligencia artificial aplicada al cliente. Ahora puede continuar explorando los otros [servicios inteligentes](../../home.md) y las guías que se ofrecen.
