---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;grupo de campos;grupo de campos;grupos de campos;crear
solution: Experience Platform
title: Extremo de API de grupos de campos
description: El extremo /fieldgroups de la API de Registro de esquemas le permite administrar mediante programación grupos de campos de esquema XDM dentro de la aplicación de experiencia.
exl-id: d26257e4-c7d5-4bff-b555-7a2997c88c74
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 3%

---

# Extremo de grupos de campos de esquema

Los grupos de campos de esquema son componentes reutilizables que definen uno o varios campos que representan un concepto determinado, como una persona individual, una dirección de correo o un entorno de explorador web. Los grupos de campos están pensados para incluirse como parte de un esquema que implementa una clase compatible, según el comportamiento de los datos que representan (registro o serie temporal). El extremo `/fieldgroups` de la API [!DNL Schema Registry] le permite administrar mediante programación grupos de campos dentro de la aplicación de experiencia.

## Introducción

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de grupos de campos {#list}

Puede enumerar todos los grupos de campos bajo el contenedor `global` o `tenant` realizando una solicitud de GET a `/global/fieldgroups` o `/tenant/fieldgroups`, respectivamente.

>[!NOTE]
>
>Al enumerar recursos, el Registro de esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos que superen este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato de API**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor del que desea recuperar los grupos de campos: `global` para los grupos de campos creados mediante Adobe o `tenant` para los grupos de campos propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte el [documento del apéndice](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista de grupos de campos del contenedor `tenant`, con un parámetro de consulta `orderby` para ordenar los grupos de campos por su atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para enumerar grupos de campos:

| `Accept` encabezado | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para enumerar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el grupo de campos JSON completo para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

{style="table-layout:auto"}

**Respuesta**

La solicitud anterior utilizó el encabezado `application/vnd.adobe.xed-id+json` `Accept`, por lo que la respuesta solo incluye los atributos `title`, `$id`, `meta:altId` y `version` para cada grupo de campos. Al usar el otro encabezado `Accept` (`application/vnd.adobe.xed+json`) se devuelven todos los atributos de cada grupo de campos. Seleccione el encabezado `Accept` apropiado según la información que necesite en la respuesta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.mixins.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.mixins.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.mixins.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.mixins.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## Búsqueda de un grupo de campos {#lookup}

Puede buscar un grupo de campos específico incluyendo el ID del grupo de campos en la ruta de una solicitud de GET.

**Formato de API**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que aloja el grupo de campos que desea recuperar: `global` para un grupo de campos creado mediante Adobe o `tenant` para un grupo de campos propiedad de su organización. |
| `{FIELD_GROUP_ID}` | `meta:altId` o `$id` con codificación de dirección URL del grupo de campos que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera un grupo de campos por su valor `meta:altId` proporcionado en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Todas las solicitudes de búsqueda requieren que se incluya un `version` en el encabezado `Accept`. Los siguientes `Accept` encabezados están disponibles:

| `Accept` encabezado | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Sin procesar con `$ref` y `allOf`, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` y `allOf` resueltos, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Sin procesar con `$ref` y `allOf`, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` y `allOf` resueltos, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` y `allOf` resueltos, se incluyen descriptores. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles del grupo de campos. Los campos que se devuelven dependen del encabezado `Accept` enviado en la solicitud. Experimente con diferentes encabezados `Accept` para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
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

## Creación de un grupo de campos {#create}

Puede definir un grupo de campos personalizados bajo el contenedor `tenant` realizando una solicitud de POST.

**Formato de API**

```http
POST /tenant/fieldgroups
```

**Solicitud**

Al definir un nuevo grupo de campos, debe incluir un atributo `meta:intendedToExtend`, que enumere `$id` de las clases con las que es compatible el grupo de campos. En este ejemplo, el grupo de campos es compatible con una clase `Property` definida anteriormente. Los campos personalizados deben anidarse en `_{TENANT_ID}` (como se muestra en el ejemplo) para evitar conflictos con campos similares proporcionados por clases y otros grupos de campos.

>[!NOTE]
>
>Para obtener más información sobre cómo definir distintos tipos de campo para incluirlos en el grupo de campos, consulte la guía sobre [definición de campos personalizados en la API](../tutorials/custom-fields-api.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del grupo de campos recién creado, incluidos `$id`, `meta:altId` y `version`. Estos valores son de sólo lectura y los asigna el [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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
      "$ref": "#/definitions/customFields",
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

Al realizar una solicitud de GET para [enumerar todos los grupos de campos](#list) en el contenedor de inquilino, ahora se incluiría el grupo de campos Detalles de propiedad; o bien, puede [realizar una solicitud de búsqueda (GET)](#lookup) utilizando el URI `$id` con codificación de dirección URL para ver el nuevo grupo de campos directamente.

## Actualización de un grupo de campos {#put}

Puede reemplazar un grupo de campos completo mediante una operación de PUT, básicamente reescribiendo el recurso. Al actualizar un grupo de campos mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios al [crear un nuevo grupo de campos](#create) en una solicitud de POST.

>[!NOTE]
>
>Si solo desea actualizar parte de un grupo de campos en lugar de reemplazarlo por completo, consulte la sección sobre [actualizar una parte de un grupo de campos](#patch).

**Formato de API**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{FIELD_GROUP_ID}` | `meta:altId` o `$id` con codificación de dirección URL del grupo de campos que desea volver a escribir. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud reescribe un grupo de campos existente y agrega un nuevo campo `propertyCountry`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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

Una respuesta correcta devuelve los detalles del grupo de campos actualizado.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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
  "imsOrg": "{ORG_ID}",
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

## Actualizar una parte de un grupo de campos {#patch}

Puede actualizar una parte de un grupo de campos mediante una solicitud de PATCH. [!DNL Schema Registry] admite todas las operaciones de parche de JSON estándar, incluidas `add`, `remove` y `replace`. Para obtener más información sobre el parche JSON, consulte la [guía de aspectos básicos de la API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con valores nuevos en lugar de actualizar campos individuales, consulte la sección sobre [reemplazo de un grupo de campos mediante una operación de PUT](#put).

**Formato de API**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{FIELD_GROUP_ID}` | URI `$id` con codificación de dirección URL o `meta:altId` del grupo de campos que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente actualiza `description` de un grupo de campos existente y agrega un nuevo campo `propertyCity`.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), en qué campo se debe realizar la operación (`path`) y qué información se debe incluir en esa operación (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**Respuesta**

La respuesta muestra que ambas operaciones se realizaron correctamente. Se ha actualizado `description` y se ha agregado `propertyCountry` en `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
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
  "imsOrg": "{ORG_ID}",
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

## Eliminación de un grupo de campos {#delete}

En ocasiones puede ser necesario quitar un grupo de campos del Registro de esquemas. Para ello, realice una solicitud de DELETE con el ID de grupo de campos proporcionado en la ruta.

**Formato de API**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{FIELD_GROUP_ID}` | El URI `$id` con codificación URL o `meta:altId` del grupo de campos que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación si intenta realizar una [solicitud de búsqueda (GET)](#lookup) al grupo de campos. Deberá incluir un encabezado `Accept` en la solicitud, pero debería recibir el estado HTTP 404 (no encontrado) porque el grupo de campos se ha eliminado del Registro de esquemas.
