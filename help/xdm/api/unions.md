---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;unión;unión;uniones;sindicatos;segmentación;pertenencia a segmentos;eventos de series temporales;
solution: Experience Platform
title: Punto final de la API de Unions
description: El extremo /union de la API del Registro de esquemas permite administrar mediante programación esquemas de unión XDM en la aplicación de experiencia.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Punto final de unión

Los sindicatos (o vistas de unión) son esquemas generados por el sistema, de solo lectura que acumulan los campos de todos los esquemas que comparten la misma clase ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) y están activados para [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Este documento cubre conceptos esenciales para trabajar con sindicatos en la API del Registro de esquemas, incluidas llamadas de ejemplo para diversas operaciones. Para obtener información más general sobre los sindicatos en XDM, consulte la sección sobre los sindicatos en la [conceptos básicos de la composición del esquema](../schema/composition.md#union).

## Campos de esquema de unión

La variable [!DNL Schema Registry] incluye automáticamente tres campos clave dentro de un esquema de unión: `identityMap`, `timeSeriesEvents`y `segmentMembership`.

### Mapa de identidad

Un esquema de unión `identityMap` es una representación de las identidades conocidas dentro de los esquemas de registros asociados a la unión. El mapa de identidad separa las identidades en diferentes matrices tecleadas por el área de nombres. Cada identidad enumerada es en sí mismo un objeto que contiene un `id` valor. Consulte la [Documentación del servicio de identidad](../../identity-service/home.md) para obtener más información.

### Eventos de series temporales

La variable `timeSeriesEvents` matriz es una lista de eventos de series temporales relacionados con los esquemas de registros asociados a la unión. Cuando se exportan datos de perfil a conjuntos de datos, esta matriz se incluye para cada registro. Esto resulta útil en varios casos de uso, como el aprendizaje automático en el que los modelos necesitan todo el historial de comportamiento de un perfil, además de sus atributos de registro.

### Mapa de pertenencia a segmentos

La variable `segmentMembership` map almacena los resultados de las evaluaciones de segmentos. Cuando los trabajos de segmentos se ejecutan correctamente usando la variable [API de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/), se actualiza el mapa. `segmentMembership` también almacena todos los segmentos de audiencia preevaluados que se incorporan a Platform, lo que permite la integración con otras soluciones como Adobe Audience Manager. Consulte el tutorial en [creación de segmentos mediante API](../../segmentation/tutorials/create-a-segment.md) para obtener más información.

## Recuperar una lista de uniones {#list}

Al configurar la variable `union` en un esquema, la variable [!DNL Schema Registry] agrega automáticamente el esquema a la unión para la clase en la que se basa el esquema. Si no existe unión para la clase en cuestión, se crea automáticamente una nueva unión. La variable `$id` para la unión es similar al estándar `$id` de otro [!DNL Schema Registry] recursos, con la única diferencia que se añade es con dos guiones bajos y la palabra &quot;unión&quot; (`__union`).

Puede ver una lista de los sindicatos disponibles realizando una solicitud de GET a la `/tenant/unions` punto final.

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

El formato de respuesta depende de la variable `Accept` encabezado enviado en la solicitud. Lo siguiente `Accept` los encabezados están disponibles para listar uniones:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para listar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve la clase JSON completa para cada recurso, con el original `$ref` y `allOf` incluido. (Límite: 300) |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y un `results` en el cuerpo de respuesta. Si se han definido uniones, los detalles de cada unión se proporcionan como objetos dentro de la matriz. Si no se ha definido ninguna unión, el estado HTTP 200 (OK) sigue siendo devuelto, pero la variable `results` la matriz estará vacía.

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

## Buscar un sindicato {#lookup}

Para ver una unión específica, realice una solicitud de GET que incluya la variable `$id` y, según el encabezado Accept, algunos o todos los detalles de la unión.

>[!NOTE]
>
>Las búsquedas de unión están disponibles mediante el `/unions` y `/schemas` para habilitarlos para su uso en [!DNL Profile] exporta a un conjunto de datos.

**Formato de API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{UNION_ID}` | La dirección URL codificada `$id` URI de la unión que desea buscar. Los URI de los esquemas de unión se añaden a &quot;__union&quot;. |

{style=&quot;table-layout:auto&quot;}

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

Las solicitudes de búsqueda de unión requieren un `version` se incluya en el encabezado Accept .

Los siguientes encabezados Accept están disponibles para las búsquedas de esquema de unión:

| Accept | Descripción |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Sin procesar con `$ref` y `allOf`. Incluye títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos y `allOf` resuelto. Incluye títulos y descripciones. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve la vista de unión de todos los esquemas que implementan la clase cuyo `$id` se proporcionó en la ruta de solicitud.

El formato de respuesta depende del encabezado Accept enviado en la solicitud. Experimente con diferentes encabezados Accept para comparar las respuestas y determinar qué encabezado es el mejor para su caso de uso.

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

## Habilitar un esquema para la pertenencia a una unión {#enable}

Para que un esquema se incluya en la unión de su clase, se debe establecer una `union` se debe agregar a la `meta:immutableTags` atributo. Para ello, puede realizar una solicitud de PATCH para agregar un `meta:immutableTags` matriz con un valor de cadena único de `union` al esquema en cuestión. Consulte la [guía de extremo de esquemas](./schemas.md#union) para ver un ejemplo detallado.

## Enumerar esquemas en una unión {#list-schemas}

Para ver qué esquemas forman parte de una unión específica, se puede realizar una solicitud de GET al `/tenant/schemas` punto final. Al usar la variable `property` parámetro de consulta, puede configurar la respuesta para que solo devuelva esquemas que contengan un `meta:immutableTags` campo y `meta:class` igual a la clase a la que accede la unión.

**Formato de API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | La variable `$id` de la clase cuyos esquemas habilitados para la unión desea enumerar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud recupera una lista de todos los esquemas que forman parte de la unión para la [!DNL XDM Individual Profile] Clase .

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende de la variable `Accept` encabezado enviado en la solicitud. Lo siguiente `Accept` los encabezados están disponibles para enumerar esquemas:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Este es el encabezado recomendado para listar recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el esquema JSON completo para cada recurso, con el original `$ref` y `allOf` incluido. (Límite: 300) |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve una lista filtrada de esquemas, que contienen solo aquellos que pertenecen a la clase especificada y que han sido habilitados para la pertenencia a la unión. Recuerde que cuando se utilizan varios parámetros de consulta, se asume una relación AND.

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
