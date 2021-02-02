---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de clases;Registro de Esquemas;clase;clase;clases;clases;crear
solution: Experience Platform
title: Crear una clase
description: El extremo /classes de la API del Registro de Esquema permite administrar mediante programación clases XDM dentro de la aplicación de experiencia.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---


# Extremo de clases

Todos los esquemas del Modelo de datos de experiencia (XDM) deben basarse en una clase. Una clase determina la estructura base de las propiedades comunes que deben contener todos los esquemas basados en esa clase, así como las mezclas que pueden utilizarse en esos esquemas. Además, una clase de esquema determina los aspectos de comportamiento de los datos que contendrá un esquema, de los cuales hay dos tipos:

* **[!UICONTROL Registro]**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **[!UICONTROL Serie]** temporal: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

>[!NOTE]
>
>Para obtener más información sobre las clases de comportamiento de datos en cuanto a cómo afectan a la composición de esquemas, consulte los [conceptos básicos de la composición de esquemas](../schema/composition.md).

El extremo `/classes` de la API [!DNL Schema Registry] le permite administrar clases mediante programación dentro de la aplicación de experiencia.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas exitosas a cualquier API de Experience Platform.

## Recuperar una lista de clases {#list}

Puede realizar la lista de todas las clases bajo el contenedor `global` o `tenant` haciendo una solicitud de GET a `/global/classes` o `/tenant/classes`, respectivamente.

