---
title: Punto final de perfiles
description: Aprenda a realizar llamadas al extremo /profiles en la API de Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 5%

---

# Punto de conexión del perfil

En la API de Reactor, un perfil representa a un usuario de Adobe Experience Platform. La API de Reactor no mantiene su propia base de datos de usuarios y permisos, sino que se basa en los ID de Adobe administrados por el [sistema de administración de identidades (IMS)](https://helpx.adobe.com/es/enterprise/using/identity.html) del Adobe.

Un perfil contiene toda la información sobre el usuario que ha iniciado sesión, incluidas todas las organizaciones de IMS a las que pertenece, los perfiles de producto a los que pertenece dentro de cada organización y los derechos que tiene de cada perfil de producto.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [API del reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperar el perfil actual {#lookup}

Puede recuperar los detalles del perfil registrado actualmente realizando una solicitud de GET al extremo `/profile` .

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
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
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
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

