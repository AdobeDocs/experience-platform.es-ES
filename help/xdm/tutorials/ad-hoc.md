---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;ad-hoc;ad hoc;adhoc;Ad-hoc;Ad hoc;Adhoc;tutorial;Tutorial;create;Create;schema;Schema
solution: Experience Platform
title: Creación de un esquema ad-hoc
description: En circunstancias específicas, puede que sea necesario crear un esquema de modelo de datos de experiencia (XDM) con campos a los que solo un conjunto de datos debe asignar un nombre para su uso. Esto se denomina esquema "ad-hoc". Los esquemas específicos se utilizan en varios flujos de trabajo de ingestión de datos para Experience Platform, incluida la ingesta de archivos CSV y la creación de determinados tipos de conexiones de origen.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---


# Creación de un esquema ad-hoc

En circunstancias específicas, puede ser necesario crear un esquema [!DNL Experience Data Model] (XDM) con campos a los que se les asigne un solo conjunto de datos para su uso. Esto se denomina esquema &quot;ad-hoc&quot;. Los esquemas ad-hoc se utilizan en varios flujos de trabajo de ingesta de datos para [!DNL Experience Platform], incluyendo la ingesta de archivos CSV y la creación de determinados tipos de conexiones de origen.

Este documento proporciona pasos generales para crear un esquema ad-hoc mediante la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquemas. Está pensado para utilizarse junto con otros [!DNL Experience Platform] tutoriales que requieran la creación de un esquema ad-hoc como parte de su flujo de trabajo. Cada uno de esos documentos proporciona información detallada sobre cómo configurar correctamente un esquema ad-hoc para su caso de uso específico.

## Primeros pasos

Este tutorial requiere un conocimiento práctico del sistema [!DNL Experience Data Model] (XDM). Antes de iniciar este tutorial, consulte la siguiente documentación de XDM:

- [Descripción general](../home.md)del sistema XDM: Información general de alto nivel sobre XDM y su implementación en [!DNL Experience Platform].
- [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Información general sobre los componentes básicos de los esquemas XDM.

Antes de iniciar este tutorial, consulte la guía [del](../api/getting-started.md) desarrollador para obtener información importante que necesita conocer a fin de realizar correctamente llamadas a la [!DNL Schema Registry] API. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).

## Creación de una clase ad-hoc

El comportamiento de los datos de un esquema XDM viene determinado por su clase subyacente. El primer paso para crear un esquema ad-hoc es crear una clase basada en el `adhoc` comportamiento. Esto se realiza realizando una solicitud de POST al `/tenant/classes` extremo.

**Formato API**

```http
POST /tenant/classes
```

**Solicitud**

La siguiente solicitud crea una nueva clase XDM, configurada por los atributos suministrados en la carga útil. Al proporcionar una `$ref` propiedad definida como `https://ns.adobe.com/xdm/data/adhoc` en la `allOf` matriz, esta clase hereda el `adhoc` comportamiento. La solicitud también define un `_adhoc` objeto, que contiene los campos personalizados de la clase.

>[!NOTE]
>
>Los campos personalizados definidos en `_adhoc` varían según el caso de uso del esquema ad-hoc. Consulte el flujo de trabajo específico en el tutorial correspondiente para los campos personalizados requeridos según el caso de uso.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `$ref` | El comportamiento de los datos de la nueva clase. Para las clases ad-hoc, este valor debe establecerse en `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Objeto que contiene los campos personalizados de la clase, expresados como pares de clave-valor de los nombres de campo y los tipos de datos. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la nueva clase, reemplazando el nombre del `properties._adhoc` objeto por un GUID que es un identificador único de sólo lectura para la clase generado por el sistema. El `meta:datasetNamespace` atributo también se genera automáticamente y se incluye en la respuesta.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `$id` | URI que sirve como identificador único de sólo lectura generado por el sistema para la nueva clase ad-hoc. Este valor se utiliza en el siguiente paso de la creación de un esquema ad-hoc. |

## Creación de un esquema ad-hoc

Una vez que haya creado una clase ad-hoc, puede crear un nuevo esquema que implemente esa clase realizando una solicitud de POST al `/tenant/schemas` extremo.

**Formato API**

```http
POST /tenant/schemas
```

**Solicitud**

La siguiente solicitud crea un nuevo esquema, que proporciona una referencia (`$ref`) al `$id` de la clase ad-hoc creada previamente en su carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema recién creado, incluyendo el generado por el sistema, de sólo lectura `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Vista del esquema ad hoc completo

>[!NOTE]
>
>Este paso es opcional. Si no desea inspeccionar la estructura de campos de su esquema ad-hoc, puede saltar a la sección de [próximos pasos](#next-steps) al final de este tutorial.

Una vez creado el esquema ad-hoc, puede realizar una solicitud de búsqueda (GET) para vista del esquema en su formulario ampliado. Esto se lleva a cabo utilizando el encabezado Accept adecuado en la solicitud de GET, como se muestra a continuación.

**Formato API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El `$id` URI con codificación URL o `meta:altId` del esquema ad-hoc al que desea acceder. |

**Solicitud**

La siguiente solicitud utiliza el encabezado Accept `application/vnd.adobe.xed-full+json; version=1`, que devuelve la forma expandida del esquema. Tenga en cuenta que al recuperar un recurso específico desde el [!DNL Schema Registry], el encabezado Accept de la solicitud debe incluir la versión principal del recurso en cuestión.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema, incluidos todos los campos anidados en `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Pasos siguientes {#next-steps}

Siguiendo este tutorial, ha creado correctamente un nuevo esquema ad-hoc. Si se le ha traído a este documento como parte de otro tutorial, ahora puede utilizar el `$id` de su esquema ad-hoc para completar el flujo de trabajo como se le ha indicado.

Para obtener más información sobre cómo trabajar con la [!DNL Schema Registry] API, consulte la guía [para](../api/getting-started.md)desarrolladores.