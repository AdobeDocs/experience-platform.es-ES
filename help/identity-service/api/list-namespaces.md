---
keywords: Experience Platform;inicio;temas populares;lista de área de nombres;área de nombres de la lista
solution: Experience Platform
title: Enumerar espacios de nombres de identidad disponibles
topic-legacy: API guide
description: Enumere todos los espacios de nombres disponibles.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 5%

---

# Enumerar áreas de nombres de identidad disponibles

**Formato de API**

```http
GET /idnamespace/identities
```

**Solicitud**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye una matriz de objetos, cada uno de los cuales representa un espacio de nombres disponible. Los espacios de nombres con un valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL false]&quot; son espacios de nombres estándar, mientras que los que tienen un valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL true]&quot; son espacios de nombres creados por su organización.

>[!NOTE]
>
>Esta respuesta se ha truncado para el espacio.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Pasos siguientes

Continúe con el siguiente tutorial para [crear un espacio de nombres personalizado](./create-custom-namespace.md)
