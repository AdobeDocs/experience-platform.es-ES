---
title: Añadir campos específicos a un esquema mediante la API del Registro de esquemas
description: Aprenda a añadir campos individuales de grupos de campos preexistentes a un esquema del Modelo de datos de experiencia (XDM) mediante la API del Registro de esquemas.
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# Añadir campos específicos a un esquema mediante la API del Registro de esquemas

Los esquemas del Modelo de datos de experiencia (XDM) están compuestos por una clase base, con campos adicionales incluidos mediante el uso de grupos de campos estándar definidos por grupos de campos personalizados y de Adobe definidos por su organización.

Al crear un esquema, es posible que desee utilizar algunos campos de un grupo de campos dado y excluir otros del mismo grupo que no necesite. Este tutorial muestra cómo añadir campos individuales de un grupo de campos a un esquema mediante la API del Registro de esquemas.

>[!NOTE]
>
>Para obtener información sobre cómo añadir y quitar campos de esquema individuales en la interfaz de usuario de Adobe Experience Platform, consulte la guía de [flujos de trabajo basados en el campo](../ui/field-based-workflows.md) (actualmente en versión beta).

## Requisitos previos

Este tutorial implica realizar llamadas a la función [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de empezar, revise la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar correctamente llamadas a la API de , incluido su `{TENANT_ID}`, el concepto de contenedores y los encabezados necesarios para realizar solicitudes.

## Información sobre `meta:refProperty` field

Para cualquier esquema determinado, los grupos de clases y campos que componen su estructura se encuentran bajo su `allOf` matriz. Cada componente se representa como un objeto que contiene un `$ref` propiedad que hace referencia al URI del componente `$id`.

El siguiente JSON representa un esquema simplificado que utiliza una sola clase (`experienceevent`) y grupo de campos (`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

Para cualquier objeto del `allOf` matriz que hace referencia a un grupo de campos, puede agregar un elemento secundario `meta:refProperty` para especificar los campos del grupo que deben incluirse en el esquema.

>[!NOTE]
>
>Cada campo se especifica mediante una cadena de puntero JSON, que representa la ruta al campo dentro de su grupo de campos respectivo. La cadena debe comenzar con una barra diagonal (`/`) y no debe incluir ninguno `properties` áreas de nombres. Por ejemplo: `/_experience/campaign/message/id`.

Cuando se incluye como una cadena, `meta:refProperty` puede hacer referencia a un solo campo de un grupo. Se pueden incluir otros campos del mismo grupo utilizando el mismo `$ref` en otro objeto con un `meta:refProperty` valor.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

Alternativamente, `meta:refProperty` se puede proporcionar como una matriz, lo que permite especificar varios campos para incluir de un grupo determinado en un único `allOf` elemento de lista:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Adición de campos mediante una operación de PUT

Puede utilizar una solicitud de PUT para reescribir todo un esquema y configurar los campos que desea incluir en `allOf`.

**Formato de API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema que desea reescribir. |

**Solicitud**

La siguiente solicitud actualiza los campos específicos incluidos en el grupo de campos en el `allOf` matriz.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
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

>[!NOTE]
>
>Para obtener información más detallada sobre las solicitudes de PUT para esquemas, consulte la [guía de extremo de esquemas](../api/schemas.md#put).

## Adición de campos mediante una operación de PATCH

Puede utilizar una solicitud de PATCH para añadir campos individuales a un esquema sin sobrescribir otros. El Registro de esquemas admite todas las operaciones de parches de JSON estándar, incluidas las `add`, `remove`y `replace`. Para obtener más información sobre el parche JSON, consulte la [Guía de fundamentos de API](../../landing/api-fundamentals.md#json-patch).

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema que desea reescribir. |

**Solicitud**

La siguiente solicitud agrega un nuevo objeto al `allOf` matriz, especificando los campos que se van a añadir.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
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

>[!NOTE]
>
>Para obtener información más detallada sobre las solicitudes de PATCH para esquemas, consulte la [guía de extremo de esquemas](../api/schemas.md#patch).

## Pasos siguientes

Esta guía explica cómo utilizar las llamadas API para añadir campos individuales de un grupo de campos existente a un esquema. Para obtener más información sobre cómo realizar tareas similares basadas en campos en la interfaz de usuario de Platform, consulte la guía de [flujos de trabajo basados en el campo](../ui/field-based-workflows.md).

Para obtener más información sobre las capacidades de la API del Registro de esquemas, consulte la [Información general de API](../api/overview.md) para obtener una lista completa de endpoints y procesos.
