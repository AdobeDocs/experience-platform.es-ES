---
keywords: Experience Platform;inicio;temas populares;acceso a datos;sdk de python;spark sdk;api de acceso a datos;exportar;Exportar
solution: Experience Platform
title: Guía de API de acceso a datos
description: La API de acceso a datos es compatible con Adobe Experience Platform al proporcionar a los desarrolladores una interfaz RESTful centrada en la detección y accesibilidad de conjuntos de datos ingeridos dentro de Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 1070c34bcd4577fcc5f0ac160196450db3aab9b0
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 5%

---

# Guía de API de acceso a datos

>[!IMPORTANT]
>
>La API de acceso a datos está **en desuso**. Se recomienda utilizar Destinos para exportar datos desde Adobe Experience Platform. Para obtener más información, consulte la [documentación de destinos de exportación de conjuntos de datos](../destinations/destination-types.md#dataset-export-destinations).

La API de acceso a datos admite Adobe Experience Platform al proporcionar a los usuarios una interfaz RESTful centrada en la detección y accesibilidad de conjuntos de datos ingeridos en [!DNL Experience Platform].

![Diagrama de cómo el acceso a datos facilita la detección y accesibilidad de los conjuntos de datos ingeridos dentro de Experience Platform.](images/Data_Access_Experience_Platform.png)

## Referencia de especificación de API

La documentación de referencia de OpenAPI se encuentra [aquí](https://developer.adobe.com/experience-platform-apis/references/data-access/).

## Terminología {#terminology}

En la tabla se describen algunos términos que se utilizan normalmente en este documento.

| Término | Descripción |
| ----- | ------------ |
| Conjunto de datos | Recopilación de datos que incluye un esquema y campos. |
| Lote | Conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. |

## Recuperar lista de archivos dentro de un lote {#retrieve-list-of-files-in-a-batch}

Para recuperar una lista de archivos pertenecientes a un lote concreto, utilice el identificador de lote (batchID) con la API de acceso a datos.

**Formato de API**

```http
GET /batches/{BATCH_ID}/files
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote especificado. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

La matriz `"data"` contiene una lista de todos los archivos del lote especificado. Cada archivo devuelto tiene su propio identificador único (`{FILE_ID}`) contenido en el campo `"dataSetFileId"`. Puede utilizar este ID único para acceder al archivo o descargarlo.

| Propiedad | Descripción |
| -------- | ----------- |
| `data.dataSetFileId` | Id. de archivo para cada archivo del lote especificado. |
| `data._links.self.href` | URL para acceder al archivo. |

## Acceso y descarga de archivos dentro de un lote

Para obtener acceso a detalles específicos de un archivo, use un identificador de archivo (`{FILE_ID}`) con la API de acceso a datos, incluido su nombre, tamaño en bytes y un vínculo para descargar.

La respuesta contiene una matriz de datos. Dependiendo de si el archivo al que apunta el ID es un archivo individual o un directorio, la matriz de datos devuelta puede contener una sola entrada o una lista de archivos pertenecientes a ese directorio. Cada elemento de archivo incluye los detalles del archivo.

**Formato de API**

```http
GET /files/{FILE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | Igual a `"dataSetFileId"`, el identificador del archivo al que se va a tener acceso. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta de un solo archivo**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
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
| `data.name` | Nombre del archivo (por ejemplo, `profiles.csv`). |
| `data.length` | El tamaño del archivo (en bytes). |
| `data._links.self.href` | Dirección URL para descargar el archivo. |

**Respuesta de directorio**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
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

Cuando se devuelve un directorio, contiene una matriz de todos los archivos del directorio.

| Propiedad | Descripción |
| -------- | ----------- |
| `data.name` | Nombre del archivo (por ejemplo, `profiles.csv`). |
| `data._links.self.href` | Dirección URL para descargar el archivo. |

## Acceder al contenido de un archivo {#access-file-contents}

También puede usar la API [!DNL Data Access] para tener acceso al contenido de un archivo. A continuación, puede descargar el contenido en una fuente externa.

**Formato de API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_NAME}` | El nombre del archivo al que intenta acceder. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | ID del archivo dentro de un conjunto de datos. |
| `{FILE_NAME}` | Nombre completo del archivo (por ejemplo, `profiles.csv`). |

**Respuesta**

`Contents of the file`

## Ejemplos de código adicionales

Para obtener más ejemplos, consulte el [tutorial de acceso a datos](tutorials/dataset-data.md).

## Suscripción a eventos de ingesta de datos {#subscribe-to-data-ingestion-events}

Puede suscribirse a eventos de alto valor específicos mediante [Adobe Developer Console](https://developer.adobe.com/console/). Por ejemplo, puede suscribirse a eventos de ingesta de datos para recibir notificaciones de posibles retrasos y errores. Consulte el tutorial sobre [suscripción a notificaciones de eventos de Adobe](../observability/alerts/subscribe.md) para obtener más información.
