---
keywords: Experience Platform;home;popular topics;catalog;object lookup;api
solution: Experience Platform
title: Buscar un objeto
topic: developer guide
description: 'Si conoce el identificador único de un objeto Catalog específico, puede realizar una solicitud de GET para vista de los detalles de dicho objeto. '
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 2%

---


# Buscar un objeto

Si conoce el identificador único de un [!DNL Catalog] objeto específico, puede realizar una solicitud de GET para vista de los detalles de dicho objeto.

>[!NOTE]
>
>Al ver objetos específicos, sigue siendo recomendable [filtrar por propiedades](filter-data.md) y devolver solo las propiedades que le interesen.

**Formato API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera un conjunto de datos por su ID, devolviendo sus `name`propiedades, `description`, `state`, `tags`y `files` .

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>Las propiedades cuyos valores llevan el prefijo `@` representan objetos interrelacionados. Consulte la sección del apéndice sobre la [visualización de objetos](appendix.md#view-interrelated-objects) interrelacionados para ver los pasos para la vista de los detalles de estos objetos.
