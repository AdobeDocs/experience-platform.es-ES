---
keywords: Experience Platform;inicio;temas populares;acceso a datos;acceso a datos;acceso a datos;acceso a datos de consulta
solution: Experience Platform
title: Vista de datos de conjuntos de datos mediante la API de acceso a datos
topic: tutorial
type: Tutorial
description: Obtenga información sobre cómo localizar, acceder y descargar datos almacenados en un conjunto de datos mediante la API de acceso a datos de Adobe Experience Platform. También se le presentarán algunas de las características únicas de la API de acceso a datos, como paginación y descargas parciales.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 2%

---


# Datos del conjunto de datos de vista mediante la API [!DNL Data Access]

Este documento proporciona un tutorial paso a paso que explica cómo localizar, acceder y descargar datos almacenados en un conjunto de datos mediante la API [!DNL Data Access] de Adobe Experience Platform. También se le presentarán algunas de las características únicas de la API [!DNL Data Access], como paginación y descargas parciales.

## Primeros pasos

Este tutorial requiere un conocimiento práctico sobre cómo crear y rellenar un conjunto de datos. Consulte el [tutorial de creación de conjuntos de datos](../../catalog/datasets/create.md) para obtener más información.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API de plataforma.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Diagrama de secuencia

Este tutorial sigue los pasos descritos en el diagrama de secuencias a continuación, resaltando la funcionalidad básica de la API [!DNL Data Access].</br>
![](../images/sequence_diagram.png)

La API [!DNL Catalog] permite recuperar información sobre lotes y archivos. La API [!DNL Data Access] le permite acceder y descargar estos archivos a través de HTTP como descargas completas o parciales, según el tamaño del archivo.

## Localizar los datos

Antes de empezar a utilizar la API [!DNL Data Access], debe identificar la ubicación de los datos a los que desea acceder. En la API [!DNL Catalog], hay dos extremos que puede utilizar para examinar los metadatos de una organización y recuperar el ID de un lote o archivo al que desea acceder:

- `GET /batches`:: Devuelve una lista de lotes de su organización
- `GET /dataSetFiles`:: Devuelve una lista de archivos de su organización

