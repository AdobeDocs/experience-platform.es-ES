---
keywords: Experience Platform;inicio;temas populares;permisos de control de acceso;tipos de recursos de control de acceso;api de control de acceso
solution: Experience Platform
title: Punto final de API de referencia
topic-legacy: developer guide
description: El control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funcionalidades de Platform mediante Adobe Admin Console. Puede enumerar los nombres de todos los permisos y tipos de recursos realizando una solicitud de GET al extremo /acl/reference en la API de control de acceso. Estos nombres se pueden utilizar en llamadas a API para ver las políticas efectivas para el usuario actual.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 2%

---

# Punto de referencia

Puede enumerar los nombres de todos los permisos y tipos de recursos realizando una solicitud de GET al `/acl/reference` punto final. Estos nombres se pueden utilizar en llamadas de API a [ver políticas eficaces](./effective-policies.md) para el usuario actual.

Un permiso es una directiva que se administra a través de Adobe Admin Console y que se asigna a cero o más directivas de tipo de recurso. Un tipo de recurso es una directiva que habilita las capacidades de lectura, escritura o eliminación para un tipo específico [!DNL Platform] recurso (como conjuntos de datos o esquemas).

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

Una respuesta correcta devuelve un valor `permissions` y `resource-types` , cada uno con una lista completa de nombres para permisos de acceso o tipos de recursos, respectivamente.

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