>[!NOTE]
>
>Al enumerar los recursos, el Registro de Esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos más allá de este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor desde el que desea recuperar las clases: `global` para clases creadas por Adobe o `tenant` para clases propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales para filtrar los resultados. Consulte el [documento del apéndice](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

**Solicitud**

La siguiente solicitud recupera una lista de clases del contenedor `tenant`, mediante un parámetro de consulta `orderby` para ordenar las clases por su atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para las clases de listado:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Éste es el encabezado recomendado para enumerar los recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve la clase JSON completa para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

**Respuesta**

En la solicitud anterior se utilizó el encabezado `application/vnd.adobe.xed-id+json` `Accept`, por lo que la respuesta sólo incluye los atributos `title`, `$id`, `meta:altId` y `version` para cada clase. El uso del otro encabezado `Accept` (`application/vnd.adobe.xed+json`) devuelve todos los atributos de cada clase. Seleccione el encabezado `Accept` correspondiente en función de la información que necesite en la respuesta.

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

## Buscar una clase {#lookup}

Puede buscar una clase específica incluyendo el ID de la clase en la ruta de una solicitud de GET.

**Formato API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que aloja la clase que desea recuperar: `global` para una clase creada por Adobe o `tenant` para una clase propiedad de su organización. |
| `{CLASS_ID}` | El `meta:altId` o el `$id` con codificación URL de la clase que desea buscar. |

**Solicitud**

La siguiente solicitud recupera una clase por su valor `meta:altId` proporcionado en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

Una respuesta correcta devuelve los detalles de la clase. Los campos devueltos dependen del encabezado `Accept` enviado en la solicitud. Experimente con diferentes `Accept` encabezados para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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
  "imsOrg":"{IMS_ORG}",
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

Puede definir una clase personalizada en el contenedor `tenant` realizando una solicitud de POST.

>[!IMPORTANT]
>
>Al componer un esquema basado en una clase personalizada que usted defina, no podrá utilizar mezclas estándar. Cada mezcla define las clases con las que son compatibles en su atributo `meta:intendedToExtend`. Una vez que comience a definir mezclas compatibles con la nueva clase (utilizando la `$id` de la nueva clase en el campo `meta:intendedToExtend` de la mezcla), podrá reutilizar esas mezclas cada vez que defina un esquema que implemente la clase que haya definido. Consulte las secciones sobre [creación de mezclas](./mixins.md#create) y [creación de esquemas](./schemas.md#create) en sus respectivas guías de punto final para obtener más información.
>
>Si planea utilizar esquemas basados en clases personalizadas en el Perfil del cliente en tiempo real, también es importante tener en cuenta que los esquemas de unión solo se construyen en función de esquemas que comparten la misma clase. Si desea incluir un esquema de clase personalizada en la unión de otra clase como [!UICONTROL Perfil individual XDM] o [!UICONTROL evento de experiencia XDM], debe establecer una relación con otro esquema que emplee esa clase. Consulte el tutorial sobre [establecimiento de una relación entre dos esquemas en la API](../tutorials/relationship-api.md) para obtener más información.

**Formato API**

```http
POST /tenant/classes
```

**Solicitud**

La solicitud para crear (POST) una clase debe incluir un atributo `allOf` que contenga `$ref` en uno de los dos valores: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Estos valores representan el comportamiento en el que se basa la clase (registro o serie temporal, respectivamente). Para obtener más información sobre las diferencias entre los datos de registros y los datos de series temporales, consulte la sección sobre tipos de comportamiento dentro de los [conceptos básicos de la composición de esquemas](../schema/composition.md).

Al definir una clase, también puede incluir mezclas o campos personalizados en la definición de clase. Esto haría que las mezclas y campos agregados se incluyeran en todos los esquemas que implementan la clase. La siguiente solicitud de ejemplo define una clase llamada &quot;Property&quot;, que captura información sobre diferentes propiedades que son propiedad de una compañía y que son operadas por ella. Incluye un campo `propertyId` que se incluirá cada vez que se utilice la clase.

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
| `_{TENANT_ID}` | La Área de nombres `TENANT_ID` para su organización. Todos los recursos creados por su organización deben incluir esta propiedad para evitar conflictos con otros recursos en [!DNL Schema Registry]. |
| `allOf` | Lista de recursos cuyas propiedades van a heredar la nueva clase. Uno de los objetos `$ref` dentro de la matriz define el comportamiento de la clase. En este ejemplo, la clase hereda el comportamiento &quot;record&quot;. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles de la clase recién creada, incluidos los `$id`, `meta:altId` y `version`. Estos tres valores son de sólo lectura y son asignados por [!DNL Schema Registry].

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

Al realizar una solicitud de GET a [lista de todas las clases](#list) en el contenedor `tenant`, ahora se incluiría la clase Property. También puede [realizar una solicitud de búsqueda (GET)](#lookup) mediante la vista de la nueva clase `$id` con codificación URL.

## Actualizar una clase {#put}

Puede reemplazar una clase completa mediante una operación de PUT, lo que básicamente es volver a escribir el recurso. Al actualizar una clase mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios cuando [cree una nueva clase](#create) en una solicitud de POST.

>[!NOTE]
>
>Si solo desea actualizar parte de una clase en lugar de reemplazarla por completo, consulte la sección sobre [actualización de una parte de una clase](#patch).

**Formato API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El `meta:altId` o el `$id` con codificación URL de la clase que desea volver a escribir. |

**Solicitud**

La siguiente solicitud vuelve a escribir una clase existente, cambiando su `description` y el `title` de uno de sus campos.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Actualizar una parte de una clase {#patch}

Puede actualizar una parte de una clase mediante una solicitud de PATCH. El [!DNL Schema Registry] soporta todas las operaciones estándar de parche JSON, incluyendo `add`, `remove` y `replace`. Para obtener más información sobre JSON Patch, consulte la [guía de principios de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con nuevos valores en lugar de actualizar campos individuales, consulte la sección sobre [reemplazo de una clase mediante una operación de PUT](#put).

**Formato API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El URI `$id` con codificación URL o `meta:altId` de la clase que desea actualizar. |

**Solicitud**

La solicitud de ejemplo siguiente actualiza el `description` de una clase existente y el `title` de uno de sus campos.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), el campo en el que se debe realizar la operación (`path`) y la información que se debe incluir en esa operación (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Respuesta**

La respuesta muestra que ambas operaciones se realizaron correctamente. El `description` se ha actualizado, junto con el `title` del campo `propertyId`.

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

## Eliminar una clase {#delete}

En ocasiones puede ser necesario eliminar una clase del Registro de Esquemas. Esto se realiza realizando una solicitud de DELETE con el ID de clase proporcionado en la ruta.

**Formato API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El URI `$id` con codificación URL o `meta:altId` de la clase que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar la eliminación, intente una solicitud de [búsqueda (GET)](#lookup) para la clase. Deberá incluir un encabezado `Accept` en la solicitud, pero debe recibir un estado HTTP 404 (no encontrado) porque la clase se ha eliminado del Registro de Esquemas.