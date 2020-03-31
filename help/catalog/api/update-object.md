---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Actualizar un objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 4361032b419622d7decc02194d38885b114749e4

---


# Actualizar un objeto

Puede actualizar parte de un objeto Catalog incluyendo su ID en la ruta de una solicitud PATCH. Este documento cubre los dos métodos para realizar operaciones PATCH en objetos Catalog:

* Uso de campos
* Uso de notación de parche JSON

>[!NOTE] Las operaciones PATCH de un objeto no pueden modificar sus campos ampliables, que representan objetos interrelacionados.  Las modificaciones de los objetos interrelacionados deben realizarse directamente.

## Actualización mediante campos

La siguiente llamada de ejemplo muestra cómo actualizar un objeto mediante campos y valores.

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a actualizar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los campos `name` y `description` de un conjunto de datos a los valores proporcionados en la carga útil. Los campos de objeto que no se van a actualizar se pueden excluir de la carga útil.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud PATCH. Al realizar una solicitud GET para este conjunto de datos, ahora se muestra que solo se han actualizado `name` `description` y mientras que todos los demás valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Actualizar con notación de parche JSON

La siguiente llamada de ejemplo muestra cómo actualizar un objeto mediante JSON Patch, como se describe en [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a actualizar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los campos `name` y `description` de un conjunto de datos a los valores proporcionados en cada objeto JSON Patch. Al utilizar JSON Patch, también debe establecer el encabezado Content-Type en `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del objeto actualizado. Este ID debe coincidir con el enviado en la solicitud PATCH. Al realizar una solicitud GET para este objeto, ahora se muestra que solo se han actualizado `name` `description` y mientras que todos los demás valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
