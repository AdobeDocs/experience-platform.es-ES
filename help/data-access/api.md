---
keywords: Experience Platform;inicio;temas populares;acceso a datos;sdk de python;spark sdk;api de acceso a datos;exportar;Exportar
solution: Experience Platform
title: Guía de API de acceso a datos
description: La API de acceso a datos es compatible con Adobe Experience Platform al proporcionar a los desarrolladores una interfaz RESTful centrada en la detección y accesibilidad de conjuntos de datos ingeridos dentro de Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 6%

---

# Guía de API de acceso a datos

La API de acceso a datos es compatible con Adobe Experience Platform al proporcionar a los usuarios una interfaz RESTful centrada en la detección y accesibilidad de conjuntos de datos ingeridos en [!DNL Experience Platform].

![Acceso a datos en el Experience Platform](images/Data_Access_Experience_Platform.png)

## Referencia de especificación de API

La documentación de referencia de la API de Swagger se encuentra aquí [aquí](https://www.adobe.io/experience-platform-apis/references/data-access/).

## Terminología

Descripción de algunos términos de uso común de este documento.

| Término | Descripción |
| ----- | ------------ |
| Conjunto de datos | Recopilación de datos que incluye esquemas y campos. |
| Lote | Conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. |

## Recuperar lista de archivos dentro de un lote

Mediante un identificador de lote (batchID), la API de acceso a datos puede recuperar una lista de archivos que pertenecen a ese lote en particular.

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

El `"data"` contiene una lista de todos los archivos del lote especificado. Cada archivo devuelto tiene su propio ID único (`{FILE_ID}`) incluido en `"dataSetFileId"` field. A continuación, este ID único se puede utilizar para acceder al archivo o descargarlo.

| Propiedad | Descripción |
| -------- | ----------- |
| `data.dataSetFileId` | Id. de archivo para cada archivo del lote especificado. |
| `data._links.self.href` | URL para acceder al archivo. |

## Acceso y descarga de archivos dentro de un lote

Utilizando un identificador de archivo (`{FILE_ID}`), la API de acceso a datos se puede utilizar para acceder a detalles específicos de un archivo, incluido su nombre, tamaño en bytes y un vínculo para descargar.

La respuesta contendrá una matriz de datos. Dependiendo de si el archivo al que apunta el ID es un archivo individual o un directorio, la matriz de datos devuelta puede contener una sola entrada o una lista de archivos pertenecientes a ese directorio. Cada elemento de archivo incluye los detalles del archivo.

**Formato de API**

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
| `data.name` | Nombre del archivo (p. ej. profiles.csv). |
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
| `data.name` | Nombre del archivo (p. ej. profiles.csv). |
| `data._links.self.href` | Dirección URL para descargar el archivo. |

## Acceder al contenido de un archivo

El [!DNL Data Access] API también se puede utilizar para acceder al contenido de un archivo. A continuación, se puede utilizar para descargar el contenido en una fuente externa.

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
| `{FILE_NAME}` | El nombre completo del archivo (por ejemplo profiles.csv). |

**Respuesta**

`Contents of the file`

## Ejemplos de código adicionales

Para obtener más ejemplos, consulte la [tutorial de acceso a datos](tutorials/dataset-data.md).

## Suscripción a eventos de ingesta de datos

[!DNL Platform] ofrece la posibilidad de suscribirse a eventos específicos de alto valor a través del [Consola de Adobe Developer](https://www.adobe.com/go/devs_console_ui). Por ejemplo, puede suscribirse a eventos de ingesta de datos para recibir notificaciones de posibles retrasos y errores. Consulte el tutorial sobre [suscripción a notificaciones de ingesta de datos](../ingestion/quality/subscribe-events.md) para obtener más información.
