---
keywords: Experience Platform;inicio;temas populares;eliminar un objeto;servicio de catálogo;api
solution: Experience Platform
title: Eliminar un objeto en la API
description: Puede eliminar un objeto Catalog proporcionando su ID en la ruta de una petición del DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 2%

---

# Eliminación de un objeto en la API

Puede eliminar un objeto [!DNL Catalog] si proporciona su ID en la ruta de una solicitud de DELETE.

>[!WARNING]
>
>Tenga especial cuidado al eliminar objetos, ya que esto no se puede deshacer y puede producir cambios importantes en cualquier otra parte de [!DNL Experience Platform].

**Formato de API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>El extremo `DELETE /batches/{ID}` se ha desaprobado. Para eliminar un lote, debe usar la [API de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a eliminar. Los objetos válidos son: <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | El identificador del objeto específico que desea actualizar. |

**Solicitud**

La siguiente solicitud elimina un conjunto de datos cuyo ID se especifica en la ruta de solicitud.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos eliminado. Este ID debe coincidir con el enviado en la solicitud del DELETE. Al realizar una solicitud de GET en el objeto eliminado, se devuelve el estado HTTP 404 (no encontrado), que confirma que el conjunto de datos se ha eliminado correctamente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Si ningún objeto [!DNL Catalog] coincide con el identificador proporcionado en su solicitud, es posible que reciba un código de estado HTTP 200, pero la matriz de respuesta estará vacía.
