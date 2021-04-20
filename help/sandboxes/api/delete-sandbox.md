---
keywords: Experience Platform;inicio;temas populares;eliminar entorno limitado
solution: Experience Platform
title: Eliminación de un Simulador para pruebas en la API
topic: developer guide
description: Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el nombre del simulador para pruebas en la ruta de solicitud.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---


# Eliminación de un simulador para pruebas en la API

Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el `name` del simulador para pruebas en la ruta de solicitud.

>[!NOTE]
>
>Al realizar esta llamada de API, se actualiza la propiedad `status` del entorno limitado a &quot;eliminado&quot; y se desactiva. Las solicitudes de GET aún pueden recuperar los detalles del entorno limitado una vez que se han eliminado.

**Formato de API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | El `name` del simulador de pruebas que desea eliminar. |

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

Una respuesta correcta devuelve los detalles actualizados del entorno limitado, mostrando que su `state` está &quot;eliminado&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
