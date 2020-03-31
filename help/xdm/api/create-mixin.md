---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear una mezcla
topic: developer guide
translation-type: tm+mt
source-git-commit: b2ceac3de73ac622dc885eb388e46e93551f43a8

---


# Crear una mezcla

Las mezclas son un conjunto de campos utilizados para describir un concepto concreto, como &quot;dirección&quot; o &quot;preferencias de perfil&quot;. Existen numerosas mezclas estándar disponibles o puede definir las suyas cuando desee capturar información exclusiva de su organización. Cada mezcla contiene un `meta:intendedToExtend` campo que lista las clases con las que es compatible la mezcla.

Puede que le resulte útil revisar todas las mezclas disponibles para familiarizarse con los campos incluidos en cada una. Puede realizar la lista (GET) de todas las mezclas compatibles con una clase determinada realizando una solicitud con cada uno de los contenedores &quot;global&quot; y &quot;inquilino&quot;, devolviendo solo aquellas mezclas en las que el campo &quot;meta:didToExtend&quot; coincida con la clase que está utilizando. Los ejemplos siguientes devolverán todas las mezclas que se pueden utilizar con la clase de Perfil XDM Individual:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

La solicitud de API de ejemplo siguiente crea una nueva mezcla en el contenedor del inquilino.

**Formato API**

```http
POST /tenant/mixins
```

**Solicitud**

Al definir una nueva mezcla, debe incluir un `meta:intendedToExtend` atributo, enumerando el número `$id` de clases con las que la mezcla es compatible. En este ejemplo, la mezcla es compatible con la clase Property que definió anteriormente. Los campos personalizados deben anidarse en `_{TENANT_ID}` (como se muestra en el ejemplo) para evitar conflictos con otras mezclas o campos de los esquemas de clase. Observe que el `propertyConstruction` campo es una referencia al tipo de datos creado en la llamada anterior.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
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
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles de la mezcla recién creada, incluidos los `$id`, `meta:altId`y `version`. Estos valores son de sólo lectura y son asignados por el Registro de Esquemas.

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
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
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
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Al realizar una solicitud GET para lista de todas las mezclas en el contenedor del inquilino, ahora se incluirá la combinación Detalles del vehículo, o bien se puede realizar una solicitud de búsqueda (GET) utilizando el `$id` URI con codificación URL para realizar la vista de la nueva mezcla directamente. Recuerde incluir el `version` en el encabezado Aceptar para todas las solicitudes de búsqueda.
