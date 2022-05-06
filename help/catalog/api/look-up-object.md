---
keywords: Experience Platform;inicio;temas populares;catálogo;búsqueda de objetos;api
solution: Experience Platform
title: Buscar un objeto de catálogo
topic-legacy: developer guide
description: Si conoce el identificador único de un objeto Catalog específico, puede realizar una solicitud de GET para ver los detalles de ese objeto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Buscar un objeto Catálogo

Si conoce el identificador único de un [!DNL Catalog] , puede realizar una solicitud de GET para ver los detalles de ese objeto.

>[!NOTE]
>
>Cuando se ven objetos específicos, sigue siendo recomendable realizar [filtrar por propiedades](filter-data.md) y devuelven solo las propiedades que le interesen.

**Formato de API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera un conjunto de datos por su ID y devuelve su valor `name`, `description`, `state`, `tags`y `files` propiedades.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el conjunto de datos especificado con solo el `properties` en el cuerpo.

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
>Propiedades cuyos valores tienen el prefijo `@` representan objetos interrelacionados. Consulte la sección del apéndice sobre [visualización de objetos interrelacionados](appendix.md#view-interrelated-objects) para ver los detalles de estos objetos.
