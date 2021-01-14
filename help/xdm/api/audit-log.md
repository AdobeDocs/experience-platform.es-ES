---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;audit;audit log;changelog;change log;rpc;
solution: Experience Platform
title: Guía de extremo del registro de auditoría
description: El extremo /auditlog de la API del Registro de Esquema permite recuperar una lista cronológica de los cambios realizados en un recurso XDM existente.
topic: developer guide
translation-type: tm+mt
source-git-commit: eb5e34dc3b48a6fe0757635cad1df08caa68b019
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Extremo del registro de auditoría

Para cada recurso del Modelo de datos de experiencia (XDM), el [!DNL Schema Registry] mantiene un registro de todos los cambios que se han producido entre distintas actualizaciones. El extremo `/auditlog` de la API [!DNL Schema Registry] permite recuperar un registro de auditoría para cualquier clase, mezcla, tipo de datos o esquema especificado por el ID.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas exitosas a cualquier API de Experience Platform.

El extremo `/auditlog` forma parte de las llamadas a procedimientos remotos (RPC) que admite [!DNL Schema Registry]. A diferencia de otros extremos de la API [!DNL Schema Registry], los extremos de RPC no requieren encabezados adicionales como `Accept` o `Content-Type` y no utilizan un `CONTAINER_ID`. En su lugar, deben utilizar la Área de nombres `/rpc`, como se muestra en la llamada de API que se muestra a continuación.

## Recuperar un registro de auditoría para un recurso

Puede recuperar un registro de auditoría para cualquier clase, mezcla, tipo de datos o esquema dentro de la biblioteca de Esquemas especificando el ID del recurso en la ruta de una solicitud de GET al extremo `/auditlog`.

**Formato API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_ID}` | El `meta:altId` o `$id` con codificación URL del recurso cuyo registro de auditoría desea recuperar. |

**Solicitud**

La siguiente solicitud recupera el registro de auditoría para una mezcla `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista cronológica de los cambios realizados en el recurso, desde los más recientes hasta los menos recientes.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Propiedad | Descripción |
| --- | --- |
| `auditTrails` | Matriz de objetos, con cada objeto que representa un cambio realizado en el recurso especificado o en uno de sus recursos dependientes. |
| `id` | El `$id` del recurso que se cambió. Normalmente, este valor representa el recurso especificado en la ruta de solicitud, pero puede representar un recurso dependiente si ese es el origen del cambio. |
| `action` | El tipo de cambio que se realizó. |
| `path` | Una cadena [puntero JSON](../../landing/api-fundamentals.md#json-pointer) que indica la ruta al campo específico que se cambió o agregó. |
| `value` | Valor asignado al campo nuevo o actualizado. |