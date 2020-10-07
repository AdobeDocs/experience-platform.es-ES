---
keywords: Experience Platform;home;popular topics;access control permissions;access control resource types;access control api
solution: Experience Platform
title: Nombres de lista de permisos y tipos de recursos
topic: developer guide
description: Control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funciones de la plataforma mediante Adobe Admin Console. Puede realizar una lista de los nombres de todos los permisos y tipos de recursos mediante una solicitud de GET al extremo /acl/reference. Estos nombres se pueden utilizar en llamadas de API para vista de políticas eficaces para el usuario actual.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# Nombres de lista de permisos y tipos de recursos

Puede lista los nombres de todos los permisos y tipos de recursos realizando una solicitud de GET en el `/acl/reference` extremo. Estos nombres se pueden usar en llamadas de API para [vista de políticas](./effective-policies.md) efectivas para el usuario actual.

Un permiso es una directiva que se administra a través del Adobe Admin Console y se asigna a cero o más directivas de tipo de recurso. Un tipo de recurso es una directiva que habilita las capacidades de lectura, escritura o eliminación para un tipo específico de [!DNL Platform] recurso (como conjuntos de datos o esquemas).

**Formato API**

```http
GET /acl/reference
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Respuesta**

Una respuesta correcta devuelve un `permissions` objeto y un `resource-types` objeto, cada uno con una lista completa de nombres para los permisos de acceso o tipos de recursos, respectivamente.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
