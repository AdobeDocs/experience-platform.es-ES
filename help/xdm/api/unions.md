---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;unión;uniones;uniones;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Extremo de API de uniones
description: El extremo /union de la API de Registro de esquemas le permite administrar mediante programación esquemas de unión XDM en la aplicación de experiencia.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# Extremo de uniones

Las uniones (o vistas de unión) son esquemas de solo lectura generados por el sistema que agregan los campos de todos los esquemas que comparten la misma clase ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) y que están habilitados para [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Este documento cubre conceptos esenciales para trabajar con uniones en la API del Registro de esquemas, incluidas llamadas de ejemplo para varias operaciones. Para obtener información más general acerca de las uniones en XDM, consulte la sección sobre uniones en los [conceptos básicos de la composición de esquemas](../schema/composition.md#union).

## Campos de esquema de unión

[!DNL Schema Registry] incluye automáticamente tres campos clave dentro de un esquema de unión: `identityMap`, `timeSeriesEvents` y `segmentMembership`.

### Mapa de identidad

`identityMap` de un esquema de unión es una representación de las identidades conocidas dentro de los esquemas de registros asociados de la unión. El mapa de identidad separa las identidades en diferentes matrices marcadas por el área de nombres. Cada identidad enumerada es en sí misma un objeto que contiene un valor `id` único. Consulte la [documentación del servicio de identidad](../../identity-service/home.md) para obtener más información.

### Eventos de series de tiempo

La matriz `timeSeriesEvents` es una lista de eventos de series temporales relacionados con los esquemas de registros asociados a la unión. Cuando los datos de perfil se exportan a conjuntos de datos, esta matriz se incluye para cada registro. Esto resulta útil para varios casos de uso, como el aprendizaje automático, en el que los modelos necesitan todo el historial de comportamiento de un perfil, además de sus atributos de registro.

### Mapa de abono de segmento

El mapa `segmentMembership` almacena los resultados de la evaluación de una definición de segmento. Cuando los trabajos de segmentación se ejecutan correctamente mediante la [API de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/), la asignación se actualiza. `segmentMembership` también almacena cualquier audiencia preevaluada que se haya introducido en Experience Platform, lo que permite la integración con otras soluciones como Adobe Audience Manager. Consulte el tutorial sobre [creación de audiencias mediante API](../../segmentation/tutorials/create-a-segment.md) para obtener más información.

## Recuperación de una lista de uniones {#list}

Cuando establece la etiqueta `union` en un esquema, [!DNL Schema Registry] agrega automáticamente el esquema a la unión de la clase en la que se basa el esquema. Si no existe ninguna unión para la clase en cuestión, se crea automáticamente una nueva unión. El `$id` de la unión es similar al estándar `$id` de otros [!DNL Schema Registry] recursos, con la única diferencia de que se anexa mediante dos guiones bajos y la palabra &quot;unión&quot; (`__union`).

Puede ver una lista de uniones disponibles realizando una petición GET al extremo `/tenant/unions`.

**Formato de API**

```http
GET /tenant/unions
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para enumerar uniones:

| `Accept` encabezado | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para enumerar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve la clase JSON completa para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y una matriz `results` en el cuerpo de la respuesta. Si se han definido uniones, los detalles de cada unión se proporcionan como objetos dentro de la matriz. Si no se han definido uniones, se sigue devolviendo el estado HTTP 200 (OK) pero la matriz `results` estará vacía.

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

## Búsqueda de un sindicato {#lookup}

Puede ver una unión específica realizando una petición GET que incluya `$id` y, según el encabezado Aceptar, algunos o todos los detalles de la unión.

>[!NOTE]
>
>Las búsquedas de unión están disponibles mediante los extremos `/unions` y `/schemas` para habilitarlas y usarlas en exportaciones de [!DNL Profile] a un conjunto de datos.

**Formato de API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{UNION_ID}` | URI con codificación URL `$id` de la unión que desea buscar. Los URI de los esquemas de unión se anexan con &quot;__union&quot;. |

{style="table-layout:auto"}

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Las solicitudes de búsqueda de unión requieren que se incluya `version` en el encabezado Aceptar.

Los siguientes encabezados Aceptar están disponibles para las búsquedas de esquema de unión:

| Aceptar | Descripción |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Sin procesar con `$ref` y `allOf`. Incluye títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos y `allOf` resueltos. Incluye títulos y descripciones. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve la vista de unión de todos los esquemas que implementan la clase cuyo `$id` se proporcionó en la ruta de solicitud.

El formato de respuesta depende del encabezado Aceptar enviado en la solicitud. Experimente con diferentes encabezados Aceptar para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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

## Habilitar un esquema para la afiliación a una unión {#enable}

Para que se incluya un esquema en la unión de su clase, se debe agregar una etiqueta `union` al atributo `meta:immutableTags` del esquema. Puede hacerlo realizando una petición PATCH para agregar una matriz `meta:immutableTags` con un solo valor de cadena de `union` al esquema en cuestión. Consulte la [guía de extremo de esquemas](./schemas.md#union) para ver un ejemplo detallado.

## Enumeración de esquemas en una unión {#list-schemas}

Para ver qué esquemas forman parte de una unión específica, puede realizar una petición GET al extremo `/tenant/schemas`. Con el parámetro de consulta `property`, puede configurar la respuesta para que solo devuelva esquemas que contengan un campo `meta:immutableTags` y un `meta:class` igual a la clase a cuya unión está accediendo.

**Formato de API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El `$id` de la clase cuyos esquemas habilitados para unión desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista de todos los esquemas que forman parte de la unión para la clase [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
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

Una respuesta correcta devuelve una lista filtrada de esquemas, que contiene solo los que pertenecen a la clase especificada que se han habilitado para la pertenencia a la unión. Recuerde que cuando se utilizan varios parámetros de consulta, se asume una relación Y.

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
