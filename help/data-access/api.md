---
keywords: Experience Platform;inicio;temas populares;acceso a datos;python sdk;spark sdk;acceso a datos api;exportar;Exportar
solution: Experience Platform
title: Guía de API de acceso a datos
topic: developer guide
description: La API de acceso a datos admite Adobe Experience Platform al proporcionar a los desarrolladores una interfaz RESTful centrada en la capacidad de descubrimiento y accesibilidad de conjuntos de datos ingestados dentro de Experience Platform.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---


# Guía de API de acceso a datos

La API de acceso a datos admite Adobe Experience Platform al proporcionar a los usuarios una interfaz RESTful centrada en la capacidad de descubrimiento y accesibilidad de conjuntos de datos ingestados dentro de [!DNL Experience Platform].

![Acceso a datos en el Experience Platform](images/Data_Access_Experience_Platform.png)

## Referencia de especificación de API

La documentación de referencia de la API Swagger se encuentra [aquí](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminología

Descripción de algunos términos de uso común a lo largo de este documento.

| Término | Descripción |
| ----- | ------------ |
| Conjunto de datos | Recopilación de datos que incluye esquemas y campos. |
| Lote | Conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. |

## Recuperar lista de archivos dentro de un lote

Mediante el uso de un identificador de lote (batchID), la API de acceso a datos puede recuperar una lista de archivos pertenecientes a ese lote concreto.

**Formato API**

```http
GET /batches/{BATCH_ID}/files
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote especificado. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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

La matriz `"data"` contiene una lista de todos los archivos dentro del lote especificado. Cada archivo devuelto tiene su propia ID única (`{FILE_ID}`) incluida en el campo `"dataSetFileId"`. Esta ID única se puede utilizar para acceder al archivo o descargarlo.

| Propiedad | Descripción |
| -------- | ----------- |
| `data.dataSetFileId` | El ID de archivo de cada archivo del lote especificado. |
| `data._links.self.href` | La dirección URL para acceder al archivo. |

## Acceso y descarga de archivos dentro de un lote

Mediante el uso de un identificador de archivo (`{FILE_ID}`), la API de acceso a datos se puede utilizar para acceder a detalles específicos de un archivo, incluido su nombre, tamaño en bytes y un vínculo para descargar.

La respuesta contendrá una matriz de datos. Según si el archivo señalado por el ID es un archivo individual o un directorio, la matriz de datos devuelta puede contener una única entrada o una lista de archivos pertenecientes a ese directorio. Cada elemento de archivo incluirá los detalles del archivo.

**Formato API**

```http
GET /files/{FILE_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | Igual a `"dataSetFileId"`, el ID del archivo al que se va a acceder. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.name` | Nombre del archivo (p. ej. perfiles.csv). |
| `data.length` | Tamaño del archivo (en bytes). |
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
| `data.name` | Nombre del archivo (p. ej. perfiles.csv). |
| `data._links.self.href` | Dirección URL para descargar el archivo. |

## Acceso al contenido de un archivo

La API [!DNL Data Access] también puede utilizarse para acceder al contenido de un archivo. Esto se puede utilizar para descargar el contenido en una fuente externa.

**Formato API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_NAME}` | Nombre del archivo al que está intentando acceder. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_ID}` | ID del archivo dentro de un conjunto de datos. |
| `{FILE_NAME}` | Nombre completo del archivo (por ejemplo: perfiles.csv). |

**Respuesta**

`Contents of the file`

## Ejemplos de código adicionales

Para obtener más ejemplos, consulte el [tutorial de acceso a datos](tutorials/dataset-data.md).

## Suscripción a eventos de ingesta de datos

[!DNL Platform] pone a disposición de la suscripción eventos específicos de alto valor mediante la consola [ de desarrollo de ](https://www.adobe.com/go/devs_console_ui)Adobe. Por ejemplo, puede suscribirse a eventos de ingesta de datos para recibir notificaciones de posibles retrasos y errores. Consulte el tutorial sobre [suscripción a notificaciones de ingesta de datos](../ingestion/quality/subscribe-events.md) para obtener más información.