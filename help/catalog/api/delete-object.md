---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eliminar un objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---


# Eliminar un objeto

Puede eliminar un [!DNL Catalog] objeto proporcionando su ID en la ruta de una solicitud de DELETE.

>[!WARNING]
>
>Tenga especial cuidado al eliminar objetos, ya que esto no se puede deshacer y puede producir cambios de ruptura en otras partes de [!DNL Experience Platform].

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>El extremo se ha desaprobado `DELETE /batches/{ID}` . Para eliminar un lote, debe utilizar la API [de ingestión de](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)lotes.

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a eliminar. Los objetos válidos son: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud elimina un conjunto de datos cuyo ID se especifica en la ruta de la solicitud.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Aceptar) y una matriz que contiene el ID del conjunto de datos eliminado. Este ID debe coincidir con el enviado en la solicitud de DELETE. Al realizar una solicitud GET en el objeto eliminado, se devuelve el estado HTTP 404 (no encontrado), lo que confirma que el conjunto de datos se ha eliminado correctamente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Si no hay ningún [!DNL Catalog] objeto que coincida con el ID proporcionado en la solicitud, puede recibir un código de estado HTTP 200, pero la matriz de respuesta estará vacía.
