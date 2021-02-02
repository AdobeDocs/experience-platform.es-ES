---
keywords: Experience Platform;ai de atribución;puntuaciones de acceso;temas populares;puntuaciones de descarga;puntuaciones de ai de atribución;exportar;Exportar
solution: Experience Platform, Intelligent Services
title: Acceso a las puntuaciones en la Attribution AI
topic: Accessing scores
description: Este documento sirve como guía para descargar puntuaciones para Attribution AI.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 2%

---


# Descarga de puntuaciones en Attribution AI

Este documento sirve como guía para descargar puntuaciones para Attribution AI.

## Primeros pasos

Attribution AI le permite descargar puntuaciones en el formato de archivo Parquet. Este tutorial requiere que haya leído y terminado la sección de puntuaciones de Attribution AI de descarga en la guía [introducción](./getting-started.md).

Además, para acceder a las puntuaciones de Attribution AI, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite la [guía del usuario de Attribution AI](./user-guide.md). Si ha creado recientemente una instancia de servicio y aún está en formación y puntaje, espere 24 horas para que termine de ejecutarse.

## Busque su ID de conjunto de datos {#dataset-id}

En la instancia de servicio para obtener información sobre Attribution AI, haga clic en la lista desplegable *Más acciones* en la navegación superior derecha y, a continuación, seleccione **[!UICONTROL Puntuaciones de acceso]**.

![más acciones](./images/download-scores/more-actions.png)

Aparece un nuevo cuadro de diálogo que contiene un vínculo a la documentación de las puntuaciones de descarga y al ID del conjunto de datos de la instancia actual. Copie el ID del conjunto de datos en el portapapeles y continúe con el paso siguiente.

![Id. de conjunto de datos](../customer-ai/images/download-scores/access-scores.png)

## Recupere su ID de lote {#retrieve-your-batch-id}

Con el ID del conjunto de datos del paso anterior, debe realizar una llamada a la API del catálogo para recuperar un ID de lote. Se utilizan parámetros de consulta adicionales para esta llamada de API a fin de devolver el último lote exitoso en lugar de una lista de lotes que pertenecen a su organización. Para devolver lotes adicionales, aumente el número del parámetro de consulta `limit` a la cantidad deseada que desee que se devuelva. Para obtener más información sobre los tipos de parámetros de consulta disponibles, visite la guía sobre [filtrado de datos del catálogo mediante parámetros de consulta](../../catalog/api/filter-data.md).

**Formato API**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto de ID de lote. En este ejemplo, el valor Key del objeto devuelto es el ID de lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie el ID de lote para utilizarlo en la siguiente llamada de API.

