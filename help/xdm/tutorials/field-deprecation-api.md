---
title: Dejar de utilizar un campo XDM en la API
description: Obtenga información sobre cómo dejar de utilizar los campos de Modelo de datos de experiencia (XDM) en la API de Registro de esquemas.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 6%

---

# Dejar de utilizar un campo XDM en la API

En Experience Data Model (XDM), puede retirar un campo de un esquema o recurso personalizado mediante la [API de Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Si se deja de utilizar un campo, se ocultará de las interfaces de usuario que siguen el flujo de trabajo, como el espacio de trabajo y el Customer Journey Analytics de [!UICONTROL Perfiles], pero, por lo demás, no supone un cambio importante y no afecta negativamente a los flujos de datos existentes.

Este documento explica cómo dejar de utilizar los campos para diferentes recursos XDM. Para ver los pasos sobre cómo dejar de utilizar un campo XDM mediante el Editor de esquemas en la interfaz de usuario del Experience Platform, consulte el tutorial sobre [dejar de utilizar un campo XDM en la IU](./field-deprecation-ui.md).

## Introducción

Este tutorial requiere realizar llamadas a la API de Registro de esquemas. Consulte la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesite conocer a fin de realizar estas llamadas a la API. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados necesarios para realizar solicitudes (con especial atención al encabezado `Accept` y sus posibles valores).

## Dejar obsoleto un campo personalizado {#custom}

Para dejar de utilizar un campo en una clase, grupo de campos o tipo de datos personalizado, actualice el recurso personalizado mediante una solicitud de PUT o PATCH y agregue el atributo `meta:status: deprecated` al campo en cuestión.

>[!NOTE]
>
>Para obtener información general sobre la actualización de recursos personalizados en XDM, consulte la siguiente documentación:
>
>* [Actualizar una clase](../api/classes.md#patch)
>* [Actualizar un grupo de campos](../api/field-groups.md#patch)
>* [Actualizar un tipo de datos](../api/data-types.md#patch)

La llamada de API de ejemplo siguiente anula la compatibilidad de un campo en un tipo de datos personalizado.

**Formato de API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Solicitud**

La siguiente solicitud anula la compatibilidad del campo `expansionArea` con un tipo de datos que describe una propiedad inmobiliaria.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de actualización del recurso personalizado, con el campo obsoleto que contiene un valor `meta:status` de `deprecated`. La respuesta de ejemplo siguiente se ha truncado para el espacio.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
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
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Dejar obsoleto un campo estándar en un esquema {#standard}

Los campos de clases estándar, grupos de campos y tipos de datos no pueden quedar directamente obsoletos. En su lugar, puede descontinuar su uso en los esquemas individuales que emplean estos recursos estándar mediante un descriptor.

### Creación de un descriptor de obsolescencia de campo {#create-descriptor}

Para crear un descriptor para los campos de esquema que desea retirar, realice una solicitud de POST al extremo `/tenant/descriptors`.

**Formato de API**

```http
POST /tenant/descriptors
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | El tipo de descriptor. Para un descriptor de desaprobación de campo, este valor debe establecerse en `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` del esquema al que está aplicando el descriptor. |
| `xdm:sourceVersion` | La versión del esquema al que está aplicando el descriptor. Debe establecerse en `1`. |
| `xdm:sourceProperty` | Ruta a la propiedad dentro del esquema al que está aplicando el descriptor. Si desea aplicar el descriptor a varias propiedades, puede proporcionar una lista de rutas en forma de matriz (por ejemplo, `["/firstName", "/lastName"]`). |

**Respuesta**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Compruebe el campo obsoleto {#verify-deprecation}

Una vez aplicado el descriptor, puede comprobar si el campo ha quedado obsoleto buscando el esquema en cuestión mientras utiliza el encabezado `Accept` adecuado.

>[!NOTE]
>
>Actualmente no se admite mostrar los campos obsoletos cuando se enumeran esquemas.

**Formato de API**

```http
GET /tenant/schemas
```

**Solicitud**

Para incluir información sobre campos obsoletos en la respuesta de la API, debe establecer el encabezado `Accept` en `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema, con el campo obsoleto que contiene un valor `meta:status` de `deprecated`. La respuesta de ejemplo siguiente se ha truncado para el espacio.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Pasos siguientes

En este documento se explica cómo dejar de utilizar los campos XDM mediante la API de Registro de esquemas. Para obtener más información sobre la configuración de campos para recursos personalizados, consulte la guía sobre [definición de campos XDM en la API](./custom-fields-api.md). Para obtener más información sobre la administración de descriptores, consulte la [guía de extremo de descriptores](../api/descriptors.md).
