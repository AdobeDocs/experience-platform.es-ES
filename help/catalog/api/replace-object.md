---
keywords: Experience Platform;inicio;temas populares;catálogo;api;reemplazar un objeto
solution: Experience Platform
title: Reemplazar un objeto de catálogo
description: Puede sobrescribir el contenido de un objeto Catalog mediante una solicitud del PUT, en la que todo el recurso se reemplaza por la carga útil de la solicitud.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 3%

---

# Reemplazar un objeto Catalog

Puede sobrescribir el contenido de un objeto [!DNL Catalog] mediante una solicitud de PUT, en la que todo el recurso se reemplaza por la carga útil de la solicitud.

>[!NOTE]
>
>Si solo necesita actualizar algunos campos específicos dentro de un objeto [!DNL Catalog], el uso de una solicitud de PATCH puede ser más eficiente.

**Formato de API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de objeto [!DNL Catalog] que se reemplazará. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | El identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud sobrescribe un conjunto de datos con los valores proporcionados en la carga útil.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del objeto sobrescrito. Este ID debe coincidir con el enviado en la solicitud del PUT. Al realizar una solicitud de GET para este objeto, ahora se muestra que sus detalles se han sustituido por los proporcionados en la carga útil de la solicitud de PUT anterior.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
