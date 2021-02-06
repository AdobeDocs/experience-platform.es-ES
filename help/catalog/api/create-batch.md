---
keywords: Experience Platform;inicio;temas populares;crear lote;servicio de catálogo;api
solution: Experience Platform
title: Crear un lote en la API
topic: developer guide
description: Puede crear un lote realizando una solicitud de POST al extremo /lotes en la API del catálogo.
translation-type: tm+mt
source-git-commit: 8a213ac0ef1ac0f9c42e4b880b24157d28878bf1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---


# Crear un lote

Para que un conjunto de datos ingeste datos, debe tener un lote asociado a él. Con el valor `id` de un conjunto de datos existente, puede crear un lote realizando una solicitud de POST al extremo `/batches` en la API [!DNL Catalog].

**Formato API**

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
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `datasetId` | El `id` del conjunto de datos con el que se asociará el lote. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y un objeto de respuesta que contiene detalles del lote recién creado, incluida su `id`, una cadena de sólo lectura generada por el sistema.

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