>[!NOTE]
>
> La siguiente respuesta ha tenido el objeto `tags` reformado para facilitar la lectura.

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

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID de lote que se recuperó en el paso anterior [recupere el ID de lote](#retrieve-your-batch-id). |

**Solicitud**

Con su propio ID de lote, realice la siguiente solicitud.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene un objeto `_links`. Dentro del objeto `_links` hay un `href` con una nueva llamada de API como valor. Copie este valor para continuar con el paso siguiente.

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

Utilizando el valor `href` obtenido en el paso anterior como una llamada de API, realice una nueva solicitud de GET para recuperar el directorio de archivos.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | El ID de dataSetFile se devuelve en el valor `href` del [paso anterior](#retrieve-the-next-api-call-with-your-batch-id). También se puede acceder a ella en la matriz `data`, bajo el tipo de objeto `dataSetFileId`. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
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
| `_links.self.href` | Dirección URL de solicitud de GET utilizada para descargar un archivo en el directorio. |


Copie el valor `href` para cualquier objeto de archivo de la matriz `data` y, a continuación, continúe con el paso siguiente.

## Descargar los datos del archivo

Para descargar los datos del archivo, realice una solicitud de GET al valor `"href"` que copió en el paso anterior [para recuperar los archivos](#retrieving-your-files).

>[!NOTE]
>
>Si realiza esta solicitud directamente en la línea de comandos, es posible que se le pregunte si desea agregar un resultado después de los encabezados de la solicitud. El siguiente ejemplo de solicitud utiliza `--output {FILENAME.FILETYPE}`.

**Formato API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASETFILE_ID}` | El ID de dataSetFile se devuelve en el valor `href` de un [paso anterior](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Nombre del archivo. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Antes de realizar la solicitud de GET, asegúrese de que se encuentra en el directorio o la carpeta en los que desea guardar el archivo.

**Respuesta**

La respuesta descarga el archivo solicitado en el directorio actual. En este ejemplo, el nombre de archivo es &quot;file.parquet&quot;.

![Terminal](./images/download-scores/terminal-output.png)

Las puntuaciones descargadas estarán en formato Parquet y necesitarán un [!DNL Spark] shell o un lector de parquet para vista de las puntuaciones. Para ver la puntuación sin procesar, puede utilizar [Herramientas de parquet de Apache](https://github.com/apache/parquet-mr/tree/master/parquet-tools). Las herramientas de parquet pueden analizar los datos con [!DNL Spark].

## Pasos siguientes

Este documento describió los pasos necesarios para descargar puntuaciones de Attribution AI. Para obtener más información sobre los resultados, visite la documentación de [entradas y salidas de AI de asignación](./input-output.md).

## Acceso a las puntuaciones mediante Snowflake

>[!IMPORTANT]
>
>Póngase en contacto con attributionai-support@adobe.com para obtener más información sobre el acceso a las puntuaciones mediante Snowflake.

Puede acceder a las puntuaciones de Attribution AI agregadas a través del Snowflake. Actualmente, debe enviar por correo electrónico la asistencia técnica de Adobe a attributionai-support@adobe.com para configurar y recibir las credenciales de Snowflake en su cuenta de lector.

Una vez que la asistencia de Adobe haya procesado su solicitud, se le proporcionará una dirección URL para la cuenta de lector al Snowflake y las credenciales correspondientes a continuación:

- URL del Snowflake
- Nombre de usuario
- Contraseña

>[!NOTE]
>
>La cuenta de lector es para consultar los datos mediante clientes SQL, hojas de cálculo y soluciones BI que admiten el conector JDBC.

Una vez que tenga las credenciales y la dirección URL, puede realizar la consulta de las tablas de modelos, agregadas por fecha de punto de contacto o fecha de conversión.

### Búsqueda de su esquema en Snowflake

Con las credenciales proporcionadas, inicie sesión en Snowflake. Haga clic en la ficha **Hojas de cálculo** en la navegación principal superior izquierda y, a continuación, navegue hasta el directorio de la base de datos en el panel izquierdo.

![Hojas de cálculo y navegación](./images/download-scores/edited_snowflake_1.png)

A continuación, haga clic en **Seleccionar Esquema** en la esquina superior derecha de la pantalla. En la ventana emergente que aparece, confirme que tiene seleccionada la base de datos correcta. A continuación, haga clic en la lista desplegable *Esquema* y seleccione uno de los esquemas enumerados. Puede realizar la consulta directamente desde las tablas de puntuación que aparecen bajo el esquema seleccionado.

![buscar un esquema](./images/download-scores/edited_snowflake_2.png)

## Conexión de PowerBI al Snowflake (opcional)

Las credenciales de Snowflake se pueden utilizar para configurar una conexión entre las bases de datos de PowerBI Desktop y Snowflake.

Primero, en el cuadro *Servidor*, escriba la dirección URL del Snowflake. A continuación, en *Almacén*, escriba &quot;XSMALL&quot;. A continuación, escriba su nombre de usuario y contraseña.

![ejemplo de POWERBI](./images/download-scores/powerbi-snowflake.png)

Una vez establecida la conexión, seleccione la base de datos Snowflake y, a continuación, seleccione el esquema adecuado. Ahora puede cargar todas las tablas.
