---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;esquema;esquemas;esquemas;crear
solution: Experience Platform
title: Extremo de API de esquemas
description: El extremo /schemas de la API de Registro de esquemas le permite administrar mediante programación esquemas XDM dentro de la aplicación de experiencia.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 974faad835b5dc2a4d47249bb672573dfb4d54bd
workflow-type: tm+mt
source-wordcount: '2095'
ht-degree: 4%

---

# Extremo de esquemas

Un esquema se puede considerar como el modelo para los datos que desea introducir en Adobe Experience Platform. Cada esquema está compuesto por una clase y cero o más grupos de campos de esquema. El extremo `/schemas` de la API [!DNL Schema Registry] le permite administrar mediante programación esquemas dentro de la aplicación de experiencia.

## Introducción

El extremo de API utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de esquemas {#list}

Puede enumerar todos los esquemas bajo el contenedor `global` o `tenant` realizando una petición GET a `/global/schemas` o `/tenant/schemas`, respectivamente.

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
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte el [documento del apéndice](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista de esquemas del contenedor `tenant`, con un parámetro de consulta `orderby` para ordenar los resultados por su atributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para enumerar esquemas:

| `Accept` encabezado | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para enumerar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el esquema JSON completo para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

{style="table-layout:auto"}

**Respuesta**

La solicitud anterior utilizó el encabezado `application/vnd.adobe.xed-id+json` `Accept`, por lo que la respuesta solo incluye los atributos `title`, `$id`, `meta:altId` y `version` para cada esquema. Al usar el otro encabezado `Accept` (`application/vnd.adobe.xed+json`) se devuelven todos los atributos de cada esquema. Seleccione el encabezado `Accept` apropiado según la información que necesite en la respuesta.

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

Puede buscar un esquema específico realizando una petición GET que incluya el ID del esquema en la ruta.

**Formato de API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor que aloja el esquema que desea recuperar: `global` para un esquema creado por Adobe o `tenant` para un esquema propiedad de su organización. |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codificación de dirección URL del esquema que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera un esquema especificado por su valor `meta:altId` en la ruta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` y `allOf` resueltos, tiene títulos y descripciones. Los campos obsoletos se indican con un atributo `meta:status` de `deprecated`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema. Los campos que se devuelven dependen del encabezado `Accept` enviado en la solicitud. Experimente con diferentes encabezados `Accept` para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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

Para obtener instrucciones sobre cómo crear un esquema sin clases ni grupos de campos, conocido como esquema basado en modelos, vea la sección [Crear un esquema basado en modelos](#create-model-based-schema).

>[!NOTE]
>
>La llamada de ejemplo siguiente es solo un ejemplo de línea de base de cómo crear un esquema en la API, con los requisitos mínimos de composición de una clase y sin grupos de campos. Para ver los pasos completos sobre cómo crear un esquema en la API, incluido cómo asignar campos mediante grupos de campos y tipos de datos, consulte el [tutorial de creación de esquemas](../tutorials/create-schema-api.md).

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La solicitud debe incluir un atributo `allOf` que haga referencia a `$id` de una clase. Este atributo define la &quot;clase base&quot; que implementará el esquema. En este ejemplo, la clase base es una clase &quot;Información de propiedad&quot; creada anteriormente.

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
| `allOf` | Matriz de objetos, cada uno de los cuales hace referencia a una clase o grupo de campos cuyos campos implementa el esquema. Cada objeto contiene una sola propiedad (`$ref`) cuyo valor representa el `$id` de la clase o grupo de campos que implementará el nuevo esquema. Se debe proporcionar una clase con cero o más grupos de campos adicionales. En el ejemplo anterior, el objeto único de la matriz `allOf` es la clase del esquema. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y una carga útil que contiene los detalles del esquema recién creado, incluidos `$id`, `meta:altId` y `version`. Estos valores son de sólo lectura y los asigna el [!DNL Schema Registry].

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

Al realizar una petición GET para [enumerar todos los esquemas](#list) en el contenedor de inquilino, ahora se incluiría el nuevo esquema. Puede realizar una [solicitud de búsqueda (GET)](#lookup) usando el URI `$id` con codificación de dirección URL para ver el nuevo esquema directamente.

Para agregar campos adicionales a un esquema, puede realizar una [operación de PATCH](#patch) para agregar grupos de campos a las matrices `allOf` y `meta:extends` del esquema.

## Crear un esquema basado en modelo {#create-model-based-schema}

>[!AVAILABILITY]
>
>Data Mirror y los esquemas basados en modelos están disponibles para los titulares de licencias de **campañas orquestadas** de Adobe Journey Optimizer. También están disponibles como una **versión limitada** para los usuarios de Customer Journey Analytics, según su licencia y la habilitación de características. Póngase en contacto con su representante de Adobe para obtener acceso.

Cree un esquema basado en modelos realizando una petición POST al extremo `/schemas`. Los esquemas basados en modelos almacenan datos de estilo relacional estructurados **sin** clases o grupos de campos. Defina los campos directamente en el esquema e identifique el esquema como basado en modelos mediante una etiqueta de comportamiento lógica.

>[!IMPORTANT]
>
>Para crear un esquema basado en modelos, establezca `meta:extends` en `"https://ns.adobe.com/xdm/data/adhoc-v2"`. Este es un **identificador lógico de comportamiento** (no un comportamiento físico o clase). **no** hace referencia a clases o grupos de campos en `allOf`, y **no** incluye clases o grupos de campos en `meta:extends`.

Cree primero el esquema con `POST /tenant/schemas`. A continuación, agregue los descriptores necesarios con la API de [Descriptores (`POST /tenant/descriptors`)](../api/descriptors.md):

- [Descriptor de clave principal](../api/descriptors.md#primary-key-descriptor): un campo de clave principal debe estar en el **nivel raíz** y **marcado como obligatorio**.
- [Descriptor de versión](../api/descriptors.md#version-descriptor): **Requerido** cuando existe una clave principal.
- [Descriptor de relación](../api/descriptors.md#relationship-descriptor): opcional; define uniones; cardinalidad no impuesta durante la ingesta.
- [Descriptor de marca de tiempo](../api/descriptors.md#timestamp-descriptor): para los esquemas de series de tiempo, la clave principal debe ser una clave **compuesta** que incluya el campo de marca de tiempo.

>[!NOTE]
>
>En el Editor de esquemas de interfaz de usuario, el descriptor de versión y los descriptores de marca de tiempo aparecen como &quot;[ !UICOTRNOL Identificador de versión]&quot; y &quot;[ !UICOTRNOL Identificador de marca de tiempo]&quot; respectivamente.

<!-- >[!AVAILABILITY]
>
>Although `meta:behaviorType` technically accepts `time-series`, support is not currently available for model-based schemas. Set `meta:behaviorType` to `"record"`. -->

>[!CAUTION]
>
>Los esquemas basados en modelos son **no compatibles con los esquemas de unión**. No aplique la etiqueta `union` a `meta:immutableTags` cuando trabaje con esquemas basados en modelos. Esta configuración está bloqueada en la interfaz de usuario, pero la API no la bloquea en este momento. Consulte la [guía de extremo de uniones](./unions.md) para obtener más información sobre el comportamiento del esquema de unión.

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### Solicitar propiedades del cuerpo

| Propiedad | Tipo | Descripción |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | Cadena | Nombre para mostrar del esquema. |
| `description` | Cadena | Breve explicación del propósito del esquema. |
| `type` | Cadena | Debe ser `"object"` para esquemas basados en modelos. |
| `definitions` | Objeto | Contiene los objetos de nivel raíz que definen los campos de esquema. |
| `definitions.<name>.properties` | Objeto | Nombres de campo y tipos de datos. |
| `allOf` | Matriz | Hace referencia a la definición de objeto de nivel raíz (por ejemplo, `#/definitions/marketing_customers`). |
| `meta:extends` | Matriz | Debe incluir `"https://ns.adobe.com/xdm/data/adhoc-v2"` para identificar el esquema como basado en modelos. |
| `meta:behaviorType` | Cadena | Establecido en `"record"`. Use `"time-series"` solo cuando esté habilitado y sea apropiado. |

>[!IMPORTANT]
>
>La evolución del esquema para esquemas basados en modelos sigue las mismas reglas aditivas que los esquemas estándar. Puede añadir nuevos campos con una petición PATCH. Los cambios como cambiar el nombre o eliminar campos solo se permiten si no se han introducido datos en el conjunto de datos.

**Respuesta**

Una solicitud correcta devuelve **HTTP 201 (Created)** y el esquema creado.

>[!NOTE]
>
>Los esquemas basados en modelos no heredan campos predefinidos (por ejemplo, id, timestamp o eventType). Defina todos los campos obligatorios explícitamente en el esquema.

**Respuesta de ejemplo**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### Propiedades del cuerpo de respuesta

| Propiedad | Tipo | Descripción |
| ------------------- | ------ | -------------------------- |
| `$id` | Cadena | La dirección URL única del esquema creado. Se utiliza en llamadas de API posteriores. |
| `meta:altId` | Cadena | Un identificador alternativo para el esquema. |
| `meta:resourceType` | Cadena | El tipo de recurso (siempre `"schemas"`). |
| `version` | Cadena | Una versión de esquema asignada durante la creación. |
| `title` | Cadena | El nombre para mostrar del esquema. |
| `description` | Cadena | Una breve explicación del propósito del esquema. |
| `type` | Cadena | El tipo de esquema. |
| `definitions` | Objeto | Define objetos reutilizables o grupos de campos utilizados en el esquema. Esto generalmente incluye la estructura de datos principal y se hace referencia a ella en la matriz `allOf` para definir la raíz del esquema. |
| `allOf` | Matriz | Especifica el objeto raíz del esquema haciendo referencia a una o varias definiciones (por ejemplo, `#/definitions/marketing_customers`). |
| `meta:extends` | Matriz | Identifica el esquema como basado en modelo (`adhoc-v2`). |
| `meta:behaviorType` | Cadena | Tipo de comportamiento (`record` o `time-series`, cuando está habilitado). |
| `meta:containerId` | Cadena | Contenedor en el que se almacena el esquema (por ejemplo, `tenant`). |

Para agregar campos a un esquema basado en modelos una vez creado, realice una [petición PATCH](#patch). Los esquemas basados en modelos no heredan ni evolucionan automáticamente. Los cambios estructurales como cambiar el nombre o eliminar campos solo se permiten si no se han introducido datos en el conjunto de datos. Una vez que existen los datos, solo se admiten **cambios aditivos** (como agregar nuevos campos).

Puede agregar nuevos campos de nivel raíz (dentro de la definición raíz o de la raíz `properties`), pero no puede quitar, cambiar el nombre ni cambiar el tipo de los campos existentes.

>[!CAUTION]
>
>La evolución del esquema se restringe después de que se inicialice un conjunto de datos con el esquema. Planifique los nombres y tipos de los campos con cuidado de antemano, ya que una vez introducidos los datos, los campos no se pueden eliminar ni modificar.

## Actualización de un esquema {#put}

Puede reemplazar un esquema completo mediante una operación de PUT, básicamente reescribiendo el recurso. Al actualizar un esquema mediante una petición PUT, el cuerpo debe incluir todos los campos que serían necesarios al [crear un nuevo esquema](#create) en una petición POST.

>[!NOTE]
>
>Si solo desea actualizar parte de un esquema en lugar de reemplazarlo por completo, consulte la sección sobre [actualizar una parte de un esquema](#patch).

**Formato de API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codificación URL del esquema que desea volver a escribir. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud reemplaza un esquema existente y cambia sus atributos `title`, `description` y `allOf`.

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

Puede actualizar una parte de un esquema mediante una petición PATCH. [!DNL Schema Registry] admite todas las operaciones de parche de JSON estándar, incluidas `add`, `remove` y `replace`. Para obtener más información sobre el parche JSON, consulte la [guía de aspectos básicos de la API](../../landing/api-fundamentals.md#json-patch).

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
| `{SCHEMA_ID}` | URI `$id` con codificación URL o `meta:altId` del esquema que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente agrega un nuevo grupo de campos a un esquema al agregar el valor `$id` de ese grupo de campos a las matrices `meta:extends` y `allOf`.

El cuerpo de la solicitud adopta la forma de una matriz, y cada objeto de la lista representa un cambio específico en un campo individual. Cada objeto incluye la operación que se va a realizar (`op`), en qué campo se debe realizar la operación (`path`) y qué información se debe incluir en esa operación (`value`).

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

La respuesta muestra que ambas operaciones se realizaron correctamente. El grupo de campos `$id` se ha agregado a la matriz `meta:extends` y ahora aparece una referencia (`$ref`) al grupo de campos `$id` en la matriz `allOf`.

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

Para que un esquema participe en [Perfil del cliente en tiempo real](../../profile/home.md), debe agregar una etiqueta `union` a la matriz `meta:immutableTags` del esquema. Puede hacerlo realizando una petición PATCH para el esquema en cuestión.

>[!IMPORTANT]
>
>Las etiquetas inmutables son etiquetas que se van a configurar, pero que nunca se quitan.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` con codificación URL o `meta:altId` del esquema que desea habilitar. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente agrega una matriz `meta:immutableTags` a un esquema existente, dando a la matriz un valor de cadena único de `union` para habilitarla para su uso en el perfil.

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

Una respuesta correcta devuelve los detalles del esquema actualizado, que muestran que se ha agregado la matriz `meta:immutableTags`.

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

Ahora puede ver la unión de la clase de este esquema para confirmar que se representan los campos del esquema. Consulte la [guía de extremo de uniones](./unions.md) para obtener más información.

## Eliminar un esquema {#delete}

En ocasiones puede ser necesario quitar un esquema del Registro de esquemas. Esto se realiza realizando una petición DELETE con el ID de esquema proporcionado en la ruta.

**Formato de API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` con codificación URL o `meta:altId` del esquema que desea eliminar. |

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

Puede confirmar la eliminación intentando una solicitud de consulta (GET) al esquema. Deberá incluir un encabezado `Accept` en la solicitud, pero debería recibir el estado HTTP 404 (no encontrado) porque el esquema se ha eliminado del Registro de esquemas.
