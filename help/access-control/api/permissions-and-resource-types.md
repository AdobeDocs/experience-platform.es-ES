---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nombres de Lista de permisos y tipos de recursos
topic: developer guide
translation-type: tm+mt
source-git-commit: 7b354a96d70332cf7a7e9eff322cd3d6ee0fc96a

---


# Nombres de Lista de permisos y tipos de recursos

Puede lista los nombres de todos los permisos y tipos de recursos realizando una solicitud GET al extremo `/acl/reference` . Estos nombres se pueden usar en llamadas de API para [vista de políticas](./effective-policies.md) efectivas para el usuario actual.

Un **permiso** es una directiva que se administra a través de Adobe Admin Console y se asigna a cero o más directivas de tipo de recurso. Un tipo **de** recurso es una directiva que habilita las capacidades de lectura, escritura o eliminación para un tipo específico de recurso de la Plataforma (como conjuntos de datos o esquemas).

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
