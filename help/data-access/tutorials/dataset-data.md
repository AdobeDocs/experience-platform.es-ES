---
keywords: Experience Platform;inicio;temas populares;acceso a datos;api de acceso a datos;acceso a datos de consulta
solution: Experience Platform
title: Ver datos del conjunto de datos mediante la API de acceso a datos
type: Tutorial
description: Obtenga información sobre cómo localizar, acceder y descargar datos almacenados en un conjunto de datos mediante la API de acceso a datos en Adobe Experience Platform. Este documento presenta algunas de las características únicas de la API de acceso a datos, como la paginación y las descargas parciales.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 9144a5f4cce88fc89973a7fea6d69384cc5f4ba1
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 8%

---

# Ver datos del conjunto de datos mediante la API [!DNL Data Access]

Utilice este tutorial paso a paso para aprender a localizar, acceder y descargar datos almacenados en un conjunto de datos mediante la API [!DNL Data Access] en Adobe Experience Platform. Este documento presenta algunas de las características únicas de la API [!DNL Data Access], como paginación y descargas parciales.

## Introducción

Este tutorial requiere una comprensión práctica sobre cómo crear y rellenar un conjunto de datos. Consulte el [tutorial de creación de conjuntos de datos](../../catalog/datasets/create.md) para obtener más información.

Las secciones siguientes proporcionan información adicional que necesita saber para realizar llamadas correctamente a las API de Platform.

### Lectura de llamadas de API de muestra {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](../../landing/api-authentication.md). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realiza la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Diagrama de secuencia

Este tutorial sigue los pasos descritos en el diagrama de secuencia siguiente, destacando la funcionalidad principal de la API [!DNL Data Access].

![Diagrama de secuencia de la funcionalidad principal de la API de acceso a datos.](../images/sequence_diagram.png)

Para recuperar información sobre lotes y archivos, use la API [!DNL Catalog]. Para acceder y descargar estos archivos a través de HTTP como descargas completas o parciales, según el tamaño del archivo, utilice la API [!DNL Data Access].

## Busque los datos

Antes de empezar a usar la API [!DNL Data Access], debe identificar la ubicación de los datos a los que desea acceder. En la API [!DNL Catalog], hay dos extremos que puede utilizar para examinar los metadatos de una organización y recuperar el ID de un lote o archivo al que desee tener acceso:

- `GET /batches`: Devuelve una lista de lotes bajo su organización
- `GET /dataSetFiles`: devuelve una lista de archivos de su organización

