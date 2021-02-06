---
keywords: Experience Platform;inicio;temas populares;filtrar;filtrar;filtrar datos;Filtrar datos
solution: Experience Platform
title: Objetos del catálogo de listas
topic: developer guide
description: Puede recuperar una lista de todos los objetos disponibles de un tipo específico a través de una sola llamada de API, siendo recomendable incluir filtros que limiten el tamaño de la respuesta.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---


# Objetos del catálogo de listas

Puede recuperar una lista de todos los objetos disponibles de un tipo específico a través de una sola llamada de API, siendo recomendable incluir filtros que limiten el tamaño de la respuesta.

**Formato API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de objeto [!DNL Catalog] que se va a enumerar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Parámetro de consulta utilizado para filtrar los resultados devueltos en la respuesta. Los parámetros múltiples se separan con ampersands (`&`). Consulte la guía sobre [filtrado de datos del catálogo](filter-data.md) para obtener más información. |

**Solicitud**

La solicitud de ejemplo siguiente recupera una lista de conjuntos de datos, con un filtro `limit` que reduce la respuesta a cinco resultados y un filtro `properties` que limita las propiedades mostradas para cada conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de [!DNL Catalog] objetos en forma de pares clave-valor, filtrados por los parámetros de consulta proporcionados en la solicitud. Para cada par clave-valor, la clave representa un identificador único para el objeto [!DNL Catalog] en cuestión, que se puede utilizar en otra llamada a [vista de ese objeto específico](look-up-object.md) para obtener más detalles.

>[!NOTE]
>
>Si un objeto devuelto no contiene una o más de las propiedades solicitadas indicadas por la consulta `properties`, la respuesta devuelve sólo las propiedades solicitadas que incluye, como se muestra en ***`Sample Dataset 3`*** y ***`Sample Dataset 4`*** a continuación.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
