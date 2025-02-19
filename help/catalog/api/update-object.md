---
keywords: Experience Platform;inicio;temas populares;catálogo;api;actualizar un objeto
solution: Experience Platform
title: Actualizar un objeto de catálogo
description: Puede actualizar parte de un objeto Catalog incluyendo su ID en la ruta de una petición PATCH. Este documento cubre el uso de campos y el uso de la notación de parches JSON para realizar operaciones de PATCH en objetos de catálogo.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Actualizar un objeto Catalog

Puede actualizar parte de un objeto [!DNL Catalog] incluyendo su ID en la ruta de una petición PATCH. Este documento describe los dos métodos para realizar operaciones de PATCH en objetos Catalog:

* Uso de campos
* Uso de la notación de parches JSON

>[!NOTE]
>
>Las operaciones de PATCH en un objeto no pueden modificar sus campos expandibles, que representan objetos interrelacionados. Las modificaciones en objetos interrelacionados deben realizarse directamente.

## Actualizar mediante campos

La siguiente llamada de ejemplo muestra cómo actualizar un objeto mediante campos y valores.

**Formato de API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de objeto [!DNL Catalog] que se va a actualizar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | El identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los campos `name` y `description` de un conjunto de datos a los valores proporcionados en la carga útil. Los campos de objeto que no se vayan a actualizar se pueden excluir de la carga útil.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud de PATCH. Al realizar una solicitud GET para este conjunto de datos, ahora se muestra que solo se han actualizado `name` y `description`, mientras que el resto de valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Actualización mediante la notación de parches de JSON {#patch-notation}

La siguiente llamada de ejemplo muestra cómo actualizar un objeto mediante el parche JSON, como se describe en [RFC-6902](https://tools.ietf.org/html/rfc6902).

Para obtener más información sobre la sintaxis de parches de JSON, consulte la [guía de aspectos básicos de la API](../../landing/api-fundamentals.md#json-patch).

**Formato de API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de objeto [!DNL Catalog] que se va a actualizar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | El identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los campos `name` y `description` de un conjunto de datos a los valores proporcionados en cada objeto de parche JSON. Al utilizar el parche JSON, también debe establecer el encabezado Content-Type en `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del objeto actualizado. Este ID debe coincidir con el enviado en la solicitud de PATCH. Al realizar una petición GET para este objeto, ahora se muestra que solamente se han actualizado `name` y `description`, mientras que el resto de valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Actualización mediante la notación de PATCH v2 {#patch-v2-notation}

El extremo `/v2/dataSets/{DATASET_ID}` proporciona una forma más flexible de actualizar atributos de conjuntos de datos complejos o profundamente anidados.

Normalmente, cuando se actualiza un campo anidado profundamente (como `a.b.c.d`), cada nivel de la ruta de acceso ya debe existir. Si falta algún nivel, debe crear manualmente cada uno antes de establecer el valor final. Esto a menudo requiere varias operaciones, lo que añade complejidad y aumenta la posibilidad de errores.

El extremo `/v2/dataSets/{DATASET_ID}` crea automáticamente los niveles que faltan en la ruta de acceso. En lugar de comprobar y agregar manualmente `b` y `c` antes de establecer `d`, la operación de PATCH `v2` hace esto por usted.

Cuando envía una solicitud de PATCH al extremo `/v2/dataSets/{DATASET_ID}`, solo necesita enviar la estructura final y el sistema rellena las partes que faltan antes de aplicar la actualización.

>[!NOTE]
>
>Los encabezados `If-Match` y `If-None-Match` son opcionales para el extremo `/v2/dataSets/{id}`. Las solicitudes de PATCH a este extremo combinan actualizaciones de forma dinámica, lo que permite realizar modificaciones sin recuperar la última versión del conjunto de datos. Aunque esto reduce el riesgo de pérdida de datos debido a las actualizaciones simultáneas, puede usar `If-Match` con la última `etag` para asegurarse de que los cambios se apliquen únicamente a una versión específica. Como alternativa, `If-None-Match` evita actualizaciones si el conjunto de datos no ha cambiado desde la última versión conocida.

**Formato de API**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El identificador del conjunto de datos que se va a actualizar. |

**Solicitud**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos actualizado, que debe coincidir con el ID enviado en la solicitud de PATCH. Al realizar una petición GET para este objeto, ahora se muestra que el objeto `extensions.adobe_lakeHouse.rowExpiration` se ha creado sin requerir pasos de creación manuales previos.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### Ejemplo de conjunto de datos antes y después de la actualización

El siguiente JSON de ejemplo ilustra la estructura del conjunto de datos **antes de** la solicitud de PATCH, donde el objeto `extensions.adobe_lakeHouse.rowExpiration` no está presente en el conjunto de datos.

+++Seleccione para ver el ejemplo

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

El siguiente JSON muestra la estructura del conjunto de datos **después** de la solicitud de PATCH. La actualización crea automáticamente el objeto `extensions.adobe_lakeHouse.rowExpiration` que falta sin pasos de creación manuales anteriores. En este ejemplo se muestra cómo la solicitud de PATCH `/v2/` elimina la necesidad de realizar varias operaciones, lo que hace que las actualizaciones sean más sencillas y eficaces.


+++Seleccione para ver el ejemplo

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
