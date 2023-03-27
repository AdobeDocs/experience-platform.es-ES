---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;lote;habilitar conjunto de datos;información general sobre ingesta por lotes;información general;información general sobre ingesta por lotes
solution: Experience Platform
title: Información general sobre la API de ingesta de lotes
description: La API de ingesta por lotes de Adobe Experience Platform le permite introducir datos en Platform como archivos por lotes. Los datos introducidos pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o los datos que se ajustan a un esquema conocido en el registro del Modelo de datos de experiencia (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 7%

---

# Información general sobre la API de ingesta por lotes

La API de ingesta por lotes de Adobe Experience Platform le permite introducir datos en Platform como archivos por lotes. Los datos que se introducen pueden ser datos de perfil de un archivo plano (como un archivo Parquet) o datos que se ajustan a un esquema conocido en la [!DNL Experience Data Model] (XDM).

La variable [Referencia de la API de ingesta de lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) proporciona información adicional sobre estas llamadas a API.

El diagrama siguiente describe el proceso de ingesta por lotes:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte del [API de ingesta de lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Antes de continuar, revise la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

### [!DNL Data Ingestion] requisitos previos

- Los datos que se van a cargar deben estar en los formatos Parquet o JSON.
- Un conjunto de datos creado en la variable [[!DNL Catalog services]](../../catalog/home.md).
- El contenido del archivo de parquet debe coincidir con un subconjunto del esquema del conjunto de datos que se está cargando en.
- Tenga su token de acceso único después de la autenticación.

### Prácticas recomendadas sobre la ingesta por lotes

- El tamaño recomendado del lote está entre 256 MB y 100 GB.
- Cada lote debe contener como máximo 1500 archivos.

### Restricciones de ingesta por lotes

La ingesta de datos por lotes tiene algunas restricciones:

- Número máximo de archivos por lote: 1500
- Tamaño máximo del lote: 100 GB
- Número máximo de propiedades o campos por fila: 10000
- Número máximo de lotes por minuto, por usuario: 138

>[!NOTE]
>
>Para cargar un archivo de más de 512 MB, el archivo deberá dividirse en trozos más pequeños. Las instrucciones para cargar un archivo grande se encuentran en la sección [sección de carga de archivos grandes de este documento](#large-file-upload---create-file).

### Tipos

Al ingerir datos, es importante comprender cómo [!DNL Experience Data Model] Los esquemas (XDM) funcionan. Para obtener más información sobre cómo se asignan los tipos de campos XDM a diferentes formatos, lea la [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md).

Hay cierta flexibilidad a la hora de introducir datos: si un tipo no coincide con lo que hay en el esquema de destino, los datos se convertirán al tipo de destino expresado. Si no puede, fallará el lote con un `TypeCompatibilityException`.

Por ejemplo, ni JSON ni CSV tienen un `date` o `date-time` tipo . Como resultado, estos valores se expresan mediante [Cadenas con formato ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15&quot;:05:59.000-08:00&quot;) o Tiempo Unix formateados en milisegundos (1531263959000) y se convierten en el momento de la ingesta al tipo XDM de destino.

La tabla siguiente muestra las conversiones admitidas al introducir datos.

| Entrante (fila) frente a Target (col.) | Cadena | Byte | corto | Número entero | Largo | Doble | Fecha | Fecha-hora | Objeto | Mapa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Cadena | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| corto | X | X | X | X | X | X |  |  |  |  |
| Número entero | X | X | X | X | X | X |  |  |  |  |
| Largo | X | X | X | X | X | X | X | X |  |  |
| Doble | X | X | X | X | X | X |  |  |  |  |
| Fecha |  |  |  |  |  |  | X |  |  |  |
| Fecha-hora |  |  |  |  |  |  |  | X |  |  |
| Objeto |  |  |  |  |  |  |  |  | X | X |
| Mapa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Los booleanos y las matrices no se pueden convertir a otros tipos.

## Uso de la API

La variable [!DNL Data Ingestion] La API le permite introducir datos como lotes (una unidad de datos que consta de uno o varios archivos que se van a introducir como una sola unidad) en [!DNL Experience Platform] en tres pasos básicos:

1. Cree un nuevo lote.
2. Cargue archivos a un conjunto de datos especificado que coincida con el esquema XDM de los datos.
3. Indica el final del lote.

## Crear un lote

Para poder agregar datos a un conjunto de datos, estos deben vincularse a un lote que luego se cargará en un conjunto de datos especificado.

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `datasetId` | El ID del conjunto de datos en el que se cargarán los archivos. |

**Respuesta**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El ID del lote que se acaba de crear (se utiliza en solicitudes posteriores). |
| `relatedObjects.id` | El ID del conjunto de datos en el que se cargarán los archivos. |

## Carga de archivos

Después de crear correctamente un nuevo lote para su carga, los archivos se pueden cargar en un conjunto de datos específico.

Puede cargar archivos mediante la API de carga de archivos pequeños. Sin embargo, si los archivos son demasiado grandes y se supera el límite de la puerta de enlace (como los tiempos de espera extendidos, las solicitudes de tamaño de cuerpo excedidos y otras restricciones), puede cambiar a la API de carga de archivos grandes. Esta API carga el archivo en fragmentos y vincula los datos mediante la llamada API de finalización de carga de archivos grandes.

>[!NOTE]
>
>La ingesta por lotes se puede utilizar para actualizar los datos de forma incremental en el Almacenamiento de perfiles. Para obtener más información, consulte la sección sobre [actualización de un lote](#patch-a-batch) en el [guía para desarrolladores sobre ingesta por lotes](api-overview.md).

>[!INFO]
>
>Los ejemplos siguientes utilizan la variable [Apache Parquet](https://parquet.apache.org/docs/) formato de archivo. Puede encontrar un ejemplo que utilice el formato de archivo JSON en la [guía para desarrolladores sobre ingesta por lotes](api-overview.md).

### Carga de archivo pequeño

Una vez creado un lote, los datos se pueden cargar en un conjunto de datos preexistente.  El archivo que se está cargando debe coincidir con su esquema XDM al que se hace referencia.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos para cargar archivos. |
| `{FILE_NAME}` | El nombre del archivo tal como se verá en el conjunto de datos. |

**Solicitud**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta y nombre de archivo del archivo que se va a cargar en el conjunto de datos. |

**Respuesta**

```JSON
#Status 200 OK, with empty response body
```

### Carga de archivo grande: crear archivo

Para cargar un archivo grande, el archivo debe dividirse en fragmentos más pequeños y cargarse de uno en uno.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos que incorpora los archivos. |
| `{FILE_NAME}` | El nombre del archivo tal como se verá en el conjunto de datos. |

**Solicitud**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

```JSON
#Status 201 CREATED, with empty response body
```

### Carga de archivos grande: cargue las partes siguientes

Una vez creado el archivo, todos los fragmentos posteriores se pueden cargar realizando solicitudes de PATCH repetidas, una para cada sección del archivo.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote. |
| `{DATASET_ID}` | El ID del conjunto de datos en el que se cargarán los archivos. |
| `{FILE_NAME}` | Nombre del archivo tal como se verá en el conjunto de datos. |

**Solicitud**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta y nombre de archivo del archivo que se va a cargar en el conjunto de datos. |

**Respuesta**

```JSON
#Status 200 OK, with empty response
```

## Finalización del lote de señales

Una vez cargados todos los archivos en el lote, se puede indicar que el lote ha finalizado. Al hacer esto, la variable [!DNL Catalog] Las entradas DataSetFile se crean para los archivos completados y se asocian al lote generado anteriormente. La variable [!DNL Catalog] a continuación, se marca como correcto, lo que déclencheur los flujos descendentes a la ingesta de los datos disponibles.

**Solicitud**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que se cargará en el conjunto de datos. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Respuesta**

```JSON
#Status 200 OK, with empty response
```

## Comprobar el estado del lote

Mientras esperan que los archivos se carguen en el lote, se puede comprobar el estado del lote para ver su progreso.

**Formato de API**

```http
GET /batch/{BATCH_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que se está comprobando. |

**Solicitud**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{USER_ID}` | ID del usuario que creó o actualizó el lote. |

La variable `"status"` es lo que muestra el estado actual del lote solicitado. Los lotes pueden tener uno de los siguientes estados:

## Estados de ingesta por lotes

| Estado | Descripción |
| ------ | ----------- |
| Abandonado | El lote no se ha completado en el intervalo de tiempo esperado. |
| Anulado | Una operación de anulación tiene **explícitamente** se ha llamado (a través de la API de ingesta de lotes) para el lote especificado. Una vez que el lote está en estado &quot;Loaded&quot;, no se puede anular. |
| Activo | El lote se ha promocionado correctamente y está disponible para el consumo descendente. Este estado se puede utilizar de forma intercambiable con &quot;Success&quot;. |
| Eliminado | Los datos del lote se han eliminado por completo. |
| Fallido | Estado de terminal que resulta de una configuración incorrecta o de datos incorrectos. Los datos de un lote fallido **not** aparece. Este estado se puede utilizar de forma intercambiable con &quot;Fallo&quot;. |
| Inactivo | El lote se promocionó correctamente, pero se ha revertido o ha caducado. El lote ya no está disponible para el consumo descendente. |
| Cargado | Los datos del lote se completan y el lote está listo para su promoción. |
| Carga | Los datos de este lote se están cargando y el lote está actualmente **not** listo para ser promocionado. |
| Reintentando | Se están procesando los datos de este lote. Sin embargo, debido a un error del sistema o transitorio, el lote falló, por lo que se está reintentando este lote. |
| Ensayo | La fase de ensayo del proceso de promoción de un lote se ha completado y el trabajo de ingesta se ha ejecutado. |
| Ensayo | Se están procesando los datos del lote. |
| Estancado | Se están procesando los datos del lote. Sin embargo, la promoción por lotes se ha estancado después de varios reintentos. |
