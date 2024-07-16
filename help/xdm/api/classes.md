---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de clases;registro de esquemas;clase;clases;clases;crear
solution: Experience Platform
title: Extremo de API de clases
description: El extremo /classes de la API de Registro de esquemas permite administrar mediante programación las clases XDM dentro de la aplicación de experiencia.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 2%

---

# Extremo de clases

Todos los esquemas XDM (Experience Data Model) deben basarse en una clase. Una clase determina la estructura base de las propiedades comunes que deben contener todos los esquemas basados en esa clase, así como los grupos de campos de esquema que pueden utilizarse en esos esquemas. Además, la clase de un esquema determina los aspectos de comportamiento de los datos que contendrá un esquema, de los cuales hay dos tipos:

* **[!UICONTROL Registro]**: proporciona información sobre los atributos de un asunto. Un sujeto podría ser una organización o un individuo.
* **[!UICONTROL Serie temporal]**: proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

>[!NOTE]
>
>Para obtener más información sobre las clases de comportamientos de datos en términos de cómo afectan a la composición de esquemas, consulte los [conceptos básicos de la composición de esquemas](../schema/composition.md).

El extremo `/classes` de la API [!DNL Schema Registry] le permite administrar clases mediante programación dentro de la aplicación de experiencia.

## Introducción

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de clases {#list}

Puede enumerar todas las clases bajo el contenedor `global` o `tenant` realizando una solicitud de GET a `/global/classes` o `/tenant/classes`, respectivamente.

>[!NOTE]
>
>Al enumerar recursos, el Registro de esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos que superen este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato de API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor del que desea recuperar las clases: `global` para las clases creadas mediante Adobe o `tenant` para las clases propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte el [documento del apéndice](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista de clases del contenedor `tenant`, utilizando un parámetro de consulta `orderby` para ordenar las clases por su atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para enumerar clases:

| `Accept` encabezado | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para enumerar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve la clase JSON completa para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

{style="table-layout:auto"}

**Respuesta**

La solicitud anterior utilizó el encabezado `application/vnd.adobe.xed-id+json` `Accept`, por lo que la respuesta incluye solo los atributos `title`, `$id`, `meta:altId` y `version` para cada clase. Al usar el otro encabezado `Accept` (`application/vnd.adobe.xed+json`) se devuelven todos los atributos de cada clase. Seleccione el encabezado `Accept` apropiado según la información que necesite en la respuesta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Búsqueda de una clase {#lookup}

Puede buscar una clase específica incluyendo el ID de la clase en la ruta de una petición GET.

**Formato de API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que aloja la clase que desea recuperar: `global` para una clase creada por el Adobe o `tenant` para una clase propiedad de su organización. |
| `{CLASS_ID}` | `meta:altId` o `$id` con codificación de dirección URL de la clase que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una clase por su valor `meta:altId` proporcionado en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Todas las solicitudes de búsqueda requieren que se incluya un `version` en el encabezado `Accept`. Los siguientes `Accept` encabezados están disponibles:

| `Accept` encabezado | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Sin procesar con `$ref` y `allOf`, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` y `allOf` resueltos, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version=1` | Sin procesar con `$ref` y `allOf`, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` y `allOf` resueltos, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` y `allOf` resueltos, se incluyen descriptores. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la clase. Los campos que se devuelven dependen del encabezado `Accept` enviado en la solicitud. Experimente con diferentes encabezados `Accept` para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{ORG_ID}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Crear una clase {#create}

Puede definir una clase personalizada bajo el contenedor `tenant` realizando una solicitud de POST.

>[!IMPORTANT]
>
>Al maquetar un esquema basado en una clase personalizada que haya definido, no podrá utilizar grupos de campos estándar. Cada grupo de campos define las clases con las que son compatibles en su atributo `meta:intendedToExtend`. Una vez que comience a definir grupos de campos compatibles con la nueva clase (utilizando `$id` de la nueva clase en el campo `meta:intendedToExtend` del grupo de campos), podrá volver a utilizar esos grupos de campos cada vez que defina un esquema que implemente la clase definida. Consulte las secciones sobre [creación de grupos de campos](./field-groups.md#create) y [creación de esquemas](./schemas.md#create) en sus respectivas guías de extremos para obtener más información.
>
>Si planea utilizar esquemas basados en clases personalizadas en el Perfil del cliente en tiempo real, también es importante tener en cuenta que los esquemas de unión solo se construyen en función de esquemas que comparten la misma clase. Si desea incluir un esquema de clase personalizada en la unión para otra clase como [!UICONTROL XDM Individual Profile] o [!UICONTROL XDM ExperienceEvent], debe establecer una relación con otro esquema que emplee esa clase. Consulte el tutorial sobre [establecimiento de una relación entre dos esquemas en la API](../tutorials/relationship-api.md) para obtener más información.

**Formato de API**

```http
POST /tenant/classes
```

**Solicitud**

La solicitud para crear (POST) una clase debe incluir un atributo `allOf` que contenga un `$ref` a uno de los dos valores: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Estos valores representan el comportamiento en el que se basa la clase (registro o serie temporal, respectivamente). Para obtener más información sobre las diferencias entre los datos de registro y los datos de series temporales, consulte la sección sobre tipos de comportamiento dentro de los [conceptos básicos de la composición de esquemas](../schema/composition.md).

Al definir una clase, también puede incluir grupos de campos o campos personalizados dentro de la definición de clase. Esto haría que los grupos de campos y campos agregados se incluyeran en todos los esquemas que implementan la clase. La siguiente solicitud de ejemplo define una clase denominada &quot;Propiedad&quot;, que captura información sobre diferentes propiedades propiedad de una compañía y administradas por ella. Incluye un campo `propertyId` que se debe incluir cada vez que se utiliza la clase.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | Espacio de nombres `TENANT_ID` para su organización. Todos los recursos creados por su organización deben incluir esta propiedad para evitar conflictos con otros recursos en [!DNL Schema Registry]. |
| `allOf` | Lista de recursos cuyas propiedades va a heredar la nueva clase. Uno de los objetos `$ref` de la matriz define el comportamiento de la clase. En este ejemplo, la clase hereda el comportamiento &quot;record&quot;. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles de la clase recién creada, incluidos `$id`, `meta:altId` y `version`. Estos tres valores son de sólo lectura y los asigna el [!DNL Schema Registry].

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
  "imsOrg": "{ORG_ID}",
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

Al realizar una solicitud de GET para [enumerar todas las clases](#list) en el contenedor `tenant`, ahora se incluiría la clase Property. También puede [realizar una solicitud de búsqueda (GET)](#lookup) con la dirección URL codificada `$id` para ver la nueva clase directamente.

## Actualización de una clase {#put}

Puede reemplazar una clase completa mediante una operación de PUT, básicamente reescribiendo el recurso. Al actualizar una clase mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios al [crear una nueva clase](#create) en una solicitud de POST.

>[!NOTE]
>
>Si solo desea actualizar parte de una clase en lugar de reemplazarla por completo, consulte la sección sobre [actualizar una parte de una clase](#patch).

**Formato de API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | `meta:altId` o `$id` con codificación URL de la clase que desea volver a escribir. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud reescribe una clase existente, cambiando su `description` y el `title` de uno de sus campos.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
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
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
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

**Respuesta**

Una respuesta correcta devuelve los detalles de la clase actualizada.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
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
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
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
  "imsOrg": "{ORG_ID}",
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

## Actualizar una parte de una clase {#patch}

Puede actualizar una parte de una clase mediante una solicitud de PATCH. [!DNL Schema Registry] admite todas las operaciones de parche de JSON estándar, incluidas `add`, `remove` y `replace`. Para obtener más información sobre el parche JSON, consulte la [guía de aspectos básicos de la API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con valores nuevos en lugar de actualizar campos individuales, vea la sección sobre [reemplazo de una clase mediante una operación de PUT](#put).

**Formato de API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El URI `$id` con codificación URL o `meta:altId` de la clase que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente actualiza `description` de una clase existente y `title` de uno de sus campos.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), en qué campo se debe realizar la operación (`path`) y qué información se debe incluir en esa operación (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Respuesta**

La respuesta muestra que ambas operaciones se realizaron correctamente. Se ha actualizado `description`, junto con `title` del campo `propertyId`.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
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
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
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
  "imsOrg": "{ORG_ID}",
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

## Eliminación de una clase {#delete}

En ocasiones puede ser necesario quitar una clase del Registro de esquemas. Esto se realiza realizando una solicitud de DELETE con el ID de clase proporcionado en la ruta.

**Formato de API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El URI `$id` con codificación URL o `meta:altId` de la clase que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar la eliminación, intente una [solicitud de búsqueda (GET)](#lookup) para la clase. Deberá incluir un encabezado `Accept` en la solicitud, pero debería recibir el estado HTTP 404 (no encontrado) porque la clase se ha eliminado del Registro de esquemas.
