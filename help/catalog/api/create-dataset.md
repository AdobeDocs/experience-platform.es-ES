---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear un conjunto de datos
topic: developer guide
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Crear un conjunto de datos

Para crear un conjunto de datos mediante la API de catálogo, debe conocer el valor del `$id` esquema del modelo de datos de experiencia (XDM) en el que se basará el conjunto de datos. Una vez que tenga el ID de esquema, puede crear un conjunto de datos realizando una solicitud POST al extremo en la API de catálogo `/datasets` .

>[!NOTE] Este documento solo cubre cómo crear un objeto de conjunto de datos en el catálogo. Para ver los pasos completos sobre cómo crear, rellenar y monitorear un conjunto de datos, consulte el siguiente [tutorial](../datasets/create.md).

**Formato API**

```HTTP
POST /dataSets
```

**Solicitud**

La siguiente solicitud crea un conjunto de datos que hace referencia a un esquema definido previamente.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del conjunto de datos que se va a crear. |
| `schemaRef.id` | El valor URI `$id` del esquema XDM en el que se basará el conjunto de datos. |

>[!NOTE] En este ejemplo se utiliza el formato de archivo de [parqué](https://parquet.apache.org/documentation/latest/) para su `containerFormat` propiedad. Encontrará un ejemplo que utiliza el formato de archivo JSON en la guía para desarrolladores de [ingestión por lotes](../../ingestion/batch-ingestion/api-overview.md).

**Respuesta**

Una respuesta correcta devuelve Estado HTTP 201 (Creado) y un objeto de respuesta que consta de una matriz que contiene el ID del conjunto de datos recién creado en el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de sólo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas de API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
