---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Uniones
topic: developer guide
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# Uniones

Las Uniones (o vistas de unión) son esquemas de sólo lectura generados por el sistema que acumulados los campos de todos los esquemas que comparten la misma clase (XDM ExperienceEvent o XDM Individual Perfil) y están habilitados para el Perfil [del cliente en tiempo](../../profile/home.md)real.

Este documento cubre conceptos esenciales para trabajar con uniones en la API del Registro de Esquemas, incluidas las llamadas de muestra para diversas operaciones. Para obtener información más general sobre uniones en XDM, consulte la sección sobre uniones en los [conceptos básicos de la composición](../schema/composition.md#union)de esquemas.

## Mezclas de Unión

El Registro de Esquemas incluye automáticamente tres mezclas dentro del esquema de unión: `identityMap`, `timeSeriesEvents`, y `segmentMembership`.

### Mapa de identidad

Un esquema de unión `identityMap` es una representación de las identidades conocidas dentro de los esquemas de registro asociados de la unión. El mapa de identidad separa las identidades en diferentes matrices con clave de Área de nombres. Cada identidad enumerada es en sí mismo un objeto que contiene un `id` valor único.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### eventos de series temporales

La `timeSeriesEvents` matriz es una lista de eventos de series temporales que se relacionan con los esquemas de registros asociados a la unión. Cuando se exportan datos de Perfil a conjuntos de datos, esta matriz se incluye para cada registro. Esto resulta útil en varios casos de uso, como el aprendizaje automático, en el que los modelos necesitan un historial de comportamiento completo de un perfil además de sus atributos de registro.

### Mapa de pertenencia a segmentos

El `segmentMembership` mapa almacena los resultados de las evaluaciones de segmentos. Cuando los trabajos de segmentos se ejecutan correctamente mediante la API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)de segmentación, se actualiza el mapa. `segmentMembership` también almacena todos los segmentos de audiencia preevaluados que se ingieren en Platform, lo que permite la integración con otras soluciones como Adobe Audiencia Manager.

Consulte el tutorial sobre la [creación de segmentos mediante API](../../segmentation/tutorials/create-a-segment.md) para obtener más información.

## Habilitar un esquema para la pertenencia a uniones

Para que un esquema se incluya en la vista de unión combinada, se debe añadir la etiqueta &quot;unión&quot; al `meta:immutableTags` atributo del esquema. Esto se realiza mediante una solicitud PATCH para actualizar el esquema y agregar la `meta:immutableTags` matriz con el valor &quot;unión&quot;.

>[!NOTE] Las etiquetas inmutables son etiquetas que se pretenden definir, pero que nunca se eliminan.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El `$id` URI con codificación URL o `meta:altId` del esquema que desea habilitar para su uso en Perfil. |

**Solicitud**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado, que ahora incluye una `meta:immutableTags` matriz que contiene el valor de cadena &quot;unión&quot;.

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
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## uniones de Lista

Cuando se establece la etiqueta &quot;unión&quot; en un esquema, el Registro de Esquemas crea y mantiene automáticamente una unión para la clase en la que se basa el esquema. El `$id` de la unión es similar al estándar `$id` de una clase, con la única diferencia que se anexa con dos caracteres de subrayado y la palabra &quot;unión&quot; (`"__union"`).

Para vista de una lista de uniones disponibles, puede realizar una solicitud GET al `/unions` extremo.

**Formato API**

```http
GET /tenant/unions
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y una `results` matriz en el cuerpo de la respuesta. Si se han definido uniones, `title`, `$id`, `meta:altId`y `version` para cada unión se proporcionan como objetos dentro de la matriz. Si no se ha definido ninguna unión, se devuelve el estado HTTP 200 (OK), pero la matriz `results` estará vacía.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Buscar una unión específica

Puede realizar una vista de una unión específica realizando una solicitud GET que incluya los datos `$id` y, según el encabezado Accept, algunos o todos los detalles de la unión.

>[!NOTE] Las búsquedas de Uniones están disponibles mediante el `/unions` extremo y `/schemas` para habilitarlas para usarlas en las exportaciones de Perfil a un conjunto de datos.

**Formato API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{UNION_ID}` | URI con codificación de URL de la `$id` unión que desea buscar. Los URI para esquemas de unión se anexan con &quot;__unión&quot;. |

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Las solicitudes de búsqueda de Uniones requieren que `version` se incluyan en el encabezado Accept.

Los siguientes encabezados Accept están disponibles para las búsquedas de esquemas de unión:

| Aceptar | Descripción |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Crudo con `$ref` y `allOf`. Incluye títulos y descripciones. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` atributos y `allOf` resueltos. Incluye títulos y descripciones. |

**Respuesta**

Una respuesta correcta devuelve la vista de unión de todos los esquemas que implementan la clase que `$id` se proporcionó en la ruta de solicitud.

El formato de respuesta depende del encabezado Accept enviado en la solicitud. Experimente con diferentes encabezados Accept para comparar las respuestas y determinar qué encabezado es mejor para su caso de uso.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## esquemas de Lista en una unión

Para ver qué esquemas forman parte de una unión específica, puede realizar una solicitud GET utilizando parámetros de consulta para filtrar los esquemas dentro del contenedor del inquilino.

Con el parámetro de `property` consulta, puede configurar la respuesta para que solo devuelva esquemas que contengan un `meta:immutableTags` campo y un `meta:class` igual a la clase a la que accede la unión.

**Formato de API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El `$id` de la clase a la que desea acceder la unión. |

**Solicitud**

La siguiente solicitud busca todos los esquemas que forman parte de la unión de clase de Perfil individual XDM.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista filtrada de esquemas, que contiene solo aquellos que cumplen ambos requisitos. Recuerde que cuando se utilizan varios parámetros de consulta, se asume una relación Y. El formato de la respuesta depende del encabezado Accept enviado en la solicitud.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
