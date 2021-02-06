---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de mezcla;Registro de Esquemas;mezcla;mezclas;mezclas;crear
solution: Experience Platform
title: Extremo de la API de mezclas
description: El extremo /mixins de la API del Registro de Esquema le permite administrar mediante programación mezclas XDM dentro de la aplicación de experiencia.
topic: developer guide
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 2%

---


# Extremo de mezclas

Las mezclas son componentes reutilizables que definen uno o más campos que representan un concepto particular, como una persona individual, una dirección de correo o un entorno de explorador Web. Las mezclas están pensadas para incluirse como parte de un esquema que implementa una clase compatible, en función del comportamiento de los datos que representan (registro o serie temporal). El extremo `/mixins` de la API [!DNL Schema Registry] le permite administrar mediante programación las mezclas dentro de la aplicación de experiencia.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas exitosas a cualquier API de Experience Platform.

## Recuperar una lista de mezclas {#list}

Puede lista todas las mezclas bajo el contenedor `global` o `tenant` haciendo una solicitud de GET a `/global/mixins` o `/tenant/mixins`, respectivamente.

>[!NOTE]
>
>Al enumerar los recursos, el Registro de Esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos más allá de este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato API**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor del que desea recuperar las mezclas: `global` para mezclas creadas en Adobe o `tenant` para mezclas que sean propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales para filtrar los resultados. Consulte el [documento del apéndice](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

**Solicitud**

La siguiente solicitud recupera una lista de mezclas del contenedor `tenant`, utilizando un parámetro de consulta `orderby` para ordenar las mezclas por su atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para enumerar las mezclas:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Éste es el encabezado recomendado para enumerar los recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve una mezcla JSON completa para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

**Respuesta**

En la solicitud anterior se utilizó el encabezado `application/vnd.adobe.xed-id+json` `Accept`, por lo que la respuesta sólo incluye los atributos `title`, `$id`, `meta:altId` y `version` para cada mezcla. El uso del otro encabezado `Accept` (`application/vnd.adobe.xed+json`) devuelve todos los atributos de cada mezcla. Seleccione el encabezado `Accept` correspondiente en función de la información que necesite en la respuesta.

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

## Buscar una mezcla {#lookup}

Puede buscar una mezcla específica incluyendo el ID de la mezcla en la ruta de una solicitud de GET.

**Formato API**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que alberga la mezcla que desea recuperar: `global` para una mezcla creada por Adobe o `tenant` para una mezcla propiedad de su organización. |
| `{MIXIN_ID}` | El `meta:altId` o el `$id` con codificación URL de la mezcla que desea buscar. |

**Solicitud**

La siguiente solicitud recupera una mezcla por su valor `meta:altId` proporcionado en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Todas las solicitudes de búsqueda requieren que se incluya `version` en el encabezado `Accept`. Los siguientes `Accept` encabezados están disponibles:

| `Accept` header | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Sin procesar con `$ref` y `allOf`, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` y  `allOf` resuelto, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Sin formato con `$ref` y `allOf`, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` y  `allOf` resuelto, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` y  `allOf` resueltos, se incluyen los descriptores. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la mezcla. Los campos devueltos dependen del encabezado `Accept` enviado en la solicitud. Experimente con diferentes `Accept` encabezados para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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

## Crear una mezcla {#create}

Puede definir una mezcla personalizada en el contenedor `tenant` haciendo una solicitud de POST.

**Formato API**

```http
POST /tenant/mixins
```

**Solicitud**

Al definir una nueva mezcla, debe incluir un atributo `meta:intendedToExtend`, enumerando las `$id` clases con las que la mezcla es compatible. En este ejemplo, la mezcla es compatible con una clase `Property` definida anteriormente. Los campos personalizados deben anidarse en `_{TENANT_ID}` (como se muestra en el ejemplo) para evitar conflictos con campos similares proporcionados por clases y otras mezclas.

>[!NOTE]
>
>Para obtener más información sobre cómo definir diferentes tipos de campos para incluir en la mezcla, consulte la [guía de restricciones de campo](../schema/field-constraints.md#define-fields).

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

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles de la mezcla recién creada, incluidos los `$id`, `meta:altId` y `version`. Estos valores son de sólo lectura y son asignados por [!DNL Schema Registry].

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

Al realizar una solicitud de GET a [lista de todas las mezclas](#list) en el contenedor del inquilino, ahora se incluirá la combinación Detalles de propiedad, o bien [se puede realizar una solicitud de búsqueda (GET)](#lookup) utilizando el URI `$id` codificado con URL para vista directa de la nueva mezcla.

## Actualizar una mezcla {#put}

Puede reemplazar una mezcla completa mediante una operación de PUT, básicamente reescribiendo el recurso. Al actualizar una mezcla mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios cuando [cree una nueva mezcla](#create) en una solicitud de POST.

>[!NOTE]
>
>Si sólo desea actualizar parte de una mezcla en lugar de reemplazarla por completo, consulte la sección sobre [actualización de una porción de una mezcla](#patch).

**Formato API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MIXIN_ID}` | El `meta:altId` o el `$id` codificado con URL de la mezcla que desea volver a escribir. |

**Solicitud**

La siguiente solicitud vuelve a escribir una mezcla existente, agregando un nuevo campo `propertyCountry`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una respuesta correcta devuelve los detalles de la mezcla actualizada.

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

## Actualizar una porción de una mezcla {#patch}

Puede actualizar una parte de una mezcla mediante una solicitud de PATCH. El [!DNL Schema Registry] soporta todas las operaciones estándar de parche JSON, incluyendo `add`, `remove` y `replace`. Para obtener más información sobre JSON Patch, consulte la [guía de principios de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con nuevos valores en lugar de actualizar campos individuales, consulte la sección sobre [reemplazo de una mezcla mediante una operación de PUT](#put).

**Formato API**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{MIXIN_ID}` | El URI `$id` con codificación URL o `meta:altId` de la mezcla que desea actualizar. |

**Solicitud**

La siguiente solicitud de ejemplo actualiza el `description` de una mezcla existente y agrega un nuevo campo `propertyCity`.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), el campo en el que se debe realizar la operación (`path`) y la información que se debe incluir en esa operación (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

La respuesta muestra que ambas operaciones se realizaron correctamente. El `description` se ha actualizado y `propertyCountry` se ha agregado en `definitions`.

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

## Eliminar una mezcla {#delete}

Ocasionalmente puede ser necesario retirar una mezcla del Registro de Esquemas. Esto se realiza mediante una solicitud de DELETE con el ID de mezcla proporcionado en la ruta.

**Formato API**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{MIXIN_ID}` | El URI `$id` con codificación URL o `meta:altId` de la mezcla que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar la eliminación, intente una solicitud de [búsqueda (GET)](#lookup) a la mezcla. Deberá incluir un encabezado `Accept` en la solicitud, pero debe recibir un estado HTTP 404 (no encontrado) porque la mezcla se ha eliminado del Registro de Esquemas.