---
title: Poner en desuso un campo XDM
description: Obtenga información sobre cómo eliminar los campos del Modelo de datos de experiencia (XDM) en la API del Registro de esquemas.
source-git-commit: a1b86e6976cdb5b2bd3c2ecee933dfde337c9880
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 6%

---

# Poner en desuso un campo XDM

En el Modelo de datos de Experience (XDM), puede eliminar de la memoria intermedia un campo dentro de un esquema o recurso personalizado utilizando la variable [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). El hecho de que un campo quede obsoleto hace que se oculte de las IU posteriores, como la [!UICONTROL Perfiles] espacio de trabajo y Customer Journey Analytics, pero por lo demás es un cambio no irruptivo y no afecta negativamente a los flujos de datos existentes.

Este documento explica cómo desactivar campos para distintos recursos XDM.

## Primeros pasos

Este tutorial requiere realizar llamadas a la API del Registro de esquemas. Revise el [guía para desarrolladores](../api/getting-started.md) para obtener información importante que debe conocer para realizar estas llamadas de API. Esto incluye el `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al `Accept` y sus posibles valores).

## Poner en desuso un campo personalizado {#custom}

Para eliminar un campo de una clase, un grupo de campos o un tipo de datos personalizados, actualice el recurso personalizado mediante una solicitud del PUT o del PATCH y añada el atributo `meta:status: deprecated` al campo en cuestión.

>[!NOTE]
>
>Para obtener información general sobre la actualización de recursos personalizados en XDM, consulte la siguiente documentación:
>
>* [Actualizar una clase](../api/classes.md#patch)
>* [Actualizar un grupo de campos](../api/field-groups.md#patch)
>* [Actualizar un tipo de datos](../api/data-types.md#patch)


La llamada de API de ejemplo que se muestra a continuación desaprueba un campo de un tipo de datos personalizado.

**Formato de API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Solicitud**

La siguiente solicitud desaprueba el `expansionArea` campo para un tipo de datos que describe una propiedad inmobiliaria.

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

Una respuesta correcta devuelve los detalles de actualización del recurso personalizado, con el campo obsoleto que contiene un `meta:status` valor de `deprecated`. La respuesta de ejemplo siguiente se ha truncado para el espacio.

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

## Poner en desuso un campo estándar en un esquema {#standard}

Los campos de clases estándar, grupos de campos y tipos de datos no se pueden retirar directamente. En su lugar, puede eliminar su uso en los esquemas individuales que emplean estos recursos estándar utilizando un descriptor.

### Creación de un descriptor de desaprobación de campo {#create-descriptor}

Para crear un descriptor para los campos de esquema que desea eliminar, realice una solicitud de POST al `/tenant/descriptors` punto final.

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
| `@type` | Tipo de descriptor. Para un descriptor de desaprobación de campos, este valor debe establecerse en `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | El URI `$id` del esquema al que está aplicando el descriptor. |
| `xdm:sourceVersion` | Versión del esquema al que está aplicando el descriptor. Debe configurarse como `1`. |
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

### Comprobar el campo obsoleto {#verify-deprecation}

Una vez aplicado el descriptor, puede verificar si el campo ha quedado obsoleto buscando el esquema en cuestión mientras utiliza el `Accept` encabezado.

>[!NOTE]
>
>Actualmente no se admite la visualización de campos obsoletos cuando se enumeran esquemas.

**Formato de API**

```http
GET /tenant/schemas
```

**Solicitud**

Para incluir información sobre campos obsoletos en la respuesta de API, debe establecer la variable `Accept` Encabezado a `application/vnd.adobe.xed-deprecatefield+json; version=1`.

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

Una respuesta correcta devuelve los detalles del esquema, con el campo obsoleto que contiene un `meta:status` valor de `deprecated`. La respuesta de ejemplo siguiente se ha truncado para el espacio.

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

Este documento abarcaba cómo eliminar los campos XDM mediante la API del Registro de esquemas. Para obtener más información sobre la configuración de campos para los recursos personalizados, consulte la guía de [definición de campos XDM en la API](./custom-fields-api.md). Para obtener más información sobre la administración de descriptores, consulte la [guía de extremo de descriptores](../api/descriptors.md).
