---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Cómo configurar un campo de atributo calculado
type: Documentation
description: Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor del atributo calculado. Este campo se puede crear con la API de Registro de esquemas para definir un esquema y un grupo de campos personalizados que albergarán el campo de atributo calculado.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 2%

---

# (Alpha) Configure un campo de atributo calculado usando la API de Registro de Esquemas

>[!IMPORTANT]
>
>Actualmente, la funcionalidad de atributos calculados está en formato alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor del atributo calculado. Este campo se puede crear con la API de Registro de esquemas para definir un esquema y un grupo de campos de esquema personalizado que contendrá el campo de atributo calculado. Se recomienda crear un esquema &quot;Atributos calculados&quot; y un grupo de campos independientes a los que su organización pueda agregar atributos para utilizarlos como atributos calculados. Esto permite a su organización separar claramente el esquema de atributos calculado de otros esquemas que se utilizan para la ingesta de datos.

El flujo de trabajo de este documento describe cómo utilizar la API de Registro de esquemas para crear un esquema de &quot;atributo calculado&quot; habilitado para perfiles que haga referencia a un grupo de campos personalizados. Este documento contiene un ejemplo de código específico para los atributos calculados; sin embargo, consulte la [Guía de API de Registro de esquemas](../../xdm/api/overview.md) para obtener información detallada sobre la definición de grupos de campos y esquemas mediante la API.

## Crear un grupo de campos de atributos calculados

Para crear un grupo de campos mediante la API de Registro de esquemas, comience realizando una solicitud de POST a la variable `/tenant/fieldgroups` y proporciona los detalles del grupo de campos en el cuerpo de la solicitud. Para obtener más información sobre cómo trabajar con grupos de campos mediante la API de Registro de esquemas, consulte la [guía de extremo de API de grupos de campos](../../xdm/api/field-groups.md).

**Formato de API**

```http
POST /tenant/fieldgroups
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
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
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| Propiedad | Descripción |
|---|---|
| `title` | Nombre del grupo de campos que está creando. |
| `meta:intendedToExtend` | La clase XDM con la que se puede utilizar el grupo de campos. |

**Respuesta**

Una solicitud correcta devuelve el estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del grupo de campos recién creado, incluido el `$id`, `meta:altIt`, y `version`. Estos valores son de sólo lectura y los asigna el Registro de esquemas.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
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
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
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

## Actualizar grupo de campos con atributos calculados adicionales

A medida que se necesiten más atributos calculados, puede actualizar el grupo de campos atributos calculados con atributos adicionales realizando una solicitud del PUT a `/tenant/fieldgroups` punto final. Esta solicitud requiere que incluya el ID único del grupo de campos que creó en la ruta y todos los campos nuevos que desee agregar en el cuerpo.

Para obtener más información sobre la actualización de un grupo de campos mediante la API de Registro de esquemas, consulte la [guía de extremo de API de grupos de campos](../../xdm/api/field-groups.md).

**Formato de API**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Solicitud**

Esta solicitud agrega nuevos campos relacionados con `purchaseSummary` información.

>[!NOTE]
>
>Al actualizar un grupo de campos mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios al crear un nuevo grupo de campos en una solicitud de POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
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
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del grupo de campos actualizado.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
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
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
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

## Creación de un esquema habilitado para el perfil

Para crear un esquema con la API de Registro de esquemas, comience por realizar una solicitud del POST a la variable `/tenant/schemas` y proporciona los detalles del esquema en el cuerpo de la solicitud. El esquema también debe estar habilitado para [!DNL Profile] y aparecen como parte del esquema de unión para la clase de esquema.

Para obtener más información sobre [!DNL Profile]Esquemas habilitados para y esquemas de unión, revise la [[!DNL Schema Registry] Guía de API](../../xdm/api/overview.md) y el [documentación de conceptos básicos de composición de esquemas](../../xdm/schema/composition.md).

**Formato de API**

```http
POST /tenants/schemas
```

**Solicitud**

La siguiente solicitud crea un nuevo esquema que hace referencia a `computedAttributesFieldGroup` creado anteriormente en este documento (con su ID único) y está habilitado para el esquema de unión de perfiles (con el `meta:immutableTags` matriz). Para obtener instrucciones detalladas sobre cómo crear un esquema con la API de Registro de esquemas, consulte la [guía de extremo de API de esquemas](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del esquema recién creado, incluido el `$id`, `meta:altId`, y `version`. Estos valores son de sólo lectura y los asigna el Registro de esquemas.

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
  "imsOrg": "{ORG_ID}",
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

Ahora que ha creado un esquema y un grupo de campos en los que se almacenarán los atributos calculados, puede crear el atributo calculado mediante la variable `/computedattributes` Extremo de API. Para ver los pasos detallados para crear un atributo calculado en la API, siga los pasos que se proporcionan en la [guía de extremo de API de atributos calculados](ca-api.md).
