---
title: Extremo de perfiles
description: Aprenda a realizar llamadas al extremo /profiles en la API de Reactor.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 75%

---

# Extremo del perfil

En la API de Reactor, un perfil representa a un usuario de Adobe Experience Platform. La API de Reactor no mantiene su propia base de datos de usuarios y permisos, sino que se basa en los ID de Adobe administrados por el [Sistema de administración de identidades (IMS) de Adobe](https://helpx.adobe.com/es/enterprise/using/identity.html).

Un perfil contiene toda la información sobre el usuario que ha iniciado sesión, incluidas todas las organizaciones a las que pertenece, los perfiles de producto a los que pertenece dentro de cada organización y los derechos que tiene de cada perfil de producto.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperación del perfil actual {#lookup}

Puede recuperar los detalles del perfil registrado actualmente realizando una petición GET al extremo `/profile`.

**Formato de API**

```http
GET /profile
```

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del perfil.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{ORG_1}": {
          "name": "Example organization A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{ORG_2}": {
          "name": "Example organization B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```
