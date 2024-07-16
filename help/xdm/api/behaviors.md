---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;comportamiento;comportamientos;comportamientos;comportamientos;
solution: Experience Platform
title: Extremo de API de comportamientos
description: El extremo /behavior de la API de Registro de esquemas permite recuperar todos los comportamientos disponibles en el contenedor global.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 3%

---

# Extremo de comportamientos

En el Modelo de datos de experiencia (XDM), los comportamientos definen la naturaleza de los datos que describe un esquema. Cada clase XDM debe hacer referencia a un comportamiento específico, que heredarán todos los esquemas que emplean esa clase. Para casi todos los casos de uso de Platform, hay dos comportamientos disponibles:

* **[!UICONTROL Registro]**: proporciona información sobre los atributos de un asunto. Un sujeto podría ser una organización o un individuo.
* **[!UICONTROL Serie temporal]**: proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

>[!NOTE]
>
>Hay algunos casos de uso en Platform que requieren el uso de un esquema que no emplea ninguno de los comportamientos anteriores. Para estos casos, hay disponible un tercer comportamiento &quot;ad hoc&quot;. Consulte el tutorial sobre [creación de un esquema ad hoc](../tutorials/ad-hoc.md) para obtener más información.
>
>Para obtener información más general sobre los comportamientos de datos en términos de cómo afectan a la composición de esquemas, consulte la guía de [conceptos básicos de la composición de esquemas](../schema/composition.md).

El extremo `/behaviors` de la API [!DNL Schema Registry] le permite ver los comportamientos disponibles en el contenedor `global`.

## Introducción

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de comportamientos {#list}

Puede recuperar una lista de todos los comportamientos disponibles realizando una solicitud de GET al extremo `/behaviors`.

**Formato de API**

```http
GET /global/behaviors
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Búsqueda de un comportamiento {#lookup}

Puede buscar un comportamiento específico proporcionando su ID en la ruta de una petición de GET al extremo `/behaviors`.

**Formato de API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BEHAVIOR_ID}` | `meta:altId` o `$id` con codificación de dirección URL del comportamiento que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera los detalles del comportamiento del registro al proporcionar su `meta:altId` en la ruta de solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del comportamiento, incluida su versión, descripción y los atributos que proporciona a las clases que lo emplean.

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

Esta guía describe el uso del extremo `/behaviors` en la API [!DNL Schema Registry]. Para obtener información sobre cómo asignar un comportamiento a una clase mediante la API, consulte la [guía de extremo de clases](./classes.md).
