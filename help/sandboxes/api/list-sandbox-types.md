---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Tipos de entorno limitado compatibles con la lista
topic: developer guide
description: Puede recuperar una lista de tipos de simulación de pruebas admitidos para su organización haciendo una solicitud de GET al extremo /sandboxTypes.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 2%

---


# Tipos de entorno limitado compatibles con la lista

Puede recuperar una lista de tipos de simulación de pruebas admitidos para su organización realizando una solicitud de GET al `/sandboxTypes` extremo.

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
