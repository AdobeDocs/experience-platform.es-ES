---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Configuración de un campo de atributo calculado
topic-legacy: guide
type: Documentation
description: Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear utilizando la API del Registro de Esquemas para definir un esquema y una mezcla personalizada que alojará el campo de atributo calculado.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 2%

---

# (Alpha) Configuración de un campo de atributo calculado mediante la API del Registro de esquemas

>[!IMPORTANT]
>
>La funcionalidad de atributo computado está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear utilizando la API del Registro de Esquemas para definir un esquema y una mezcla personalizada que alojará el campo de atributo calculado. Se recomienda crear un esquema de &quot;Atributos calculados&quot; independiente y una combinación en la que su organización pueda añadir atributos que se vayan a utilizar como atributos calculados. Esto permite que la organización separe limpiamente el esquema de atributos calculados de otros esquemas que se están utilizando para la ingesta de datos.

El flujo de trabajo de este documento describe cómo utilizar la API del Registro de esquemas para crear un esquema de &quot;Atributo calculado&quot; habilitado para el perfil que haga referencia a una mezcla personalizada. Este documento contiene código de muestra específico para los atributos calculados. Sin embargo, consulte la [guía de API del Registro de Esquemas](../../xdm/api/overview.md) para obtener información detallada sobre la definición de mezclas y esquemas mediante la API.

## Crear una mezcla de atributos calculados

Para crear una mezcla utilizando la API del Registro del Esquema, comience por realizar una solicitud del POST al extremo `/tenant/mixins` y proporcionar los detalles de la mezcla en el cuerpo de la solicitud. Para obtener más información sobre cómo trabajar con mezclas utilizando la API del Registro de Esquemas, consulte la [guía de extremo de la API de mezclas](../../xdm/api/mixins.md).

**Formato de API**

```http
POST /tenant/mixins
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Mixin",
        "description":"Description of the mixin.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesMixin": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

| Propiedad | Descripción |
|---|---|
| `title` | El nombre de la mezcla que está creando. |
| `meta:intendedToExtend` | Clase XDM con la que se puede utilizar la mezcla. |

**Respuesta**

Una solicitud correcta devuelve el Estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles de la mezcla recién creada, incluidos `$id`, `meta:altIt` y `version`. Estos valores son de solo lectura y son asignados por el Registro de esquemas.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of the mixin.",
  "definitions": {
    "computedAttributesMixin": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesMixin",
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
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Actualizar mezcla con atributos calculados adicionales

A medida que se necesiten atributos más calculados, puede actualizar los atributos calculados mezclados con atributos adicionales realizando una solicitud de PUT al extremo `/tenant/mixins` . Esta solicitud requiere que incluya el ID exclusivo de la mezcla que ha creado en la ruta y todos los campos nuevos que desea añadir en el cuerpo.

Para obtener más información sobre la actualización de una mezcla mediante la API del Registro de Esquemas, consulte la [guía de extremo de la API de mezclas](../../xdm/api/mixins.md).

**Formato de API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

**Solicitud**

Esta solicitud agrega nuevos campos relacionados con la información `purchaseSummary`.

>[!NOTE]
>
>Al actualizar una mezcla a través de una solicitud del PUT, el cuerpo debe incluir todos los campos que serían necesarios al crear una nueva mezcla en una solicitud del POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Mixin",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of mixin.",
        "definitions": {
          "computedAttributesMixin": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la mezcla actualizada.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of mixin.",
  "definitions": {
    "computedAttributesMixin": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesMixin",
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
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Crear un esquema habilitado para perfil

Para crear un esquema con la API del Registro de esquemas, comience por realizar una solicitud de POST al extremo `/tenant/schemas` y proporcionar los detalles del esquema en el cuerpo de la solicitud. El esquema también debe estar habilitado para [!DNL Profile] y aparecer como parte del esquema de unión para la clase schema .

Para obtener más información sobre los esquemas y esquemas de unión [!DNL Profile] habilitados, consulte la [[!DNL Schema Registry] guía de API](../../xdm/api/overview.md) y la [documentación básica de la composición de esquema](../../xdm/schema/composition.md).

**Formato de API**

```http
POST /tenants/schemas
```

**Solicitud**

La siguiente solicitud crea un nuevo esquema que hace referencia al `computedAttributesMixin` creado anteriormente en este documento (con su ID único) y está habilitado para el esquema de unión Perfil (con la matriz `meta:immutableTags`). Para obtener instrucciones detalladas sobre cómo crear un esquema con la API del Registro de esquemas, consulte la [guía de extremo de la API de esquemas](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del esquema recién creado, incluidos `$id`, `meta:altId` y `version`. Estos valores son de solo lectura y son asignados por el Registro de esquemas.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## Pasos siguientes

Ahora que ha creado un esquema y una mezcla en los que se almacenarán los atributos calculados, puede crear el atributo calculado utilizando el extremo de API `/computedattributes`. Para ver los pasos detallados para crear un atributo calculado en la API, siga los pasos que se proporcionan en la [guía de extremo de la API de atributos calculados](ca-api.md).
