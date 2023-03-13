---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de mezcla;registro de esquemas;mixin;mixin;mixins;crear
solution: Experience Platform
title: Punto final de API de Mixins
description: El extremo /mixins de la API de Registro de esquemas le permite administrar mediante programación mezclas XDM dentro de la aplicación de experiencia.
exl-id: 93ba2fe3-0277-4c06-acf6-f236cd33252e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 4%

---


# Extremo de mixins (obsoleto)

>[!IMPORTANT]
>
>Se ha cambiado el nombre de los mixins a grupos de campos de esquema y, por lo tanto, a `/mixins` El punto final ha quedado obsoleto en favor de `/fieldgroups` punto final.
>
>While `/mixins` se seguirá manteniendo como punto final heredado, se recomienda encarecidamente que utilice `/fieldgroups` para nuevas implementaciones de la API de Registro de esquemas en las aplicaciones de experiencia. Consulte la [guía de extremo de grupos de campos](./field-groups.md) para obtener más información.

Los mixins son componentes reutilizables que definen uno o varios campos que representan un concepto determinado, como una persona individual, una dirección de correo o un entorno de explorador web. Los mixins están pensados para incluirse como parte de un esquema que implementa una clase compatible, según el comportamiento de los datos que representan (registro o serie temporal). El `/mixins` punto final en la [!DNL Schema Registry] API permite administrar mezclas mediante programación dentro de la aplicación de experiencia.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API de ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de mixins {#list}

Puede enumerar todas las mezclas en `global` o `tenant` al realizar una solicitud de GET a `/global/mixins` o `/tenant/mixins`, respectivamente.

>[!NOTE]
>
>Al enumerar recursos, el Registro de esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos que superen este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato de API**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor del que desea recuperar las mezclas: `global` para mezclas creadas por el Adobe o `tenant` para mezclas propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la [documento anexo](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista de mezclas del `tenant` contenedor, usar un `orderby` parámetro de consulta para ordenar los mixins por su `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende de la variable `Accept` encabezado enviado en la solicitud. Lo siguiente `Accept` Los encabezados de están disponibles para enumerar las mezclas:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para enumerar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el mixin JSON completo para cada recurso, con el original `$ref` y `allOf` incluido. (Límite: 300) |

{style="table-layout:auto"}

**Respuesta**

La solicitud anterior utilizaba el `application/vnd.adobe.xed-id+json` `Accept` encabezado, por lo tanto la respuesta incluye solo el `title`, `$id`, `meta:altId`, y `version` atributos para cada mixin. Uso del otro `Accept` encabezado (`application/vnd.adobe.xed+json`) devuelve todos los atributos de cada mixin. Seleccione el adecuado `Accept` encabezado en función de la información que requiera en su respuesta.

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
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/mixins"
    }
  }
}
```

## Búsqueda de un mixin {#lookup}

Puede buscar un mixin específico incluyendo el ID del mixin en la ruta de una solicitud de GET.

**Formato de API**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que aloja el mixin que desea recuperar: `global` para un mixin creado con Adobe o `tenant` para un mixin propiedad de su organización. |
| `{MIXIN_ID}` | El `meta:altId` o con codificación URL `$id` del mixin que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera un mixin mediante su `meta:altId` valor proporcionado en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende de la variable `Accept` encabezado enviado en la solicitud. Todas las solicitudes de búsqueda requieren un `version` se incluirá en la `Accept` encabezado. Lo siguiente `Accept` Los encabezados de están disponibles:

| `Accept` header | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Sin procesar con `$ref` y `allOf`, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` y `allOf` resuelto, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version=1` | Sin procesar con `$ref` y `allOf`, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` y `allOf` resuelto, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` y `allOf` resuelto, se incluyen descriptores. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles del mixin. Los campos que se devuelven dependen del `Accept` encabezado enviado en la solicitud. Experimente con diferentes `Accept` para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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

## Creación de un mixin {#create}

Puede definir un mixin personalizado en las `tenant` contenedor realizando una solicitud de POST.

**Formato de API**

```http
POST /tenant/mixins
```

**Solicitud**

Al definir un nuevo mixin, debe incluir un `meta:intendedToExtend` atributo, que enumera `$id` de las clases con las que es compatible el mixin. En este ejemplo, el mixin es compatible con un `Property` clase que se definió anteriormente. Los campos personalizados deben estar anidados en `_{TENANT_ID}` (como se muestra en el ejemplo) para evitar conflictos con campos similares proporcionados por clases y otros mixins.

>[!NOTE]
>
>Para obtener más información sobre cómo definir distintos tipos de campo para incluirlos en el mixin, consulte la [guía de restricciones de campo](../schema/field-constraints.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
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

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del mixin recién creado, incluido el `$id`, `meta:altId`, y `version`. Estos valores son de solo lectura y los asigna el [!DNL Schema Registry].

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

Realización de una solicitud de GET a [enumerar todas las mezclas](#list) en el contenedor de inquilino ahora incluiría el mixin Detalles de propiedad, o puede hacer lo siguiente [realizar una solicitud de búsqueda (GET)](#lookup) uso de la codificación URL `$id` URI para ver el nuevo mixin directamente.

## Actualización de un mixin {#put}

Se puede reemplazar una mezcla completa mediante una operación de PUT, básicamente reescribiendo el recurso. Al actualizar un mixin mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios al [creación de un nuevo mixin](#create) en una solicitud de POST.

>[!NOTE]
>
>Si solo desea actualizar parte de un mixin en lugar de reemplazarlo por completo, consulte la sección sobre [actualización de una parte de un mixin](#patch).

**Formato de API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MIXIN_ID}` | El `meta:altId` o con codificación URL `$id` del mixin que desea volver a escribir. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud reescribe un mixin existente y agrega un nuevo `propertyCountry` field.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
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

Una respuesta correcta devuelve los detalles del mixin actualizado.

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

## Actualizar una parte de un mixin {#patch}

Puede actualizar una parte de un mixin mediante una solicitud de PATCH. El [!DNL Schema Registry] admite todas las operaciones de parche de JSON estándar, incluidas las siguientes `add`, `remove`, y `replace`. Para obtener más información sobre el parche JSON, consulte la [Guía de aspectos básicos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con valores nuevos en lugar de actualizar campos individuales, consulte la sección sobre [sustitución de un mixin mediante una operación de PUT](#put).

**Formato de API**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{MIXIN_ID}` | La codificación URL `$id` URI o `meta:altId` del mixin que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente actualiza el `description` de un mixin existente y añade un nuevo `propertyCity` field.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), en qué campo se debe realizar la operación (`path`) y qué información debe incluirse en esa operación (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
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

La respuesta muestra que ambas operaciones se realizaron correctamente. El `description` se ha actualizado, y `propertyCountry` se ha añadido en `definitions`.

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

## Eliminación de un mixin {#delete}

En ocasiones puede ser necesario quitar un mixin del Registro de esquemas. Esto se realiza realizando una solicitud de DELETE con el ID de mezcla proporcionado en la ruta.

**Formato de API**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MIXIN_ID}` | La codificación URL `$id` URI o `meta:altId` del mixin que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando una [solicitud de búsqueda (GET)](#lookup) al mixin. Deberá incluir un `Accept` en la solicitud, pero debe recibir un estado HTTP 404 (no encontrado) porque el mixin se ha eliminado del Registro de esquemas.
