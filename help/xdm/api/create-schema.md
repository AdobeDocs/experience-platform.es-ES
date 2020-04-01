---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear un esquema
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db

---


# Crear un esquema

Un esquema se puede considerar como el modelo para los datos que desea transferir a la plataforma de experiencia. Cada esquema está compuesto por una clase y cero o más mezclas. En otras palabras, no es necesario añadir una mezcla para definir un esquema, pero en la mayoría de los casos se utilizará al menos una mezcla.

El proceso de composición de esquema comienza asignando una clase. La clase define los aspectos de comportamiento clave de los datos (registro o serie temporal), así como los campos mínimos requeridos para describir los datos que se van a ingestar.

**Formato API**

```http
POST /tenant/schemas
```

**Solicitud**

La solicitud debe incluir un `allOf` atributo que haga referencia al `$id` de una clase. Este atributo define la &quot;clase base&quot; que implementará el esquema. En este ejemplo, la clase base es una clase &quot;Información de propiedad&quot; que se creó anteriormente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `allOf > $ref` | El `$id` valor de la clase que implementará el nuevo esquema. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del esquema recién creado, incluidos el `$id`, `meta:altId`y `version`. Estos valores son de sólo lectura y son asignados por el Registro de Esquemas.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Al realizar una solicitud GET para lista de todos los esquemas en el contenedor del inquilino, ahora se incluirá el esquema de información de propiedad, o bien se puede realizar una solicitud de búsqueda (GET) utilizando el `$id` URI con codificación de URL para vista directa del nuevo esquema. Recuerde incluir el `version` en el encabezado Aceptar para todas las solicitudes de búsqueda.
