---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tipos de entorno limitado compatibles con la Lista
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 4%

---


# Tipos de entorno limitado compatibles con la Lista

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
