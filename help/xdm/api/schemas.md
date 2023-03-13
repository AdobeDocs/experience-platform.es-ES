---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;esquema;esquemas;esquemas;crear
solution: Experience Platform
title: Extremo de API de esquemas
description: El extremo /schemas de la API de Registro de esquemas le permite administrar mediante programación esquemas XDM dentro de la aplicación de experiencia.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 3%

---

# Extremo de esquemas

Un esquema se puede considerar como el modelo para los datos que desea introducir en Adobe Experience Platform. Cada esquema está compuesto por una clase y cero o más grupos de campos de esquema. El `/schemas` punto final en la [!DNL Schema Registry] La API permite administrar esquemas mediante programación dentro de la aplicación de experiencia.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte del [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de esquemas {#list}

Puede enumerar todos los esquemas en `global` o `tenant` al realizar una solicitud de GET a `/global/schemas` o `/tenant/schemas`, respectivamente.

>[!NOTE]
>
>Al enumerar recursos, el Registro de esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos que superen este límite, debe utilizar parámetros de paginación. También se recomienda utilizar parámetros de consulta adicionales para filtrar los resultados y reducir el número de recursos devueltos. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) en el documento del apéndice para obtener más información.

**Formato de API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que contiene los esquemas que desea recuperar: `global` para esquemas creados por Adobe o `tenant` para esquemas propiedad de su organización. |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la [documento anexo](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista de esquemas de la `tenant` contenedor, usar un `orderby` parámetro de consulta para ordenar los resultados por su `title` atributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende de la variable `Accept` encabezado enviado en la solicitud. Lo siguiente `Accept` Los encabezados de están disponibles para enumerar esquemas:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para enumerar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el esquema JSON completo para cada recurso, con el original `$ref` y `allOf` incluido. (Límite: 300) |

{style="table-layout:auto"}

**Respuesta**

La solicitud anterior utilizaba el `application/vnd.adobe.xed-id+json` `Accept` encabezado, por lo tanto la respuesta incluye solo el `title`, `$id`, `meta:altId`, y `version` atributos para cada esquema. Uso del otro `Accept` encabezado (`application/vnd.adobe.xed+json`) devuelve todos los atributos de cada esquema. Seleccione el adecuado `Accept` encabezado en función de la información que requiera en su respuesta.

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

## Búsqueda de un esquema {#lookup}

Puede buscar un esquema específico realizando una solicitud de GET que incluya el ID del esquema en la ruta.

**Formato de API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que aloja el esquema que desea recuperar: `global` para un esquema creado con Adobe o `tenant` para un esquema propiedad de su organización. |
| `{SCHEMA_ID}` | El `meta:altId` o con codificación URL `$id` del esquema que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera un esquema especificado por su `meta:altId` en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` y `allOf` resuelto, tiene títulos y descripciones. Los campos obsoletos se indican con una `meta:status` atributo de `deprecated`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema. Los campos que se devuelven dependen del `Accept` encabezado enviado en la solicitud. Experimente con diferentes `Accept` para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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
  "imsOrg": "{ORG_ID}",
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

## Creación de un esquema {#create}

El proceso de composición del esquema comienza asignando una clase. La clase define los aspectos clave de comportamiento de los datos (registro o serie temporal), así como los campos mínimos necesarios para describir los datos que se van a introducir.

>[!NOTE]
>
>La llamada de ejemplo siguiente es solo un ejemplo de línea de base de cómo crear un esquema en la API, con los requisitos mínimos de composición de una clase y sin grupos de campos. Para ver los pasos completos sobre cómo crear un esquema en la API, incluido cómo asignar campos mediante grupos de campos y tipos de datos, consulte la [tutorial de creación de esquemas](../tutorials/create-schema-api.md).

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La solicitud debe incluir un `allOf` atributo que hace referencia a `$id` de una clase. Este atributo define la &quot;clase base&quot; que implementará el esquema. En este ejemplo, la clase base es una clase &quot;Información de propiedad&quot; creada anteriormente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `allOf` | Matriz de objetos, cada uno de los cuales hace referencia a una clase o grupo de campos cuyos campos implementa el esquema. Cada objeto contiene una sola propiedad (`$ref`) cuyo valor representa el `$id` del grupo de campos o clase que implementará el nuevo esquema. Se debe proporcionar una clase con cero o más grupos de campos adicionales. En el ejemplo anterior, el objeto único del `allOf` array es la clase del esquema. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del esquema recién creado, incluido el `$id`, `meta:altId`, y `version`. Estos valores son de solo lectura y los asigna el [!DNL Schema Registry].

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
    "imsOrg": "{ORG_ID}",
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

Realización de una solicitud de GET a [enumerar todos los esquemas](#list) en el contenedor de usuario ahora incluiría el nuevo esquema. Puede realizar una [solicitud de búsqueda (GET)](#lookup) uso de la codificación URL `$id` URI para ver el nuevo esquema directamente.

Para agregar campos adicionales a un esquema, puede realizar una [operación del PATCH](#patch) para agregar grupos de campos al esquema `allOf` y `meta:extends` matrices.

## Actualización de un esquema {#put}

Puede reemplazar un esquema completo mediante una operación de PUT, básicamente reescribiendo el recurso. Al actualizar un esquema mediante una solicitud de PUT, el cuerpo debe incluir todos los campos que serían necesarios al [creación de un nuevo esquema](#create) en una solicitud de POST.

>[!NOTE]
>
>Si solo desea actualizar parte de un esquema en lugar de reemplazarlo por completo, consulte la sección sobre [actualización de una parte de un esquema](#patch).

**Formato de API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El `meta:altId` o con codificación URL `$id` del esquema que desea volver a escribir. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud reemplaza un esquema existente, cambiando su `title`, `description`, y `allOf` atributos.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Puede actualizar una parte de un esquema mediante una solicitud de PATCH. El [!DNL Schema Registry] admite todas las operaciones de parche de JSON estándar, incluidas las siguientes `add`, `remove`, y `replace`. Para obtener más información sobre el parche JSON, consulte la [Guía de aspectos básicos de API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si desea reemplazar un recurso completo con valores nuevos en lugar de actualizar campos individuales, consulte la sección sobre [reemplazo de un esquema mediante una operación de PUT](#put).

Una de las operaciones de PATCH más comunes implica agregar grupos de campos definidos anteriormente a un esquema, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La codificación URL `$id` URI o `meta:altId` del esquema que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente agrega un nuevo grupo de campos a un esquema agregando el de ese grupo de campos `$id` valor para ambos `meta:extends` y `allOf` matrices.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), en qué campo se debe realizar la operación (`path`) y qué información debe incluirse en esa operación (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

La respuesta muestra que ambas operaciones se realizaron correctamente. El grupo de campos `$id` se ha añadido a `meta:extends` matriz y una referencia (`$ref`) al grupo de campos `$id` ahora aparece en la `allOf` matriz.

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
    "imsOrg": "{ORG_ID}",
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

## Habilitar un esquema para utilizarlo en el perfil del cliente en tiempo real {#union}

Para que un esquema participe en [Perfil del cliente en tiempo real](../../profile/home.md), debe agregar un `union` a la etiqueta del esquema `meta:immutableTags` matriz. Puede hacerlo realizando una solicitud de PATCH para el esquema en cuestión.

>[!IMPORTANT]
>
>Las etiquetas inmutables son etiquetas que se van a configurar, pero que nunca se quitan.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La codificación URL `$id` URI o `meta:altId` del esquema que desea activar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente agrega un `meta:immutableTags` a un esquema existente, dando a la matriz un valor de cadena único de `union` para habilitarlo y utilizarlo en el perfil.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve los detalles del esquema actualizado, que muestran que la variable `meta:immutableTags` se ha añadido la matriz.

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
    "imsOrg": "{ORG_ID}",
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

Ahora puede ver la unión de la clase de este esquema para confirmar que se representan los campos del esquema. Consulte la [guía de extremo de union](./unions.md) para obtener más información.

## Eliminación de un esquema {#delete}

En ocasiones puede ser necesario quitar un esquema del Registro de esquemas. Para ello, realice una solicitud de DELETE con el ID de esquema proporcionado en la ruta.

**Formato de API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La codificación URL `$id` URI o `meta:altId` del esquema que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando una solicitud de consulta (GET) al esquema. Deberá incluir un `Accept` en la solicitud, pero debe recibir un estado HTTP 404 (no encontrado) porque el esquema se ha eliminado del Registro de esquemas.
