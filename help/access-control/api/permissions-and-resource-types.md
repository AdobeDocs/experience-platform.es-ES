---
keywords: Experience Platform;inicio;temas populares;permisos de control de acceso;tipos de recursos de control de acceso;API de control de acceso
solution: Experience Platform
title: Extremo de API de referencia
topic: developer guide
description: Control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funciones de la plataforma mediante Adobe Admin Console. Puede realizar una lista de los nombres de todos los permisos y tipos de recursos mediante una solicitud de GET al extremo /acl/reference en la API de Control de acceso. Estos nombres se pueden utilizar en llamadas de API para vista de políticas eficaces para el usuario actual.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# Extremo de referencia

Puede realizar una lista de los nombres de todos los permisos y tipos de recursos mediante una solicitud de GET al extremo `/acl/reference`. Estos nombres se pueden usar en llamadas de API a [políticas eficaces de vista](./effective-policies.md) para el usuario actual.

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

Una respuesta correcta devuelve un objeto `permissions` y un objeto `resource-types`, cada uno con una lista completa de nombres para los permisos de acceso o tipos de recursos, respectivamente.

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
