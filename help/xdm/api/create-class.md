---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear una clase
topic: developer guide
translation-type: tm+mt
source-git-commit: 60911e32fd9235be2a258e60818011a42cd5ceba

---


# Crear una clase

El principal componente de un esquema es una clase. La clase contiene el conjunto mínimo de campos que se deben definir para capturar los datos principales de un esquema. Por ejemplo, si diseñara un esquema para automóviles y camiones, lo más probable es que utilizaría una clase llamada Vehículo que describiera las propiedades comunes básicas de todos los vehículos.

Adobe y otros socios de la plataforma de experiencia proporcionan varias clases estándar, pero también puede definir sus propias clases y guardarlas en el Registro de Esquema. A continuación, puede componer un esquema que implemente la clase que ha creado y definir mezclas compatibles con la clase recién definida.

>[!NOTE] Al componer un esquema basado en una clase definida, no podrá utilizar mezclas estándar. Cada mezcla define las clases con las que son compatibles en sus `meta:intendedToExtend` atributos. Una vez que comience a definir mezclas compatibles con su nueva clase (utilizando la `$id` de su nueva clase en el `meta:intendedToExtend` campo de la mezcla), podrá reutilizar esas mezclas cada vez que defina un esquema que implemente la clase que ha definido. Consulte las secciones sobre [creación de mezclas](create-mixin.md) y [creación de esquemas](create-schema.md) para obtener más información.

**Formato API**

```http
POST /tenant/classes
```

**Solicitud**

La solicitud para crear (POST) una clase debe incluir un `allOf` atributo que contenga `$ref` a uno de los dos valores: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Estos valores representan el comportamiento en el que se basa la clase (registro o serie temporal, respectivamente). Para obtener más información sobre las diferencias entre los datos de registros y los datos de series temporales, consulte la sección sobre los tipos de comportamiento dentro de los [conceptos básicos de la composición](../schema/composition.md)de esquemas.

Al definir una clase, también puede incluir mezclas o campos personalizados en la definición de clase. Esto haría que las mezclas y campos agregados se incluyeran en todos los esquemas que implementan la clase. La siguiente solicitud de ejemplo define una clase llamada &quot;Property&quot;, que captura información sobre diferentes propiedades que son propiedad de una compañía y que son operadas por ella. Incluye un `propertyId` campo que se incluirá cada vez que se utilice la clase.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `_{TENANT_ID}` | La `TENANT_ID` Área de nombres de su organización. Todos los recursos creados por su organización deben incluir esta propiedad para evitar conflictos con otros recursos en el Registro de Esquemas. |
| `allOf` | lista de recursos cuyas propiedades van a heredar la nueva clase. Uno de los `$ref` objetos de la matriz define el comportamiento de la clase. En este ejemplo, la clase hereda el comportamiento &quot;record&quot;. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles de la clase recién creada, incluidos los `$id`, `meta:altId`y `version`. Estos tres valores son de sólo lectura y son asignados por el Registro de Esquemas.

```JSON
{
    "title": "Property",
    "description": "Properties owned and operated by the company.",
    "type": "object",
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "property": {
                            "title": "Property Information",
                            "type": "object",
                            "description": "Information about different owned and operated properties.",
                            "properties": {
                                "propertyId": {
                                    "title": "Property Identification Number",
                                    "type": "string",
                                    "description": "Unique Property identification number",
                                    "meta:xdmType": "string"
                                }
                            },
                            "meta:xdmType": "object"
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
            "$ref": "https://ns.adobe.com/xdm/data/record"
        },
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "version": "1.0",
    "meta:resourceType": "classes",
    "meta:registryMetadata": {
        "repo:createDate": 1552086405448,
        "repo:lastModifiedDate": 1552086405448,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Realizar una solicitud GET para lista de todas las clases en el contenedor del inquilino ahora incluiría la clase Property. También puede realizar una solicitud de búsqueda (GET) utilizando el `$id` URI con codificación URL para realizar la vista de la nueva clase directamente. Asegúrese de incluir el `version` en el encabezado Accept al realizar una solicitud de búsqueda.
