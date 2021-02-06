---
keywords: Experience Platform;inicio;temas populares;eliminar entorno limitado
solution: Experience Platform
title: Eliminación de un Simulador para pruebas en la API
topic: developer guide
description: Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el nombre del simulador para pruebas en la ruta de solicitud.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 3%

---


# Eliminación de un entorno limitado en la API

Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el `name` simulador para pruebas en la ruta de solicitud.

>[!NOTE]
>
>Al realizar esta llamada de API, se actualiza la propiedad `status` del simulador para pruebas a &quot;delete&quot; y se desactiva. Las solicitudes de GET aún pueden recuperar los detalles del entorno limitado después de eliminarlo.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | El `name` del entorno limitado que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina un simulador para pruebas llamado &quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actualizados del entorno limitado, mostrando que su `state` se &quot;elimina&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
