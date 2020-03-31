---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Actualización de un simulador para pruebas
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Actualización de un simulador para pruebas

Puede actualizar uno o varios campos de un simulador para pruebas realizando una solicitud PATCH que incluya el simulador para pruebas `name` en la ruta de solicitud y la propiedad que se va a actualizar en la carga útil de la solicitud.

>[!NOTE] Actualmente solo se puede actualizar la propiedad `title` de un simulador de pruebas.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` propiedad del simulador para pruebas que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza la `title` propiedad del simulador para pruebas denominado &quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Aceptar) con los detalles del entorno limitado recién actualizado.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
