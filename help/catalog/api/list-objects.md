---
keywords: Experience Platform;inicio;temas populares;filtrar;filtrar;filtrar datos;filtrar datos
solution: Experience Platform
title: Enumerar objetos de catálogo
description: Puede recuperar una lista de todos los objetos disponibles de un tipo específico mediante una sola llamada de API, siendo la práctica recomendada incluir filtros que limiten el tamaño de la respuesta.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 2%

---

# Enumerar objetos de catálogo

Puede recuperar una lista de todos los objetos disponibles de un tipo específico mediante una sola llamada de API, siendo la práctica recomendada incluir filtros que limiten el tamaño de la respuesta.

**Formato de API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se enumerará. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Un parámetro de consulta utilizado para filtrar los resultados devueltos en la respuesta. Los parámetros múltiples se separan con el símbolo et (`&`). Consulte la guía de [filtrado de datos de catálogo](filter-data.md) para obtener más información. |

**Solicitud**

La solicitud de ejemplo siguiente recupera una lista de conjuntos de datos, con un `limit` filtro que reduce la respuesta a cinco resultados y una `properties` filtro que limita las propiedades mostradas para cada conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de [!DNL Catalog] objetos en forma de pares clave-valor, filtrados por los parámetros de consulta proporcionados en la solicitud. Para cada par clave-valor, la clave representa un identificador único para la variable [!DNL Catalog] objeto en cuestión, que se puede utilizar en otra llamada a [ver ese objeto específico](look-up-object.md) para obtener más información.

>[!NOTE]
>
>Si un objeto devuelto no contiene una o varias de las propiedades solicitadas indicadas por la variable `properties` consulta, la respuesta devuelve solo las propiedades solicitadas que sí incluye, como se muestra en ***`Sample Dataset 3`*** y ***`Sample Dataset 4`*** más abajo.

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
