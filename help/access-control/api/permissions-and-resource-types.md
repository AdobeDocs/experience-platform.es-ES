---
keywords: Experience Platform;inicio;temas populares;permisos de control de acceso;tipos de recursos de control de acceso;api de control de acceso
solution: Experience Platform
title: Punto final de API de referencia
description: El extremo de referencia de la API de control de acceso le permite ver los nombres de los permisos y tipos de recursos disponibles, que luego se pueden usar para ver las directivas de control de acceso efectivas para el usuario actual.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# Extremo de referencia

>[!NOTE]
>
>Si se pasa un token de usuario, el usuario del token debe tener un rol de &quot;administrador de organización&quot; para la organización solicitada.

Puede enumerar los nombres de todos los permisos y tipos de recursos realizando una petición GET al extremo `/acl/reference`. Estos nombres se pueden usar en llamadas API a [ver directivas de control de acceso efectivas](./effective-policies.md) para el usuario actual.

Un permiso es una directiva que se administra mediante Adobe Admin Console y que se asigna a cero o más directivas de tipo de recurso. Un tipo de recurso es una directiva que habilita las capacidades de lectura, escritura o eliminación para un tipo específico de recurso [!DNL Experience Platform] (como conjuntos de datos o esquemas).

**Formato de API**

```http
GET /acl/reference
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve un objeto `permissions` y un objeto `resource-types`, cada uno de los cuales contiene una lista completa de nombres de permisos de acceso o tipos de recursos, respectivamente.

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
