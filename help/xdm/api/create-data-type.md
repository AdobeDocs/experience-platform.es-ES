---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear un tipo de datos
topic: developer guide
translation-type: tm+mt
source-git-commit: b0d8c8ee4df11d601d8feb122c70a9cd5d7d5b77

---


# Crear un tipo de datos

Cuando hay estructuras de datos comunes que su organización desea utilizar de varias formas, es posible que desee definir un tipo de datos. Los tipos de datos permiten el uso coherente de estructuras de varios campos, con más flexibilidad que las mezclas, ya que se pueden incluir en cualquier lugar de un esquema agregándolas como el `type` de un campo.

En otras palabras, los tipos de datos permiten definir una jerarquía de objetos una vez y hacer referencia a ella en un campo de la misma manera que cualquier otro tipo escalar.

**Formato API**

```http
POST /tenant/datatypes
```

**Solicitud**

La definición de un tipo de datos no requiere `meta:extends` `meta:intendedToExtend` ni campos, ni tampoco es necesario anidar campos para evitar conflictos.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del tipo de datos recién creado, incluidos el `$id`, `meta:altId`y `version`. Estos tres valores son de sólo lectura y son asignados por el Registro de Esquemas.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Realizar una solicitud GET para lista de todos los tipos de datos en el contenedor del inquilino ahora incluiría el tipo de datos Construcción de propiedades. También puede realizar una solicitud de búsqueda (GET) utilizando el `$id` URI con codificación de URL para vista directa del nuevo tipo de datos. Asegúrese de incluir la solicitud de búsqueda `version` en el encabezado Accept.
