---
title: Punto final de autorizaciones de uso del paquete de extensiones
description: Aprenda a realizar llamadas al extremo de autorizaciones /extension_package_usage en la API de Reactor.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 16%

---

# Extremo de autorizaciones de uso del paquete de extensiones

Un paquete de extensiones representa una [extensión](./extensions.md) creada por un desarrollador de extensiones. Las funcionalidades adicionales que se pueden poner a disposición de los usuarios de etiquetas se definen mediante un paquete de extensiones. Estas funcionalidades pueden incluir módulos principales y módulos compartidos, aunque se proporcionan con mayor frecuencia como [componentes de regla](./rule-components.md) (eventos, condiciones y acciones) y [elementos de datos](./data-elements.md).

La [compañía](./companies.md) del desarrollador es propietaria de un paquete de extensiones. Los propietarios de los paquetes de extensión pueden autorizar a otras empresas a utilizar sus versiones privadas de los paquetes. Cada empresa autorizada recibe una autorización de uso para un solo paquete de extensión, que es válida para todas las versiones privadas futuras y actuales del paquete.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperación de autorizaciones de uso de paquetes de extensiones para un paquete de extensiones {#list}

Para recuperar una lista de autorizaciones de uso para un paquete de extensión, realice una solicitud de GET al siguiente extremo.

**Formato de API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `ID` de la propiedad cuya autorización de uso del paquete de extensión desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de paquetes de extensiones.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Creación de una autorización de uso del paquete de extensiones {#create}

Cree una autorización de uso del paquete de extensión para cada [paquete de extensión](./extension-packages.md) y `{ORG_ID}` de la organización que desee autorizar. Para crear una nueva autorización de uso del paquete de extensiones, realice una solicitud de POST al punto de conexión siguiente.

**Formato de API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` del paquete de extensión para el que desea crear una autorización&quot;. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Propiedad | Descripción |
| --- | --- |
| `attributes.authorized_org_id` | El `ID` de la organización que desea autorizar. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la autorización de uso del paquete de extensiones recién creada.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>En la respuesta de ejemplo anterior, la autorización se encuentra actualmente en la fase `pending_approval`. Antes de utilizar el paquete de extensión, la organización debe aprobar la autorización. Los usuarios de la organización pueden examinar el paquete de extensión privado mientras la autorización esté pendiente de aprobación, pero no pueden instalarlo y no pueden encontrarlo en su catálogo de extensiones.

## Recuperación de una lista de autorizaciones de uso de paquetes de extensiones {#list-authorizations}

Puede recuperar una lista de autorizaciones de uso de paquetes de extensiones realizando una solicitud de GET.

**Formato de API**

```http
GET /extension_package_usage_authorizations
```

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de paquetes de extensiones.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Eliminación de una autorización de uso del paquete de extensiones {#delete}

Para eliminar una autorización de uso de paquete de extensión, incluya su `ID` en la ruta de una solicitud de DELETE. Esto evita que la organización autorizada vea las versiones privadas del paquete de extensión en el catálogo e instale dicho paquete en sus propiedades.

>[!NOTE]
>
>Todas las versiones privadas instaladas anteriormente seguirán funcionando según lo esperado.

**Formato de API**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parámetro | Descripción |
| --- | --- |
| `ID` | `ID` de la autorización de uso del paquete de extensiones que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) sin cuerpo de respuesta. Esto indica que la extensión se ha eliminado.

## Actualización de una autorización de uso del paquete de extensiones {#update}

Para aprobar o rechazar una autorización de uso de paquetes de extensiones, incluya su `ID` en la ruta de una solicitud de PATCH.

>[!NOTE]
>
>Para aprobar o rechazar una autorización de uso de paquetes de extensiones para su empresa, debe tener `manage_properties` derechos.

**Formato de API**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parámetro | Descripción |
| --- | --- |
| `ID` | `ID` de la autorización de uso del paquete de extensiones que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Propiedad | Descripción |
| --- | --- |
| `attributes` | Los atributos que desea revisar. Para las autorizaciones de uso de paquetes de extensiones puede revisar sus `state`. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la autorización de uso del paquete de extensiones revisado.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>Una vez aprobada la autorización, su organización puede instalar el paquete de extensión en sus propiedades.

## Recuperación de datos para el paquete de extensión para una autorización de uso del paquete de extensión {#retrieve-data}

Puede recuperar datos para el paquete de extensión para una autorización de uso del paquete de extensión realizando una solicitud de GET.

**Formato de API**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parámetro | Descripción |
| --- | --- |
| `ID` | `ID` de la autorización de uso del paquete de extensiones que desea recuperar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve datos para el paquete de extensiones para una autorización de paquete de extensiones.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
