---
keywords: Experience Platform;inicio;temas populares;actualizar entorno limitado
solution: Experience Platform
title: Actualizar un Simulador para pruebas en la API
topic-legacy: developer guide
description: Puede actualizar uno o varios campos de un simulador de pruebas realizando una solicitud de PATCH que incluya el nombre del simulador de pruebas en la ruta de solicitud y la propiedad que se va a actualizar en la carga útil de la solicitud.
exl-id: a8ef4305-5e0c-4d8f-8663-1933c957f122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# Actualizar un simulador para pruebas en la API

Puede actualizar uno o más campos de un simulador de pruebas realizando una solicitud de PATCH que incluya el `name` del simulador de pruebas en la ruta de solicitud y la propiedad que se va a actualizar en la carga útil de la solicitud.

>[!NOTE]
>
>Actualmente solo se puede actualizar la propiedad `title` de un entorno limitado.

**Formato de API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador de pruebas que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza la propiedad `title` del simulador para pruebas llamado &quot;dev-2&quot;.

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

Una respuesta correcta devuelve el estado HTTP 200 (OK) con los detalles del entorno limitado recién actualizado.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
