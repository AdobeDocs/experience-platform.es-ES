---
keywords: Experience Platform;inicio;temas populares;catálogo;búsqueda de objetos múltiples;api
solution: Experience Platform
title: Buscar varios objetos de catálogo
description: Si desea ver varios objetos específicos, en lugar de realizar una solicitud por cada objeto, Catalog proporciona un método abreviado sencillo para solicitar varios objetos del mismo tipo. Puede utilizar una sola solicitud de GET para devolver varios objetos específicos incluyendo una lista de ID separados por comas.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Buscar varios objetos de catálogo

Si desea ver varios objetos específicos, en lugar de realizar una solicitud por objeto, [!DNL Catalog] proporciona un acceso directo simple para solicitar varios objetos del mismo tipo. Puede utilizar una sola solicitud de GET para devolver varios objetos específicos incluyendo una lista de ID separados por comas.

>[!NOTE]
>
>Incluso cuando se solicitan datos específicos [!DNL Catalog] objetos, sigue siendo recomendable `properties` parámetro de consulta para devolver solo las propiedades que necesite.

**Formato de API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | Identificador de uno de los objetos específicos que desea recuperar. |

**Solicitud**

La siguiente solicitud incluye una lista de ID de conjuntos de datos separados por comas, así como una lista de propiedades separadas por comas que se devolverán para cada conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de los conjuntos de datos especificados, que contienen solo las propiedades solicitadas (`name`, `description`, y `files`) para cada uno.

>[!NOTE]
>
>Si un objeto devuelto no contiene una o más de las propiedades solicitadas indicadas por la variable `properties` consulta, la respuesta devuelve solo las propiedades solicitadas que sí incluye, como se muestra en ***`Sample Dataset 3`*** y ***`Sample Dataset 4`*** más abajo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
