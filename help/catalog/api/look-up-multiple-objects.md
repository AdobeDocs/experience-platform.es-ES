---
keywords: Experience Platform;inicio;temas populares;catálogo;búsqueda de varios objetos;api
solution: Experience Platform
title: Buscar varios objetos de catálogo
topic: developer guide
description: Si desea realizar una vista de varios objetos específicos, en lugar de realizar una solicitud por objeto, Catalog proporciona un método abreviado sencillo para solicitar varios objetos del mismo tipo. Puede utilizar una sola solicitud de GET para devolver varios objetos específicos incluyendo una lista de ID separada por comas.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Buscar varios objetos de catálogo

Si desea realizar una vista de varios objetos específicos, en lugar de realizar una solicitud por objeto, [!DNL Catalog] proporciona un método abreviado sencillo para solicitar varios objetos del mismo tipo. Puede utilizar una sola solicitud de GET para devolver varios objetos específicos incluyendo una lista de ID separada por comas.

>[!NOTE]
>
>Incluso cuando se solicitan objetos [!DNL Catalog] específicos, se recomienda al parámetro de consulta `properties` devolver solo las propiedades que se necesitan.

**Formato API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{OBJECT_TYPE}` | El tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Identificador de uno de los objetos específicos que desea recuperar. |

**Solicitud**

La siguiente solicitud incluye una lista separada por comas de los ID de conjuntos de datos, así como una lista separada por comas de las propiedades que se devolverán para cada conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de los conjuntos de datos especificados, que contienen solamente las propiedades solicitadas (`name`, `description` y `files`) para cada uno.

>[!NOTE]
>
>Si un objeto devuelto no contiene más de las propiedades solicitadas indicadas por la consulta `properties`, la respuesta devuelve sólo las propiedades solicitadas que incluye, como se muestra en ***`Sample Dataset 3`*** y ***`Sample Dataset 4`*** a continuación.

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
