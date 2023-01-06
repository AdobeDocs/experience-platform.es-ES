---
keywords: Experience Platform;inicio;temas populares;catálogo;api;actualizar un objeto
solution: Experience Platform
title: Actualizar un objeto de catálogo
description: Puede actualizar parte de un objeto Catalog incluyendo su ID en la ruta de una solicitud del PATCH. Este documento cubre el uso de campos y el uso de notación de parches JSON para realizar operaciones de PATCH en objetos Catalog.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---

# Actualizar un objeto de catálogo

Puede actualizar parte de un [!DNL Catalog] al incluir su ID en la ruta de una solicitud de PATCH. Este documento cubre los dos métodos para realizar operaciones de PATCH en objetos Catalog:

* Uso de campos
* Uso de la notación de parches JSON

>[!NOTE]
>
>Las operaciones del PATCH en un objeto no pueden modificar sus campos ampliables, que representan objetos interrelacionados. Las modificaciones en objetos interrelacionados deben realizarse directamente.

## Actualización mediante campos

La siguiente llamada de ejemplo muestra cómo actualizar un objeto utilizando campos y valores.

**Formato de API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a actualizar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza el `name` y `description` campos de un conjunto de datos a los valores proporcionados en la carga útil. Los campos de objeto que no se van a actualizar se pueden excluir de la carga útil.

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

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. Al realizar una solicitud de GET para este conjunto de datos, ahora se muestra que solo la variable `name` y `description` se han actualizado, mientras que todos los demás valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Actualización mediante notación de parche JSON

La siguiente llamada de ejemplo muestra cómo actualizar un objeto mediante JSON Patch, tal como se describe en [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato de API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a actualizar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza el `name` y `description` campos de un conjunto de datos con los valores proporcionados en cada objeto JSON Patch. Al utilizar JSON Patch, también debe establecer el encabezado Content-Type en `application/json-patch+json`.

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

Una respuesta correcta devuelve una matriz que contiene el ID del objeto actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. Al realizar una solicitud de GET para este objeto, ahora se muestra que solo la variable `name` y `description` se han actualizado, mientras que todos los demás valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
