---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Buscar un recurso
topic: developer guide
translation-type: tm+mt
source-git-commit: 71c73a3899ccdd1c024a811b36c411915a3b14be

---


# Buscar un recurso

Puede buscar recursos específicos realizando una solicitud GET que incluya el `$id` (URI con codificación URL) del recurso en la ruta de solicitud.

**Formato API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor donde se ubican los recursos (&quot;global&quot; o &quot;inquilino&quot;). |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a recuperar de la biblioteca de Esquemas. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |
| `{RESOURCE_ID}` | El `$id` URI con codificación URL o `meta:altId` del recurso. |

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Las solicitudes de búsqueda de recursos requieren que `version` se incluyan en el encabezado Accept. Los siguientes encabezados Accept están disponibles para búsquedas:

| Aceptar | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Sin procesar con `$ref` y `allOf`, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` y `allOf` resuelto, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Sin formato `$ref` y `allOf`, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` y `allOf` resuelto, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` y `allOf` resueltos, se incluyen los descriptores. |

>[!NOTE] Si sólo se proporciona la versión `major` (1, 2, 3, etc.), el Registro devolverá automáticamente la última `minor` versión (.1, .2, .3, etc.).

**Respuesta**

Una respuesta correcta devuelve los detalles del recurso. Los campos devueltos dependen del encabezado Accept enviado en la solicitud. Experimente con diferentes encabezados Accept para comparar las respuestas y determinar qué encabezado es mejor para su caso de uso.

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