Para obtener una lista completa de los extremos en la API [!DNL Catalog], consulte la [Referencia de API](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Recupere una lista de lotes debajo de su organización

Con la API [!DNL Catalog], puede devolver una lista de lotes bajo su organización:

**Formato de API**

```http
GET /batches
```

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye un objeto que enumera todos los lotes relacionados con la organización, y cada valor de nivel superior representa un lote. Los objetos por lotes individuales contienen los detalles de ese lote específico. La respuesta siguiente se ha minimizado para el espacio.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### Filtrar la lista de lotes {#filter-batches-list}

A menudo, los filtros son necesarios para encontrar un lote concreto a fin de recuperar datos relevantes para un caso de uso determinado. Se pueden agregar parámetros a una solicitud `GET /batches` para filtrar la respuesta devuelta. La solicitud siguiente devuelve todos los lotes creados después de un tiempo especificado, dentro de un conjunto de datos concreto, ordenados por el momento en que se crearon.

**Formato de API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{START_TIMESTAMP}` | La marca de tiempo de inicio en milisegundos (por ejemplo, 1514836799000). |
| `{DATASET_ID}` | El identificador del conjunto de datos. |
| `{SORT_BY}` | Ordena la respuesta por el valor proporcionado. Por ejemplo, `desc:created` ordena los objetos por fecha de creación en orden descendente. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

Encontrará una lista completa de parámetros y filtros en la [Referencia de API de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Recupere una lista de todos los archivos que pertenecen a un lote concreto

Ahora que tiene el identificador del lote al que desea acceder, puede usar el API [!DNL Data Access] para obtener una lista de los archivos que pertenecen a ese lote.

**Formato de API**

```http
GET /batches/{BATCH_ID}/files
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | Identificador de lote del lote al que intenta acceder. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `data._links.self.href` | La URL para acceder a este archivo. |

La respuesta contiene una matriz de datos que enumera todos los archivos del lote especificado. Se hace referencia a los archivos por su ID de archivo, que se encuentra en el campo `dataSetFileId`.

## Acceso a un archivo mediante un ID de archivo {#access-file-with-file-id}

Una vez que tenga un identificador de archivo único, puede usar la API [!DNL Data Access] para obtener acceso a los detalles específicos del archivo, incluido su nombre, tamaño en bytes y un vínculo para descargarlo.

**Formato de API**

```http
GET /files/{FILE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | El identificador del archivo al que desea acceder. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Dependiendo de si el ID de archivo apunta a un archivo individual o a un directorio, la matriz de datos devuelta puede contener una sola entrada o una lista de archivos que pertenezcan a ese directorio. Cada elemento de archivo contiene detalles como el nombre del archivo, el tamaño en bytes y un vínculo para descargar el archivo.

**Caso 1: el id. de archivo apunta a un solo archivo**

**Respuesta**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
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

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | Nombre del archivo. |
| `_links.self.href` | Dirección URL para descargar el archivo. |

**Caso 2: el id. de archivo apunta a un directorio**

**Respuesta**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `data._links.self.href` | Dirección URL para descargar el archivo asociado. |

Esta respuesta devuelve un directorio que contiene dos archivos independientes, con los identificadores `{FILE_ID_2}` y `{FILE_ID_3}`. En este caso, debe seguir la dirección URL de cada archivo para acceder al archivo.

## Recuperación de los metadatos de un archivo

Puede recuperar los metadatos de un archivo realizando una solicitud al HEAD. Devuelve los encabezados de metadatos del archivo, incluido su tamaño en bytes y formato de archivo.

**Formato de API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | El identificador del archivo. |
| `{FILE_NAME}` | El nombre del archivo (por ejemplo, profiles.parquet) |

**Solicitud**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Los encabezados de respuesta contienen los metadatos del archivo consultado, que incluyen:

- `Content-Length`: indica el tamaño de la carga útil en bytes
- `Content-Type`: indica el tipo de archivo.

## Acceder al contenido de un archivo

También puede tener acceso al contenido de un archivo mediante la API [!DNL Data Access].

**Formato de API**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | El identificador del archivo. |
| `{FILE_NAME}` | El nombre del archivo (por ejemplo, profiles.parquet). |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el contenido del archivo.

## Descargar el contenido parcial de un archivo {#download-partial-file-contents}

Para descargar un intervalo específico de bytes de un archivo, especifique un encabezado de intervalo durante una solicitud `GET /files/{FILE_ID}` a la API [!DNL Data Access]. Si no se especifica el intervalo, la API descarga todo el archivo de forma predeterminada.

El ejemplo del HEAD en la [sección anterior](#retrieve-the-metadata-of-a-file) proporciona el tamaño de un archivo específico en bytes.

**Formato de API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID} ` | El identificador del archivo. |
| `{FILE_NAME}` | El nombre del archivo (por ejemplo, profiles.parquet) |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `Range: bytes=0-99` | Especifica el intervalo de bytes que se va a descargar. Si no se especifica, la API descarga todo el archivo. En este ejemplo, se descargan los primeros 100 bytes. |

**Respuesta**

El cuerpo de respuesta incluye los primeros 100 bytes del archivo (tal como especifica el encabezado &quot;Rango&quot; en la solicitud) junto con el estado HTTP 206 (Contenido parcial). La respuesta también incluye los siguientes encabezados:

- Content-Length: 100 (el número de bytes devueltos)
- Content-type: application/parquet (se solicitó un archivo Parquet y, por lo tanto, el tipo de contenido de respuesta es `parquet`)
- Content-Range: bytes 0-99/249058 (el intervalo solicitado (0-99) del número total de bytes (249058))

## Configuración de paginación de respuesta API {#configure-response-pagination}

Se paginan las respuestas en la API [!DNL Data Access]. De forma predeterminada, el número máximo de entradas por página es 100. Puede modificar el comportamiento predeterminado con los parámetros de paginación.

- `limit`: puede especificar el número de entradas por página según sus necesidades utilizando el parámetro &quot;limit&quot;.
- `start`: el desplazamiento se puede establecer mediante el parámetro de consulta &quot;start&quot;.
- `&`: puede utilizar un signo &amp; para combinar varios parámetros en una sola llamada.

**Formato de API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | Identificador de lote del lote al que intenta acceder. |
| `{OFFSET}` | El índice especificado para iniciar la matriz de resultados (por ejemplo, start=0) |
| `{LIMIT}` | Controla cuántos resultados se devuelven en la matriz de resultados (por ejemplo, limit=1) |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**:

La respuesta contiene una matriz `"data"` con un solo elemento, como se especifica en el parámetro de solicitud `limit=1`. Este elemento es un objeto que contiene los detalles del primer archivo disponible, según lo especificado por el parámetro `start=0` en la solicitud (recuerde que en la numeración basada en cero, el primer elemento es &quot;0&quot;).

El valor `_links.next.href` contiene el vínculo a la siguiente página de respuestas, donde puede ver que el parámetro `start` ha avanzado a `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
