---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;auditoría;registro de auditoría;registro de cambios;registro de cambios;rpc;
solution: Experience Platform
title: Punto final de API de registro de auditoría
description: El extremo /auditlog en la API del Registro de esquemas permite recuperar una lista cronológica de los cambios realizados en un recurso XDM existente.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 6%

---

# Extremo del registro de auditoría

Para cada recurso del Modelo de datos de experiencia (XDM), el [!DNL Schema Registry] mantiene un registro de todos los cambios que se han producido entre diferentes actualizaciones. El extremo `/auditlog` de la API [!DNL Schema Registry] permite recuperar un registro de auditoría para cualquier clase, grupo de campos de esquema, tipo de datos o esquema especificado por ID.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API de ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas correctamente a cualquier API de Experience Platform.

El extremo `/auditlog` forma parte de las llamadas a procedimientos remotos (RPC) compatibles con [!DNL Schema Registry]. A diferencia de otros extremos de la API [!DNL Schema Registry], los extremos RPC no requieren encabezados adicionales como `Accept` o `Content-Type` y no utilizan `CONTAINER_ID`. En su lugar, deben utilizar el espacio de nombres `/rpc` , como se muestra en la llamada de API que aparece a continuación.

## Recuperar un registro de auditoría para un recurso

Puede recuperar un registro de auditoría para cualquier clase, grupo de campos, tipo de datos o esquema de la Biblioteca de esquemas especificando el ID del recurso en la ruta de una solicitud de GET al extremo `/auditlog` .

**Formato de API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_ID}` | El `meta:altId` o la `$id` con codificación de URL del recurso cuyo registro de auditoría desea recuperar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud recupera el registro de auditoría de un grupo de campos `Restaurant`.

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
| `id` | El `$id` del recurso que se cambió. Este valor suele representar el recurso especificado en la ruta de solicitud, pero puede representar un recurso dependiente si ese es el origen del cambio. |
| `action` | Tipo de cambio que se ha realizado. |
| `path` | Una cadena [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) que indica la ruta al campo específico que se cambió o agregó. |
| `value` | El valor que se asignó al campo nuevo o actualizado. |

{style=&quot;table-layout:auto&quot;}
