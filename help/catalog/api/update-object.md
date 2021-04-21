---
keywords: Experience Platform;inicio;temas populares;catálogo;api;actualizar un objeto
solution: Experience Platform
title: Actualizar un objeto de catálogo
topic-legacy: developer guide
description: Puede actualizar parte de un objeto Catalog incluyendo su ID en la ruta de una solicitud del PATCH. Este documento cubre el uso de campos y el uso de notación de parches JSON para realizar operaciones de PATCH en objetos Catalog.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# Actualizar un objeto de catálogo

Puede actualizar parte de un objeto [!DNL Catalog] incluyendo su ID en la ruta de una solicitud del PATCH. Este documento cubre los dos métodos para realizar operaciones de PATCH en objetos Catalog:

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
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a actualizar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. Al realizar una solicitud de GET para este conjunto de datos, ahora se muestra que solo se han actualizado los `name` y `description` mientras que todos los demás valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Actualización mediante notación de parche JSON

La siguiente llamada de ejemplo muestra cómo actualizar un objeto mediante JSON Patch, como se describe en [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato de API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a actualizar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los campos `name` y `description` de un conjunto de datos a los valores proporcionados en cada objeto de parche JSON. Al utilizar JSON Patch, también debe establecer el encabezado Content-Type en `application/json-patch+json`.

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

Una respuesta correcta devuelve una matriz que contiene el ID del objeto actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. Al realizar una solicitud de GET para este objeto, ahora se muestra que solo se han actualizado los valores `name` y `description`, mientras que el resto de valores permanecen sin cambios.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
