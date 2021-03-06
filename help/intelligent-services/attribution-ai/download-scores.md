---
keywords: Experience Platform;ai de atribución;acceder a puntuaciones;temas populares;descargar puntuaciones;atribución de puntuaciones de ai;exportar;Exportar
feature: Attribution AI
title: Descargar puntuaciones en Attribution AI
topic-legacy: Downloading scores
description: Este documento sirve como guía para descargar puntuaciones para Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 3%

---

# Descargar puntuaciones en Attribution AI

Este documento sirve como guía para descargar puntuaciones para Attribution AI.

## Primeros pasos

Attribution AI le permite descargar puntuaciones en el formato de archivo Parquet. Este tutorial requiere que haya leído y terminado la sección de descarga de puntuaciones de Attribution AI en la sección [introducción](./getting-started.md) guía.

Además, para acceder a las puntuaciones de Attribution AI, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite [Guía del usuario del Attribution AI](./user-guide.md). Si ha creado recientemente una instancia de servicio y sigue siendo de formación y puntuación, espere 24 horas para que termine de ejecutarse.

## Búsqueda del ID del conjunto de datos {#dataset-id}

En la instancia de servicio para obtener información sobre las Attribution AI, haga clic en el botón *Más acciones* en la navegación superior derecha y seleccione **[!UICONTROL Puntuaciones de acceso]**.

![más acciones](./images/download-scores/more-actions.png)

Aparece un nuevo cuadro de diálogo que contiene un vínculo a la documentación de descarga de puntuaciones y el ID del conjunto de datos para la instancia actual. Copie el ID del conjunto de datos en el portapapeles y continúe con el paso siguiente.

![ID de conjunto de datos](../customer-ai/images/download-scores/access-scores.png)

## Recuperar el ID de lote {#retrieve-your-batch-id}

Con el ID del conjunto de datos del paso anterior, debe realizar una llamada a la API del catálogo para recuperar un ID de lote. Para esta llamada de API se utilizan parámetros de consulta adicionales para devolver el último lote correcto en lugar de una lista de lotes pertenecientes a su organización. Para devolver lotes adicionales, aumente el número de la variable `limit` parámetro de consulta a la cantidad deseada que desee que se devuelva. Para obtener más información sobre los tipos de parámetros de consulta disponibles, visite la guía de [filtrado de datos del catálogo mediante parámetros de consulta](../../catalog/api/filter-data.md).

**Formato de API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos disponible en el cuadro de diálogo &quot;Puntuaciones de acceso&quot;. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto de ID de lote. En este ejemplo, el valor Key del objeto devuelto es el ID del lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie su ID de lote para utilizarlo en la siguiente llamada de API.

>[!NOTE]
>
> La siguiente respuesta ha tenido la variable `tags` objeto modificado para facilitar la lectura.

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
                "id": "5e8f81cf7a4ecb28a8d85b22"
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

Una vez que tenga su ID de lote, podrá realizar una nueva solicitud de GET a `/batches`. La solicitud devuelve un vínculo que se utiliza como la siguiente solicitud de API.

**Formato de API**

