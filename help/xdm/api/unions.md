---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;Registro de esquemas;Registro de Esquemas;unión;Unión;uniones;Uniones;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Extremo de la API de uniones
description: El extremo /uniones de la API del Registro de Esquema permite administrar mediante programación esquemas de unión XDM en la aplicación de experiencia.
topic: developer guide
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 1%

---


# Extremo de uniones

Las uniones (o vistas de unión) son esquemas de sólo lectura generados por el sistema que acumulados los campos de todos los esquemas que comparten la misma clase ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) y están habilitados para [[!DNL Real-time Customer Profile]](../../profile/home.md).

Este documento cubre conceptos esenciales para trabajar con uniones en la API del Registro de Esquemas, incluidas las llamadas de muestra para diversas operaciones. Para obtener información más general sobre uniones en XDM, consulte la sección sobre uniones en los [conceptos básicos de la composición de esquema](../schema/composition.md#union).

## Campos de esquema de unión

El [!DNL Schema Registry] incluye automáticamente tres campos clave dentro de un esquema de unión: `identityMap`, `timeSeriesEvents` y `segmentMembership`.

### Mapa de identidad

Un esquema de unión `identityMap` es una representación de las identidades conocidas dentro de los esquemas de registros asociados de la unión. El mapa de identidad separa las identidades en diferentes matrices con clave de Área de nombres. Cada identidad enumerada es un objeto que contiene un valor único `id`. Consulte la [documentación del servicio de identidad](../../identity-service/home.md) para obtener más información.

### Eventos de series temporales

La matriz `timeSeriesEvents` es una lista de eventos de series temporales que se relacionan con los esquemas de registros asociados con la unión. Cuando se exportan datos de perfil a conjuntos de datos, esta matriz se incluye para cada registro. Esto resulta útil en varios casos de uso, como el aprendizaje automático, en el que los modelos necesitan un historial de comportamiento completo de un perfil además de sus atributos de registro.

### Mapa de pertenencia a segmentos

El mapa `segmentMembership` almacena los resultados de las evaluaciones de segmentos. Cuando los trabajos de segmentos se ejecutan correctamente mediante la [API de segmentación](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), se actualiza el mapa. `segmentMembership` también almacena todos los segmentos de audiencia preevaluados que se ingieren en la plataforma, lo que permite la integración con otras soluciones como Adobe Audience Manager. Consulte el tutorial sobre [creación de segmentos mediante API](../../segmentation/tutorials/create-a-segment.md) para obtener más información.

## Recuperar una lista de uniones {#list}

Cuando se establece la etiqueta `union` en un esquema, [!DNL Schema Registry] agrega automáticamente el esquema a la unión de la clase en la que se basa el esquema. Si no existe ninguna unión para la clase en cuestión, se crea automáticamente una nueva unión. El `$id` de la unión es similar al `$id` estándar de otros [!DNL Schema Registry] recursos, con la única diferencia que se anexa con dos guiones bajos y la palabra &quot;unión&quot; (`__union`).

Puede realizar la vista de una lista de uniones disponibles haciendo una solicitud de GET al extremo `/tenant/unions`.

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

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para las uniones de listado:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Éste es el encabezado recomendado para enumerar los recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve la clase JSON completa para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y una matriz `results` en el cuerpo de la respuesta. Si se han definido uniones, los detalles de cada unión se proporcionan como objetos dentro de la matriz. Si no se ha definido ninguna unión, se devuelve el estado HTTP 200 (OK) pero la matriz `results` estará vacía.

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

## Buscar una unión {#lookup}

Puede realizar una vista de una unión específica realizando una solicitud de GET que incluya `$id` y, según el encabezado Accept, algunos o todos los detalles de la unión.

>[!NOTE]
>
>Las búsquedas de uniones están disponibles mediante el extremo `/unions` y `/schemas` para habilitarlas para usarlas en exportaciones [!DNL Profile] en un conjunto de datos.

**Formato API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{UNION_ID}` | El URI `$id` con codificación URL de la unión que desea buscar. Los URI para esquemas de unión se anexan con &quot;__unión&quot;. |

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

Las solicitudes de búsqueda de uniones requieren que se incluya `version` en el encabezado Accept.

Los siguientes encabezados Accept están disponibles para las búsquedas de esquemas de unión:

| Accept | Descripción |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Sin procesar con `$ref` y `allOf`. Incluye títulos y descripciones. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` atributos y  `allOf` resueltos. Incluye títulos y descripciones. |

**Respuesta**

Una respuesta correcta devuelve la vista de unión de todos los esquemas que implementan la clase cuyo `$id` se proporcionó en la ruta de solicitud.

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

## Habilitar un esquema para la pertenencia a uniones {#enable}

Para que un esquema se incluya en la unión de su clase, se debe agregar una etiqueta `union` al atributo `meta:immutableTags` del esquema. Esto se puede lograr haciendo una solicitud de PATCH para agregar una matriz `meta:immutableTags` con un valor de cadena único `union` al esquema en cuestión. Consulte la guía del extremo [esquemas](./schemas.md#union) para ver un ejemplo detallado.

## Esquemas de lista en una unión {#list-schemas}

Para ver qué esquemas forman parte de una unión específica, puede realizar una solicitud de GET al extremo `/tenant/schemas`. Mediante el parámetro de consulta `property`, puede configurar la respuesta para que solo devuelva esquemas que contengan un campo `meta:immutableTags` y un `meta:class` igual a la clase a la que accede la unión.

**Formato de API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{CLASS_ID}` | El `$id` de la clase cuyos esquemas habilitados para uniones desea realizar la lista. |

**Solicitud**

La siguiente solicitud recupera una lista de todos los esquemas que forman parte de la unión para la clase [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Los siguientes `Accept` encabezados están disponibles para los esquemas de listado:

| `Accept` header | Descripción |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Devuelve un breve resumen de cada recurso. Éste es el encabezado recomendado para enumerar los recursos. (Límite: 300) |
| `application/vnd.adobe.xed+json` | Devuelve el esquema JSON completo para cada recurso, con `$ref` y `allOf` originales incluidos. (Límite: 300) |

**Respuesta**

Una respuesta correcta devuelve una lista filtrada de esquemas, que contiene solo aquellos que pertenecen a la clase especificada y que se han habilitado para la pertenencia a la unión. Recuerde que cuando se utilizan varios parámetros de consulta, se asume una relación Y.

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
