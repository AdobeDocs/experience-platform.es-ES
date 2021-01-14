---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;behavior;behaviour;behaviors;behaviours;
solution: Experience Platform
title: Guía del extremo de comportamientos
description: El extremo /Behaviors de la API del Registro de Esquema permite recuperar todos los comportamientos disponibles en el contenedor global.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# Extremo de comportamientos

En el Modelo de datos de experiencia (XDM), los comportamientos definen la naturaleza de los datos que describe un esquema. Cada clase XDM debe hacer referencia a un comportamiento específico, que heredarán todos los esquemas que empleen esa clase. Para casi todos los casos de uso en la plataforma, hay dos comportamientos disponibles:

* **[!UICONTROL Registro]**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **[!UICONTROL Serie]** temporal: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

>[!NOTE]
>
>Hay algunos casos de uso en Plataforma que requieren el uso de esquema que no emplea ninguno de los comportamientos anteriores. En estos casos, hay disponible un tercer comportamiento &quot;ad-hoc&quot;. Consulte el tutorial sobre [creación de un esquema ad-hoc](../tutorials/ad-hoc.md) para obtener más información.
>
>Para obtener información más general sobre los comportamientos de los datos en cuanto a cómo afectan a la composición del esquema, consulte la guía sobre los [conceptos básicos de la composición del esquema](../schema/composition.md).

El extremo `/behaviors` de la API [!DNL Schema Registry] le permite vista de los comportamientos disponibles en el contenedor `global`.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas exitosas a cualquier API de Experience Platform.

## Recuperar una lista de comportamientos {#list}

Puede recuperar una lista de todos los comportamientos disponibles haciendo una solicitud de GET al extremo `/behaviors`.

**Formato API**

```http
GET /global/behaviors
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Respuesta**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Buscar un comportamiento {#lookup}

Puede buscar un comportamiento específico proporcionando su ID en la ruta de una solicitud de GET al extremo `/behaviors`.

**Formato API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BEHAVIOR_ID}` | El `meta:altId` o `$id` con codificación URL del comportamiento que desea buscar. |

**Solicitud**

La siguiente solicitud recupera los detalles del comportamiento del registro al proporcionar su `meta:altId` en la ruta de la solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del comportamiento, incluida su versión, descripción y los atributos que el comportamiento proporciona a las clases que lo emplean.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Pasos siguientes

Esta guía abarcó el uso del extremo `/behaviors` en la API [!DNL Schema Registry]. Para obtener información sobre cómo asignar un comportamiento a una clase mediante la API, consulte la [guía de extremo de clases](./classes.md).