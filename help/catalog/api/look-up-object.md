---
keywords: Experience Platform;inicio;temas populares;catálogo;búsqueda de objetos;api
solution: Experience Platform
title: Buscar un objeto de catálogo
topic: developer guide
description: 'Si conoce el identificador único de un objeto Catalog específico, puede realizar una solicitud de GET para vista de los detalles de dicho objeto. '
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# Buscar un objeto Catalog

Si conoce el identificador único de un objeto [!DNL Catalog] específico, puede realizar una solicitud de GET para realizar la vista de los detalles del objeto.

>[!NOTE]
>
>Al ver objetos específicos, se recomienda [filtrar por propiedades](filter-data.md) y devolver solo las propiedades que le interesen.

**Formato API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera un conjunto de datos por su ID, devolviendo sus propiedades `name`, `description`, `state`, `tags` y `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el conjunto de datos especificado con sólo el `properties` solicitado en el cuerpo.

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
>Las propiedades cuyos valores llevan el prefijo `@` representan objetos interrelacionados. Consulte la sección del apéndice sobre [visualización de objetos interrelacionados](appendix.md#view-interrelated-objects) para ver los pasos sobre cómo realizar la vista de los detalles de estos objetos.