Para obtener una lista completa de los extremos en la API [!DNL Catalog], consulte la [Referencia de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Recuperar una lista de lotes en la organización de IMS

Mediante la API [!DNL Catalog], puede devolver una lista de lotes en su organización:

**Formato API**

```http
GET /batches
```

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye un objeto que lista todos los lotes relacionados con la organización de IMS, con cada valor de nivel superior que representa un lote. Los objetos de lote individuales contienen los detalles de ese lote específico. La respuesta que se muestra a continuación se ha minimizado para el espacio.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
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

### Filtrar la lista de los lotes

A menudo se requiere que los filtros encuentren un lote concreto para recuperar los datos relevantes de un caso de uso concreto. Se pueden agregar parámetros a una solicitud `GET /batches` para filtrar la respuesta devuelta. La solicitud siguiente devolverá todos los lotes creados después de un tiempo especificado, dentro de un conjunto de datos determinado, ordenados por el momento en que se crearon.

**Formato API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Marca de tiempo de inicio en milisegundos (por ejemplo, 1514836799000). |
| `{DATASET_ID}` | El identificador del conjunto de datos. |
| `{SORT_BY}` | Ordena la respuesta según el valor proporcionado. Por ejemplo, `desc:created` ordena los objetos por fecha de creación en orden descendente. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

Puede encontrar una lista completa de los parámetros y filtros en la [referencia de la API del catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Recuperar una lista de todos los archivos pertenecientes a un lote concreto

Ahora que tiene el ID del lote al que desea acceder, puede utilizar la API [!DNL Data Access] para obtener una lista de los archivos pertenecientes a ese lote.

**Formato API**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data._links.self.href` | La dirección URL para acceder a este archivo. |

La respuesta contiene una matriz de datos que lista todos los archivos dentro del lote especificado. El ID de archivo de los archivos hace referencia a ellos, que se encuentra en el campo `dataSetFileId`.

## Acceso a un archivo mediante un ID de archivo

Una vez que tenga un ID de archivo único, puede utilizar la API [!DNL Data Access] para acceder a los detalles específicos del archivo, incluido su nombre, tamaño en bytes y un vínculo para descargarlo.

**Formato API**

```http
GET /files/{FILE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | Identificador del archivo al que desea acceder. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Según si el ID de archivo apunta a un archivo individual o a un directorio, la matriz de datos devuelta puede contener una única entrada o una lista de archivos pertenecientes a ese directorio. Cada elemento de archivo contendrá detalles como el nombre del archivo, el tamaño en bytes y un vínculo para descargar el archivo.

**Caso 1: El ID de archivo apunta a un solo archivo**

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

**Caso 2: El ID de archivo apunta a un directorio**

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

Esta respuesta devuelve un directorio que contiene dos archivos independientes, con los ID `{FILE_ID_2}` y `{FILE_ID_3}`. En este escenario, deberá seguir la dirección URL de cada archivo para acceder al archivo.

## Recuperar los metadatos de un archivo

Puede recuperar los metadatos de un archivo realizando una solicitud de HEAD. Esto devuelve los encabezados de metadatos del archivo, incluido su tamaño en bytes y en formato de archivo.

**Formato API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | Identificador del archivo. |
| `{FILE_NAME}` | El nombre del archivo (por ejemplo, perfiles.parquet) |

**Solicitud**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Los encabezados de respuesta contienen los metadatos del archivo consultado, incluidos:
- `Content-Length`:: Indica el tamaño de la carga útil en bytes
- `Content-Type`:: Indica el tipo de archivo.

## Acceso al contenido de un archivo

También puede acceder al contenido de un archivo mediante la API [!DNL Data Access].

**Formato API**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | Identificador del archivo. |
| `{FILE_NAME}` | El nombre del archivo (por ejemplo, perfiles.parquet). |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el contenido del archivo.

## Descargar contenido parcial de un archivo

La API [!DNL Data Access] permite descargar archivos en fragmentos. Se puede especificar un encabezado de rango durante una solicitud `GET /files/{FILE_ID}` para descargar un rango específico de bytes de un archivo. Si no se especifica el intervalo, la API descargará el archivo completo de forma predeterminada.

El ejemplo de HEAD en la [sección anterior](#retrieve-the-metadata-of-a-file) proporciona el tamaño de un archivo específico en bytes.

**Formato API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID} ` | Identificador del archivo. |
| `{FILE_NAME}` | El nombre del archivo (por ejemplo, perfiles.parquet) |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `Range: bytes=0-99` | Especifica el intervalo de bytes que se va a descargar. Si no se especifica esto, la API descargará el archivo completo. En este ejemplo, se descargarán los primeros 100 bytes. |

**Respuesta**

El cuerpo de la respuesta incluye los primeros 100 bytes del archivo (según lo especificado por el encabezado &quot;Intervalo&quot; en la solicitud) junto con el Estado HTTP 206 (Contenido parcial). La respuesta también incluye los siguientes encabezados:

- Content-Length: 100 (el número de bytes devueltos)
- Tipo de contenido: aplicación/parqué (se solicitó un archivo de parquet, por lo que el tipo de contenido de respuesta es `parquet`)
- Content-Range: bytes 0-99/249058 (el intervalo solicitado (0-99) del número total de bytes (249058))

## Configurar la paginación de respuestas de API

Las respuestas dentro de la API [!DNL Data Access] están paginadas. De forma predeterminada, el número máximo de entradas por página es 100. Los parámetros de paginación se pueden utilizar para modificar el comportamiento predeterminado.

- `limit`:: Puede especificar el número de entradas por página según sus necesidades utilizando el parámetro &quot;limit&quot;.
- `start`:: El desplazamiento se puede establecer mediante el parámetro de consulta &quot;inicio&quot;.
- `&`:: Puede utilizar un símbolo de unión para combinar varios parámetros en una sola llamada.

**Formato API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | Identificador de lote del lote al que intenta acceder. |
| `{OFFSET}` | El índice especificado para el inicio de la matriz de resultados (por ejemplo, inicio=0) |
| `{LIMIT}` | Controla cuántos resultados se devuelven en la matriz de resultados (por ejemplo, limit=1) |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**:

La respuesta contiene una matriz `"data"` con un solo elemento, tal como se especifica en el parámetro de solicitud `limit=1`. Este elemento es un objeto que contiene los detalles del primer archivo disponible, tal como se especifica en el parámetro `start=0` de la solicitud (recuerde que en la numeración basada en cero, el primer elemento es &quot;0&quot;).

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
