---
keywords: Experience Platform;inicio;temas populares;lista de Área de nombres;Área de nombres de lista
solution: Experience Platform
title: Áreas de nombres de identidad disponibles de lista
topic: API guide
description: Lista de todas las Áreas de nombres disponibles.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---


# Áreas de nombres de identidad disponibles de lista

**Formato API**

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

La respuesta incluye una matriz de objetos, cada uno de los cuales representa una Área de nombres disponible. Las Áreas de nombres con un valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL false]&quot; son Áreas de nombres estándar, mientras que aquellas con un valor &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL true]&quot; son Áreas de nombres que su organización ha creado.

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

Vaya al siguiente tutorial para [crear una Área de nombres personalizada](./create-custom-namespace.md)