```http
GET batches/{BATCH_ID}/files
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID de lote recuperado en el paso anterior [recuperar el ID de lote](#retrieve-your-batch-id). |

**Solicitud**

Con su propio ID de lote, realice la siguiente solicitud.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un `_links` objeto. Dentro de `_links` el objeto es un `href` con una nueva llamada de API como su valor. Copie este valor para continuar con el paso siguiente.

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
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

## Recupere los archivos {#retrieving-your-files}

Al usar la variable `href` en el paso anterior como llamada a la API, realice una nueva solicitud de GET para recuperar el directorio de archivos.

**Formato de API**

```http
GET files/{DATASETFILE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | El ID dataSetFile se devuelve en la variable `href` del [paso anterior](#retrieve-the-next-api-call-with-your-batch-id). También se puede acceder a ella desde la `data` matriz bajo el tipo de objeto `dataSetFileId`. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta contiene una matriz de datos que puede tener una sola entrada o una lista de archivos pertenecientes a ese directorio. El ejemplo siguiente contiene una lista de archivos y se ha condensado para facilitar la lectura. En esta situación, debe seguir la dirección URL de cada archivo para acceder al archivo.

```json
{
    "data": [
        {
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
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

| Parámetro | Descripción |
| --------- | ----------- |
| `_links.self.href` | La URL de solicitud de GET utilizada para descargar un archivo en su directorio. |


Copie el `href` para cualquier objeto de archivo de la variable `data` y, a continuación, continúe con el paso siguiente.

## Descargar los datos del archivo

Para descargar los datos del archivo, realice una solicitud de GET a la `"href"` valor que ha copiado en el paso anterior [recuperación de archivos](#retrieving-your-files).

>[!NOTE]
>
>Si realiza esta solicitud directamente en la línea de comandos, es posible que se le pida que añada un resultado después de los encabezados de solicitud. El siguiente ejemplo de solicitud utiliza `--output {FILENAME.FILETYPE}`.

**Formato de API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | El ID dataSetFile se devuelve en la variable `href` de un [paso anterior](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Nombre del archivo. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Asegúrese de que está en el directorio o carpeta correcto en el que desea guardar el archivo antes de realizar la solicitud de GET.

**Respuesta**

La respuesta descarga el archivo solicitado en en el directorio actual. En este ejemplo, el nombre de archivo es &quot;file.parquet&quot;.

![Terminal](./images/download-scores/terminal-output.png)

Las puntuaciones descargadas estarán en formato Parquet y necesitarán una [!DNL Spark]-shell o lector de parquet para ver las puntuaciones. Para la visualización de puntuación sin procesar, puede utilizar [Herramientas de Apache Parquet](https://parquet.apache.org/docs/). Las herramientas de parquet pueden analizar los datos con [!DNL Spark].

## Pasos siguientes

Este documento describía los pasos necesarios para descargar puntuaciones de Attribution AI. Para obtener más información sobre los resultados de puntuación, visite el [Atribución de entrada y salida de IA](./input-output.md) documentación.

## Acceso a las puntuaciones mediante el Snowflake

>[!IMPORTANT]
>
>Póngase en contacto con attributionai-support@adobe.com para obtener más información sobre el acceso a puntuaciones con el Snowflake.

Puede acceder a las puntuaciones de Attribution AI agregadas a través del Snowflake . Actualmente, debe enviar por correo electrónico a la asistencia de Adobe a attributionai-support@adobe.com para configurar y recibir las credenciales de Snowflake en su cuenta de lector.

Una vez que la asistencia de Adobe ha procesado su solicitud, se le proporcionará una URL para la cuenta de lector al Snowflake y las credenciales correspondientes a continuación:

- URL del Snowflake
- Nombre de usuario
- Contraseña

>[!NOTE]
>
>La cuenta de lector es para consultar los datos usando clientes sql, hojas de cálculo y soluciones de BI que admiten el conector JDBC.

Una vez que tenga las credenciales y la dirección URL, puede consultar las tablas del modelo, agregadas por fecha del punto de contacto o fecha de conversión.

### Búsqueda del esquema en el Snowflake

Con las credenciales proporcionadas, inicie sesión en el Snowflake. Haga clic en el **Hojas de cálculo** en la barra de navegación principal superior izquierda, desplácese hasta el directorio de la base de datos en el panel izquierdo.

![Hojas de cálculo y navegación](./images/download-scores/edited_snowflake_1.png)

A continuación, haga clic en **Seleccionar esquema** en la esquina superior derecha de la pantalla. En la ventana emergente que aparece, confirme que tiene seleccionada la base de datos correcta. A continuación, haga clic en el *Esquema* y seleccione uno de los esquemas enumerados. Puede realizar consultas directamente desde las tablas de puntuación enumeradas en el esquema seleccionado.

![buscar un esquema](./images/download-scores/edited_snowflake_2.png)

## Conexión de PowerBI al Snowflake (opcional)

Las credenciales del Snowflake se pueden usar para configurar una conexión entre las bases de datos de PowerBI Desktop y Snowflake.

En primer lugar, en la sección *Servidor* , escriba la dirección URL del Snowflake. A continuación, en *Almacén*, escriba &quot;XSMALL&quot;. A continuación, escriba su nombre de usuario y contraseña.

![ejemplo de POWERBI](./images/download-scores/powerbi-snowflake.png)

Una vez establecida la conexión, seleccione la base de datos del Snowflake y, a continuación, seleccione el esquema adecuado. Ahora puede cargar todas las tablas.
