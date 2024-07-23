---
title: Uso compartido de paquetes de extensiones privadas en la API de Reactor
description: Obtenga información sobre cómo autorizar a otras empresas para que compartan paquetes de extensión privados en la API de Reactor.
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---


# Uso compartido de paquetes de extensiones privadas

>[!NOTE]
>
>Los usuarios con el permiso `develop_extensions` en la organización propietaria del paquete de extensiones pueden crear, enumerar y eliminar las autorizaciones de uso del paquete de extensiones para ese paquete de extensiones. Los usuarios de una organización autorizada que posean el permiso `manage_properties` solo pueden enumerar las autorizaciones de uso del paquete de extensión de su organización y actualizar su estado a `accepted` si desean utilizar ese paquete de extensión o a `rejected` si no desean utilizarlo.

Los propietarios de los paquetes de extensión pueden conceder permiso a otras empresas para utilizar sus versiones privadas a través de la API de Reactor. Se concede una licencia de uso para un paquete de extensión a cada empresa aprobada, y esta autorización es buena para todas las versiones privadas actuales y futuras del paquete.

Esta guía proporciona información general de alto nivel sobre cómo configurar las autorizaciones de uso de paquetes de extensiones. Para obtener instrucciones más detalladas sobre cómo administrar autorizaciones en la API de Reactor, incluido el ejemplo de JSON de la estructura de una autorización, consulte la [guía de extremo de autorización del uso del paquete de extensión](../endpoints/extension-package-usage-authorizations.md).

## Creación de una autorización {#create-authorization}

Para crear una nueva autorización, debe tener el derecho `develop_extensions`. En el siguiente ejemplo se muestra cómo se puede crear una autorización de uso de paquetes de extensiones para un paquete de extensiones utilizando la `authorized_org_id` de la compañía que desea autorizar.

**Formato de API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` del paquete de extensión para el que desea crear una autorización. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud crea una nueva autorización de paquete de extensiones para la compañía especificada.

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

{style="table-layout:auto"}

El estado inicial de la autorización se encuentra en la fase `pending_approval`. Antes de utilizar el paquete de extensión, la empresa debe aprobar la autorización. Los usuarios de la empresa pueden examinar el paquete de extensión privado mientras la autorización esté pendiente de aprobación, pero no pueden instalarlo y no pueden encontrarlo en su catálogo de extensiones.

## Aprobar una autorización {#approve-authorization}

Para aprobar una autorización, debe tener los derechos de `manage_properties`. Como empresa autorizada, deberá enviar una solicitud de PATCH a la autorización de uso del paquete de extensión, incluido el `ID` de la autorización y establecer el estado en `approved`.

**Formato de API**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | El `ID` de la autorización que desea aprobar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud de PATCH establece el `state` de una autorización en `approved`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
	          "state": "approved"
	        },
	        "id": ":extension_package_usage_authorization_id",
	        "type": "extension_package_usage_authorizations"
        }
      }
```

Una vez aprobada la autorización, como empresa autorizada, ahora puede instalar el paquete de extensión en sus propiedades.

>[!NOTE]
>
>Si se rechaza la autorización, la empresa autorizada no podrá utilizar el paquete de extensión.

## Eliminar una autorización {#delete-authorization}

Como propietario de un paquete de extensiones, puede revocar la autorización en cualquier momento eliminando la autorización de uso del paquete de extensiones. Esto evitará que la empresa autorizada vea versiones privadas del paquete de extensión en el catálogo e instalarlo en sus propiedades. Sin embargo, las versiones privadas ya instaladas seguirán funcionando según lo esperado después de la eliminación.

**Formato de API**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | El `ID` de la autorización que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud de DELETE elimina los privilegios de autorización de una compañía.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
