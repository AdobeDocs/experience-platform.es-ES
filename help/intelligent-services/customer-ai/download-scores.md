---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: Descarga de puntuaciones en la API del cliente
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 387cbdebccb9ae54a2907d1afe220e9711927ca6

---


# Descarga de puntuaciones en la API del cliente

Este documento sirve como guía para descargar puntuaciones para la API del cliente.

## Primeros pasos

La API del cliente le permite descargar puntuaciones en formato de archivo de parqué. Este tutorial requiere que haya leído y terminado la sección de descarga de puntuaciones de AI del cliente en la guía de [introducción](./getting-started.md) .

Además, para acceder a las puntuaciones de la API del cliente, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite la guía [de usuario de AI del](./user-guide.md)cliente. Si ha creado recientemente una instancia de servicio y aún está en formación y puntaje, espere 24 horas para que termine de ejecutarse.

Actualmente, existen dos formas de descargar puntuaciones de AI de cliente:

1. Si desea descargar las puntuaciones en el nivel individual y/o no tiene activado el Perfil del cliente en tiempo real, vaya a [buscar el ID](#dataset-id)del conjunto de datos para realizar el inicio.
2. Si tiene activado el Perfil y desea descargar segmentos que ha configurado mediante la API del cliente, navegue para [descargar un segmento configurado con la API](#segment)del cliente.

## Find your dataset ID {#dataset-id}

Dentro de la instancia de servicio para obtener información sobre la API del cliente, haga clic en el menú desplegable *Más acciones* en la navegación superior derecha y, a continuación, seleccione **Acceso a puntuaciones**.

![más acciones](./images/insights/more-actions.png)

Aparece un nuevo cuadro de diálogo que contiene un vínculo a la documentación de las puntuaciones de descarga y al ID del conjunto de datos de la instancia actual. Copie el ID del conjunto de datos en el portapapeles y continúe con el paso siguiente.

![Id. de conjunto de datos](./images/download-scores/access-scores.png)

## Recuperar el ID de lote {#retrieve-your-batch-id}

Con el ID del conjunto de datos del paso anterior, debe realizar una llamada a la API del catálogo para recuperar un ID de lote. Se utilizan parámetros de consulta adicionales para esta llamada de API con el fin de devolver un solo lote en lugar de una lista de lotes pertenecientes a su organización. Para obtener más información sobre los tipos de parámetros de consulta disponibles, visite la guía sobre el [filtrado de datos del catálogo mediante parámetros](../../catalog/api/filter-data.md)de consulta.

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&orderBy=desc:created&limit=1
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos disponible en el cuadro de diálogo &quot;Puntuaciones de acceso&quot;. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto de ID de lote de puntuación. In this example, the object is `5e602f67c2f39715a87f46b1`.

Dentro del objeto de ID de lote de puntuación hay una `relatedObjects` matriz. Esta matriz contiene dos objetos. El primer objeto tiene un `type` valor de &quot;lote&quot; y también contiene un ID. En la respuesta de ejemplo siguiente, el ID del lote es `035e2520-5e69-11ea-b624-51evfeba55d1`. Copie el ID de lote para utilizarlo en la siguiente llamada de API.

```json
{   
    "5e602f67c2f39715a87f46b1": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540e14cd3d0432",
                "type": "dataSet"
            },
            {
                "id": "035e2520-5e69-11ea-b624-51evfeba55d1",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsRead": 46721830,
            "recordsWritten": 46721830,
            "avgNumExecutorsPerTask": 33,
            "startTime": 1583362385336,
            "inputSizeInKb": 10242034,
            "endTime": 1583363197517
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    }
}
```

## Recupere la siguiente llamada de API con su ID de lote {#retrieve-the-next-api-call-with-your-batch-id}

Una vez que tenga su ID de lote, podrá realizar una nueva solicitud GET a `/batches`. La solicitud devuelve un vínculo que se utiliza como la siguiente solicitud de API.

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID de lote que se recuperó en el paso anterior [recupera el ID](#retrieve-your-batch-id)de lote. |

**Solicitud**

Con su propio ID de lote, realice la siguiente solicitud.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un `_links` objeto. Dentro del `_links` objeto hay un valor `href` con una nueva llamada de API. Copie este valor para continuar con el paso siguiente.

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

## Recuperar los archivos {#retrieving-your-files}

Utilizando el `href` valor obtenido en el paso anterior como una llamada de API, realice una nueva solicitud GET para recuperar el directorio de archivos.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | El ID de dataSetFile se devuelve en el `href` valor del paso [](#retrieve-the-next-api-call-with-your-batch-id)anterior. También se puede acceder a ella en la `data` matriz bajo el tipo de objeto `dataSetFileId`. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta contiene una matriz de datos que puede tener una sola entrada o una lista de archivos pertenecientes a ese directorio. El ejemplo siguiente contiene una lista de archivos y se ha resumido para facilitar la lectura. En este escenario, debe seguir la dirección URL de cada archivo para acceder al archivo.

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
| `_links.self.href` | Dirección URL de solicitud GET utilizada para descargar un archivo en el directorio. |


Copie el `href` valor de cualquier objeto de archivo de la `data` matriz y, a continuación, continúe con el paso siguiente.

## Descargar los datos del archivo

Para descargar los datos del archivo, realice una solicitud GET al `"href"` valor copiado en el paso anterior para [recuperar los archivos](#retrieving-your-files).

>[!NOTE] Si realiza esta solicitud directamente en la línea de comandos, es posible que se le pregunte si desea agregar un resultado después de los encabezados de la solicitud. El siguiente ejemplo de solicitud utiliza `--output {FILENAME.FILETYPE}`.

**Formato API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | El ID de dataSetFile se devuelve en el `href` valor de un paso [](#retrieve-the-next-api-call-with-your-batch-id)anterior. |
| `{FILE_NAME}` | Nombre del archivo. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP] Asegúrese de que se encuentra en el directorio o la carpeta en los que desea guardar el archivo antes de realizar la solicitud GET.

**Respuesta**

La respuesta descarga el archivo solicitado en el directorio actual. En este ejemplo, el nombre de archivo es &quot;filename.parquet&quot;.

![Terminal](./images/download-scores/response.png)

## Descargar un segmento configurado con la API del cliente {#segment}

Una forma alternativa de descargar los datos de puntuación es mediante la exportación de la audiencia a un conjunto de datos. Una vez completado correctamente un trabajo de segmentación (el valor del `status` atributo es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos en el que se pueda acceder a él y tomar medidas al respecto. Para obtener más información sobre la segmentación, visite la descripción general [de la](../../segmentation/home.md)segmentación.

>[!IMPORTANT] Para utilizar este método de exportación, es necesario habilitar el Perfil del cliente en tiempo real para el conjunto de datos.

La sección [Exportar un segmento](../../segmentation/tutorials/evaluate-a-segment.md) de la guía de evaluación de segmentos abarca los pasos necesarios para exportar un conjunto de datos de audiencia. La guía describe y proporciona ejemplos de lo siguiente:

- **Crear un conjunto de datos de destinatario:** Cree el conjunto de datos para albergar miembros de la audiencia.
- **Generar perfiles de audiencia en el conjunto de datos:** Rellene el conjunto de datos con Perfiles individuales XDM en función de los resultados de un trabajo de segmento.
- **Monitorear el progreso de exportación:** Compruebe el progreso actual del proceso de exportación.
- **Leer datos de audiencia:** Recupere los Perfiles individuales XDM resultantes que representan a los miembros de la audiencia.

## Pasos siguientes

Este documento describe los pasos necesarios para descargar puntuaciones de AI de cliente. Ahora puede seguir explorando los otros servicios [](../home.md) inteligentes y las guías que se ofrecen.
