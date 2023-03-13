---
keywords: Experience Platform;inicio;temas populares;catálogo;búsqueda de objetos;api
solution: Experience Platform
title: Búsqueda de un objeto de catálogo
description: Si conoce el identificador único de un objeto Catalog específico, puede realizar una solicitud de GET para ver los detalles de ese objeto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Búsqueda de un objeto Catalog

Si conoce el identificador único de un [!DNL Catalog] objeto, puede realizar una solicitud de GET para ver los detalles de ese objeto.

>[!NOTE]
>
>Cuando se visualizan objetos específicos, sigue siendo recomendable [filtrar por propiedades](filter-data.md) y devuelva únicamente las propiedades que le interesen.

**Formato de API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | El identificador del objeto específico que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera un conjunto de datos por su ID, devolviendo su `name`, `description`, `state`, `tags`, y `files` propiedades.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el conjunto de datos especificado con solo el solicitado `properties` en el cuerpo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>Propiedades cuyos valores tienen el prefijo `@` representar objetos interrelacionados. Consulte la sección del apéndice sobre [visualización de objetos interrelacionados](appendix.md#view-interrelated-objects) para ver los pasos de cómo ver los detalles de estos objetos.
