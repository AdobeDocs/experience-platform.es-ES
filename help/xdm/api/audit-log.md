---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;auditoría;registro de auditoría;registro de cambios;registro de cambios;rpc;
solution: Experience Platform
title: Punto final de API de registro de auditoría
description: El extremo /auditlog en la API del Registro de esquemas permite recuperar una lista cronológica de los cambios realizados en un recurso XDM existente.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Extremo del registro de auditoría

Para cada recurso del Modelo de datos de experiencia (XDM), la variable [!DNL Schema Registry] mantiene un registro de todos los cambios que se han producido entre diferentes actualizaciones. La variable `/auditlog` en la variable [!DNL Schema Registry] La API permite recuperar un registro de auditoría para cualquier clase, grupo de campos de esquema, tipo de datos o esquema especificado por ID.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API de ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

La variable `/auditlog` el extremo es parte de las llamadas a procedimientos remotos (RPC) que son compatibles con la variable [!DNL Schema Registry]. A diferencia de otros extremos en la variable [!DNL Schema Registry] Los extremos de API y RPC no requieren encabezados adicionales como `Accept` o `Content-Type`y no use un `CONTAINER_ID`. En su lugar, deben usar la variable `/rpc` como se muestra en la llamada de API a continuación.

## Recuperar un registro de auditoría para un recurso

Puede recuperar un registro de auditoría para cualquier clase, grupo de campos, tipo de datos o esquema de la Biblioteca de esquemas especificando el ID del recurso en la ruta de una solicitud de GET a la variable `/auditlog` punto final.

**Formato de API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_ID}` | La variable `meta:altId` o con codificación de URL `$id` del recurso cuyo registro de auditoría desea recuperar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud recupera el registro de auditoría de un esquema.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista cronológica de los cambios realizados en el recurso, desde los más recientes hasta los menos recientes.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Propiedad | Descripción |
| --- | --- |
| `updates` | Matriz de objetos, con cada objeto que representa un cambio realizado en el recurso especificado o en uno de sus recursos dependientes. |
| `id` | La variable `$id` del recurso que se cambió. Este valor representa generalmente el recurso especificado en la ruta de solicitud, pero puede representar un recurso dependiente si ese es el origen del cambio. |
| `xdmType` | Tipo de recurso que se cambió. |
| `action` | Tipo de cambio que se ha realizado. |
| `path` | A [Puntero JSON](../../landing/api-fundamentals.md#json-pointer) cadena que indica la ruta al campo específico que se cambió o agregó. |
| `value` | El valor que se asignó al campo nuevo o actualizado. |

{style=&quot;table-layout:auto&quot;}
