---
keywords: Experience Platform;inicio;temas populares;actualizar entorno limitado
solution: Experience Platform
title: Actualización de un Simulador para pruebas en la API
topic: developer guide
description: Puede actualizar uno o varios campos de un simulador para pruebas realizando una solicitud de PATCH que incluya el nombre del simulador para pruebas en la ruta de la solicitud y la propiedad que desea actualizar en la carga útil de la solicitud.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# Actualización de un entorno limitado en la API

Puede actualizar uno o varios campos de un simulador para pruebas realizando una solicitud de PATCH que incluya el `name` del simulador para pruebas en la ruta de solicitud y la propiedad que se va a actualizar en la carga útil de la solicitud.

>[!NOTE]
>
>Actualmente sólo se puede actualizar la propiedad `title` de un entorno limitado.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador para pruebas que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza la propiedad `title` del simulador para pruebas denominado &quot;dev-2&quot;.

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
