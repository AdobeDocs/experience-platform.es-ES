---
keywords: Experience Platform;inicio;temas populares;entornos limitados de lista
solution: Experience Platform
title: Tipos de Simulador para pruebas compatibles con la lista en la API
topic: developer guide
description: Puede recuperar una lista de tipos de simulación de pruebas admitidos para su organización haciendo una solicitud de GET al extremo /sandboxTypes.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 2%

---


# Tipos de entorno limitado admitidos en la lista en la API

Puede recuperar una lista de tipos de simulación de pruebas admitidos para su organización haciendo una solicitud de GET al extremo `/sandboxTypes`.

**Formato API**

```http
GET /sandboxTypes
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de tipos de simulación de pruebas admitidos por su organización.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
