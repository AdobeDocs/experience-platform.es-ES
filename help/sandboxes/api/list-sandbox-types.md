---
keywords: Experience Platform;inicio;temas populares;entornos limitados de lista
solution: Experience Platform
title: Lista de tipos de Simulador para pruebas admitidos en la API
topic: developer guide
description: Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al extremo /sandboxTypes .
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 2%

---


# Lista de tipos de entornos limitados admitidos en la API

Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al extremo `/sandboxTypes` .

**Formato de API**

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

Una respuesta correcta devuelve una lista de tipos de entornos limitados compatibles con su organización.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
