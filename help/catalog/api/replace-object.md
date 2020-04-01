---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Reemplazar un objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: a753c6460bfe89e2b78fb3e087e9ba7397206dec

---


# Reemplazar un objeto

Puede sobrescribir el contenido de un objeto Catalog mediante una solicitud PUT, donde todo el recurso se reemplaza por la carga útil de la solicitud.

>[!NOTE] Si sólo necesita actualizar algunos campos específicos dentro de un objeto Catalog, el uso de una solicitud PATCH puede resultar más eficaz.

**Formato API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a reemplazar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud sobrescribe un conjunto de datos con los valores proporcionados en la carga útil.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del objeto sobrescrito. Este ID debe coincidir con el enviado en la solicitud PUT. Al realizar una solicitud GET para este objeto, ahora se muestra que sus detalles se han sustituido por los proporcionados en la carga útil de la solicitud PUT anterior.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
