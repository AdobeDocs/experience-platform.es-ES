---
keywords: Experience Platform;home;popular topics;delete sandbox
solution: Experience Platform
title: Eliminar un entorno limitado
topic: developer guide
description: Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el nombre del simulador para pruebas en la ruta de solicitud.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 3%

---


# Eliminar un entorno limitado

Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el simulador para pruebas `name` en la ruta de solicitud.

>[!NOTE]
>
>Al realizar esta llamada de API, se actualiza la propiedad del `status` simulador para pruebas a &quot;eliminarse&quot; y se desactiva. Las solicitudes de GET aún pueden recuperar los detalles del entorno limitado después de eliminarlo.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | El `name` del simulador para pruebas que desea eliminar. |

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

Una respuesta correcta devuelve los detalles actualizados del simulador para pruebas, mostrando que `state` se &quot;elimina&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
