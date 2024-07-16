---
keywords: Experience Platform;inicio;temas populares;catálogo;búsqueda de objetos;api
solution: Experience Platform
title: Búsqueda de un objeto de catálogo
description: Si conoce el identificador único de un objeto Catalog específico, puede realizar una solicitud de GET para ver los detalles de ese objeto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Búsqueda de un objeto Catalog

Si conoce el identificador único de un objeto [!DNL Catalog] específico, puede realizar una solicitud de GET para ver los detalles de ese objeto.

>[!NOTE]
>
>Al ver objetos específicos, se recomienda [filtrar por propiedades](filter-data.md) y devolver solamente las propiedades que le interesen.

**Formato de API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | El identificador del objeto específico que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera un conjunto de datos por su ID, devolviendo sus propiedades `name`, `description`, `tags` y `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el conjunto de datos especificado con solo el `properties` solicitado en el cuerpo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Las propiedades cuyos valores tienen el prefijo `@` representan objetos interrelacionados. Consulte la sección del apéndice sobre [visualización de objetos interrelacionados](appendix.md#view-interrelated-objects) para ver los pasos sobre cómo ver los detalles de estos objetos.
