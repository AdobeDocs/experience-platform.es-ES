---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;esquema;esquema;esquemas;esquemas;crear esquemas
solution: Experience Platform
title: Punto final de API de Esquemas
description: El extremo /schemas de la API del Registro de esquemas le permite administrar mediante programación esquemas XDM dentro de la aplicación de experiencia.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 2%

---

# Punto final de esquemas

Un esquema se puede considerar como el modelo para los datos que desea introducir en Adobe Experience Platform. Cada esquema está compuesto por una clase y cero o más mezclas. El extremo `/schemas` de la API [!DNL Schema Registry] le permite administrar esquemas mediante programación dentro de la aplicación de experiencia.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de esquemas {#list}

Puede enumerar todos los esquemas bajo el contenedor `global` o `tenant` realizando una solicitud de GET a `/global/schemas` o `/tenant/schemas`, respectivamente.

>[!NOTE]
>
>Al enumerar recursos, el Registro de esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos más allá de este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato de API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que alberga los esquemas que desea recuperar: `global` para esquemas creados por Adobe o `tenant` para esquemas propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales para filtrar los resultados por. Consulte el [apéndice document](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

**Solicitud**

La siguiente solicitud recupera una lista de esquemas del contenedor `tenant`, utilizando un parámetro de consulta `orderby` para ordenar los resultados por su atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes encabezados `Accept` están disponibles para enumerar esquemas:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para listar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el esquema JSON completo para cada recurso, con los valores originales `$ref` y `allOf` incluidos. (Límite: 300) |

**Respuesta**

La solicitud anterior utilizaba el encabezado `application/vnd.adobe.xed-id+json` `Accept`, por lo que la respuesta incluye solo los atributos `title`, `$id`, `meta:altId` y `version` para cada esquema. El uso del otro encabezado `Accept` (`application/vnd.adobe.xed+json`) devuelve todos los atributos de cada esquema. Seleccione el encabezado `Accept` correspondiente en función de la información que necesite en su respuesta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Buscar un esquema {#lookup}

Puede buscar un esquema específico realizando una solicitud de GET que incluya el ID del esquema en la ruta.

**Formato de API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que alberga el esquema que desea recuperar: `global` para un esquema creado por el Adobe o `tenant` para un esquema propiedad de su organización. |
| `{SCHEMA_ID}` | El `meta:altId` o el `$id` con codificación de URL del esquema que desea buscar. |

**Solicitud**

La siguiente solicitud recupera un esquema especificado por su valor `meta:altId` en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Todas las solicitudes de búsqueda requieren que se incluya `version` en el encabezado `Accept`. Los siguientes encabezados `Accept` están disponibles:

| `Accept` header | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Sin procesar con `$ref` y `allOf`, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` y  `allOf` resuelto, tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version=1` | Sin procesar con `$ref` y `allOf`, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` y  `allOf` resuelto, sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` y  `allOf` resueltos, incluidos los descriptores. |

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema. Los campos devueltos dependen del encabezado `Accept` enviado en la solicitud. Experimente con diferentes encabezados `Accept` para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Crear un esquema {#create}

El proceso de composición del esquema comienza asignando una clase. La clase define los aspectos de comportamiento clave de los datos (registro o serie temporal), así como los campos mínimos necesarios para describir los datos que se van a introducir.

>[!NOTE]
>
>La llamada de ejemplo siguiente es solo un ejemplo básico de cómo crear un esquema en la API, con los requisitos de composición mínimos de una clase y sin mezclas. Para ver los pasos completos sobre cómo crear un esquema en la API, incluido cómo asignar campos mediante mezclas y tipos de datos, consulte el [tutorial de creación de esquemas](../tutorials/create-schema-api.md).

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La solicitud debe incluir un atributo `allOf` que haga referencia al `$id` de una clase. Este atributo define la &quot;clase base&quot; que implementará el esquema. En este ejemplo, la clase base es una clase &quot;Información de propiedad&quot; que se creó anteriormente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `allOf` | Matriz de objetos, con cada objeto haciendo referencia a una clase o mezcla en cuyos campos implementa el esquema. Cada objeto contiene una sola propiedad (`$ref`) cuyo valor representa el `$id` de la clase o mezcla que implementará el nuevo esquema. Debe proporcionarse una clase, con cero o más mezclas adicionales. En el ejemplo anterior, el objeto único de la matriz `allOf` es la clase del esquema. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del esquema recién creado, incluidos `$id`, `meta:altId` y `version`. Estos valores son de solo lectura y los asigna el [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Al realizar una solicitud de GET a [list all schemas](#list) en el contenedor de inquilinos, ahora se incluiría el nuevo esquema. Puede realizar una solicitud de [búsqueda (GET)](#lookup) utilizando el URI `$id` con codificación URL para ver el nuevo esquema directamente.

Para agregar campos adicionales a un esquema, puede realizar una operación [PATCH](#patch) para agregar mezclas a las matrices `allOf` y `meta:extends` del esquema.

## Actualizar un esquema {#put}

Puede reemplazar un esquema completo mediante una operación de PUT, lo que básicamente es volver a escribir el recurso. Al actualizar un esquema a través de una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios cuando [cree un nuevo esquema](#create) en una solicitud de POST.

>[!NOTE]
>
>Si solo desea actualizar parte de un esquema en lugar de reemplazarlo por completo, consulte la sección [actualización de una parte de un esquema](#patch).

**Formato de API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El `meta:altId` o el `$id` con codificación de URL del esquema que desea reescribir. |

**Solicitud**

La siguiente solicitud reemplaza un esquema existente y cambia sus atributos `title`, `description` y `allOf`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Actualizar una parte de un esquema {#patch}

Puede actualizar una parte de un esquema mediante una solicitud de PATCH. El [!DNL Schema Registry] es compatible con todas las operaciones de parches de JSON estándar, incluidas `add`, `remove` y `replace`. Para obtener más información sobre JSON Patch, consulte la [guía de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con valores nuevos en lugar de actualizar campos individuales, consulte la sección sobre [reemplazar un esquema con una operación de PUT](#put).

Una de las operaciones de PATCH más comunes implica añadir mezclas previamente definidas a un esquema, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El URI `$id` con codificación URL o `meta:altId` del esquema que desea actualizar. |

**Solicitud**

La solicitud de ejemplo siguiente agrega una nueva mezcla a un esquema añadiendo el valor `$id` de la mezcla a las matrices `meta:extends` y `allOf`.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), en qué campo se debe realizar la operación (`path`) y qué información se debe incluir en esa operación (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Respuesta**

La respuesta muestra que ambas operaciones se realizaron correctamente. La mezcla `$id` se ha añadido a la matriz `meta:extends` y ahora aparece una referencia (`$ref`) a la mezcla `$id` en la matriz `allOf`.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Habilitar un esquema para utilizarlo en el perfil de cliente en tiempo real {#union}

Para que un esquema participe en [Perfil del cliente en tiempo real](../../profile/home.md), debe agregar una etiqueta `union` a la matriz `meta:immutableTags` del esquema. Puede hacerlo realizando una solicitud de PATCH para el esquema en cuestión.

>[!IMPORTANT]
>
>Las etiquetas inmutables son etiquetas que se pretende establecer, pero que nunca se eliminan.

**Formato de API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El URI `$id` con codificación URL o `meta:altId` del esquema que desea habilitar. |

**Solicitud**

La solicitud de ejemplo siguiente agrega una matriz `meta:immutableTags` a un esquema existente, dando a la matriz un valor de cadena único de `union` para habilitarla para su uso en el perfil.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado, mostrando que se ha agregado la matriz `meta:immutableTags`.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

Ahora puede ver la unión de la clase de este esquema para confirmar que se representan los campos del esquema. Consulte la [guía de extremo de unión](./unions.md) para obtener más información.

## Eliminar un esquema {#delete}

Ocasionalmente puede ser necesario eliminar un esquema del Registro de esquemas. Esto se realiza realizando una solicitud de DELETE con el ID de esquema proporcionado en la ruta.

**Formato de API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El URI `$id` con codificación URL o `meta:altId` del esquema que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) al esquema. Deberá incluir un encabezado `Accept` en la solicitud, pero debe recibir un estado HTTP 404 (No encontrado) porque el esquema se ha eliminado del Registro de esquemas.
