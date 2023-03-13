---
keywords: Experience Platform;inicio;temas populares;crear lote;servicio de catálogo;api
solution: Experience Platform
title: Creación de un lote en la API
description: Puede crear un lote realizando una solicitud del POST al extremo /batches en la API de catálogo.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 7%

---

# Crear un lote

Para que un conjunto de datos pueda introducir datos, debe tener asociado un lote. Uso del `id` de un conjunto de datos existente, puede crear un lote realizando una solicitud de POST al `/batches` punto final en la [!DNL Catalog] API.

**Formato de API**

```HTTP
POST /batches
```

**Solicitud**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `datasetId` | El `id` del conjunto de datos al que se asociará el lote. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y un objeto de respuesta que contiene detalles del lote recién creado, incluido su `id`, una cadena generada por el sistema de solo lectura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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
