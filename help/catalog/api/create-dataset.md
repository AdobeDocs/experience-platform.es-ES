---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;conjunto de datos;crear un conjunto de datos;crear conjunto de datos;habilitar conjunto de datos
solution: Experience Platform
title: Crear un conjunto de datos en la API
topic-legacy: developer guide
description: Este documento explica cómo crear un objeto de conjunto de datos en la API del servicio de catálogo.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 2%

---

# Crear un conjunto de datos en la API

Para crear un conjunto de datos usando la variable [!DNL Catalog] API, debe conocer el `$id` del [!DNL Experience Data Model] esquema (XDM) en el que se basará el conjunto de datos. Una vez que tenga el ID de esquema, puede crear un conjunto de datos realizando una solicitud de POST al `/datasets` en la variable [!DNL Catalog] API.

>[!NOTE]
>
>Este documento solo explica cómo crear un objeto de conjunto de datos en [!DNL Catalog]. Para ver los pasos completos sobre cómo crear, rellenar y monitorizar un conjunto de datos, consulte lo siguiente [tutorial](../datasets/create.md).

**Formato de API**

```HTTP
POST /dataSets
```

**Solicitud**

La siguiente solicitud crea un conjunto de datos que hace referencia a un esquema definido anteriormente.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del conjunto de datos que se va a crear. |
| `schemaRef.id` | El URI `$id` para el esquema XDM en el que se basará el conjunto de datos. |
| `schemaRef.contentType` | Indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de la API XDM para obtener más información. |

>[!NOTE]
>
>Este ejemplo utiliza la variable [Apache Parquet](https://parquet.apache.org/docs/) formato de archivo para su `containerFormat` propiedad. Puede encontrar un ejemplo que utilice el formato de archivo JSON en la [guía para desarrolladores sobre ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md).

**Respuesta**

Una respuesta correcta devuelve el Estado HTTP 201 (Creado) y un objeto de respuesta que consta de una matriz que contiene el ID del conjunto de datos recién creado con el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de solo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
