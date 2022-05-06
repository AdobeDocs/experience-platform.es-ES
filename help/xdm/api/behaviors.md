---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquemas;comportamiento;comportamiento;comportamientos;comportamientos;
solution: Experience Platform
title: Punto final de la API Behaviors
description: El extremo /comportamientos de la API del Registro de esquemas permite recuperar todos los comportamientos disponibles en el contenedor global.
topic-legacy: developer guide
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 6%

---

# Punto final de comportamiento

En Experience Data Model (XDM), los comportamientos definen la naturaleza de los datos que describe un esquema. Cada clase XDM debe hacer referencia a un comportamiento específico, que heredarán todos los esquemas que emplean esa clase. Para casi todos los casos de uso en Platform, hay dos comportamientos disponibles:

* **[!UICONTROL Registro]**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **[!UICONTROL Serie temporal]**: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirectamente.

>[!NOTE]
>
>Existen algunos casos de uso en Platform que requieren el uso de un esquema que no emplea ninguno de los comportamientos anteriores. Para estos casos, hay disponible un tercer comportamiento &quot;ad hoc&quot;. Consulte el tutorial en [creación de un esquema ad hoc](../tutorials/ad-hoc.md) para obtener más información.
>
>Para obtener información más general sobre los comportamientos de los datos en cuanto a cómo afectan a la composición del esquema, consulte la guía de la [conceptos básicos de la composición del esquema](../schema/composition.md).

La variable `/behaviors` en la variable [!DNL Schema Registry] La API le permite ver los comportamientos disponibles en la `global` contenedor.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API de ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de comportamientos {#list}

Puede recuperar una lista de todos los comportamientos disponibles realizando una solicitud de GET al `/behaviors` punto final.

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

## Buscar un comportamiento {#lookup}

Puede buscar un comportamiento específico proporcionando su ID en la ruta de una solicitud de GET al `/behaviors` punto final.

**Formato de API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BEHAVIOR_ID}` | La variable `meta:altId` o con codificación de URL `$id` del comportamiento que desea buscar. |

{style=&quot;table-layout:auto&quot;}

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

Esta guía abarcaba el uso de la variable `/behaviors` en la variable [!DNL Schema Registry] API. Para obtener información sobre cómo asignar un comportamiento a una clase mediante la API, consulte la [guía de extremo de clases](./classes.md).
