---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;update;Update;patch;PATCH
solution: Experience Platform
title: Actualizar un recurso
description: 'Puede modificar o actualizar los recursos en el contenedor del inquilino mediante una solicitud de PATCH. El Registro de Esquemas admite todas las operaciones de parche de JSON estándar, incluidas la adición, eliminación y sustitución. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# Actualizar un recurso

Puede modificar o actualizar los recursos en el contenedor del inquilino mediante una solicitud de PATCH. El [!DNL Schema Registry] admite todas las operaciones estándar de Parche JSON, incluidas la adición, eliminación y sustitución.

Para obtener más información sobre JSON Patch, incluidas las operaciones disponibles, consulte la documentación [oficial de](http://jsonpatch.com/)JSON Patch.

>[!NOTE]
>
>Si desea reemplazar un recurso completo por valores nuevos en lugar de actualizar campos individuales, consulte el documento sobre [reemplazar un recurso mediante una operación](replace-resource.md)de PUT.

## Añadir mezclas a un esquema

Una de las operaciones de PATCH más comunes consiste en añadir mezclas previamente definidas a un esquema XDM, como se muestra en el ejemplo siguiente.

**Formato API**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a actualizar desde el [!DNL Schema Library]. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |
| `{RESOURCE_ID}` | El `$id` URI con codificación URL o `meta:altId` del recurso. |

**Solicitud**

Mediante una operación de PATCH, puede actualizar un esquema para incluir campos definidos en una mezcla creada previamente. Para ello, debe realizar una solicitud de PATCH al esquema utilizando su `meta:altId` o el URI con codificación de URL `$id` .

El cuerpo de la solicitud incluye la operación (`op`) que desea realizar, dónde (`path`) desea realizar la operación y qué información (`value`) desea incluir en la operación. En este ejemplo, el valor de la mezcla `$id` se agrega a los campos `meta:extends` y `allOf` del esquema de destinatario.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**Respuesta**

La respuesta muestra que ambas operaciones se realizaron correctamente. La mezcla `$id` se ha agregado a la `meta:extends` matriz y ahora aparece una referencia (`$ref`) a la mezcla `$id` en la `allOf` matriz.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Actualizar campos individuales para un recurso

También puede enviar solicitudes de PATCH que realicen varios cambios en campos individuales dentro de un recurso del Registro de Esquemas.

**Formato API**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a actualizar desde el [!DNL Schema Library]. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |
| `{RESOURCE_ID}` | El `$id` URI con codificación URL o `meta:altId` del recurso. |

**Solicitud**

El cuerpo de la solicitud incluye la operación (`op`), la ubicación (`path`) y la información (`value`) necesaria para actualizar la mezcla. Esta solicitud actualiza la combinación de Detalles de propiedad para quitar el campo &quot;propertyCity&quot; y agregar un nuevo campo &quot;propertyAddress&quot; que hace referencia a un tipo de datos estándar que contiene información de dirección. También agrega un nuevo campo &quot;emailAddress&quot; que hace referencia a un tipo de datos estándar con información de correo electrónico.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Respuesta**

Una respuesta correcta muestra que las operaciones se completaron correctamente porque los campos nuevos están presentes y se ha eliminado el campo &quot;propertyCity&quot;.

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "propertyType": {
                            "type": "string",
                            "title": "Property Type",
                            "description": "Type and primary use of property.",
                            "enum": [
                                "retail",
                                "yoga",
                                "fitness"
                            ],
                            "meta:enum": {
                                "retail": "Retail Store",
                                "yoga": "Yoga Studio",
                                "fitness": "Fitness Center"
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
