---
keywords: Experience Platform;inicio;temas populares;crear lote;servicio de catálogo;api
solution: Experience Platform
title: Crear un lote en la API
topic-legacy: developer guide
description: Puede crear un lote realizando una solicitud de POST al extremo /batches en la API del catálogo.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 5%

---

# Crear un lote

Para que un conjunto de datos pueda introducir datos, debe tener un lote asociado a él. Al usar la variable `id` de un conjunto de datos existente, puede crear un lote realizando una solicitud de POST al `/batches` en la variable [!DNL Catalog] API.

**Formato de API**

```HTTP
POST /batches
```

**Solicitud**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `datasetId` | La variable `id` del conjunto de datos con el que se asociará el lote. |

**Respuesta**

Una respuesta correcta devuelve el Estado HTTP 201 (Creado) y un objeto de respuesta que contiene detalles del lote recién creado, incluido su `id`, una cadena generada por el sistema de solo lectura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
