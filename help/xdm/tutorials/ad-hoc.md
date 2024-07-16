---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;ad hoc;ad hoc;ad hoc;ad hoc;ad hoc;ad hoc;tutorial;tutorial;crear;esquema;Esquema
solution: Experience Platform
title: Creación de un esquema ad hoc
description: En circunstancias específicas, puede ser necesario crear un esquema del Modelo de datos de experiencia (XDM) con campos que tengan un espacio de nombres para su uso únicamente por parte de un único conjunto de datos. Esto se conoce como esquema "ad-hoc". Los esquemas ad hoc se utilizan en varios flujos de trabajo de ingesta de datos para Experience Platform, incluida la ingesta de archivos CSV y la creación de determinados tipos de conexiones de origen.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 3%

---

# Creación de un esquema ad hoc

En circunstancias específicas, puede ser necesario crear un esquema [!DNL Experience Data Model] (XDM) con campos que tengan un espacio de nombres para que los use un solo conjunto de datos. Esto se conoce como esquema &quot;ad-hoc&quot;. Los esquemas ad hoc se utilizan en varios flujos de trabajo de ingesta de datos para [!DNL Experience Platform], incluida la ingesta de archivos CSV y la creación de determinados tipos de conexiones de origen.

Este documento proporciona pasos generales para crear un esquema ad-hoc mediante la [API de Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Está diseñado para utilizarse junto con otros tutoriales de [!DNL Experience Platform] que requieran la creación de un esquema ad-hoc como parte de su flujo de trabajo. Cada uno de estos documentos proporciona información detallada sobre cómo configurar correctamente un esquema ad-hoc para su caso de uso específico.

## Introducción

Este tutorial requiere una comprensión práctica del sistema [!DNL Experience Data Model] (XDM). Antes de iniciar este tutorial, revise la siguiente documentación de XDM:

- [Información general del sistema XDM](../home.md): Información general de alto nivel sobre XDM y su implementación en [!DNL Experience Platform].
- [Aspectos básicos de la composición de esquemas](../schema/composition.md): Una descripción general de los componentes básicos de los esquemas XDM.

Antes de comenzar este tutorial, revisa la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API [!DNL Schema Registry] correctamente. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados necesarios para realizar solicitudes (con especial atención al encabezado Aceptar y sus posibles valores).

## Creación de una clase ad hoc

El comportamiento de los datos de un esquema XDM está determinado por su clase subyacente. El primer paso para crear un esquema ad-hoc es crear una clase basada en el comportamiento `adhoc`. Para ello, realice una solicitud de POST al extremo `/tenant/classes`.

**Formato de API**

```http
POST /tenant/classes
```

**Solicitud**

La siguiente solicitud crea una nueva clase XDM, configurada por los atributos proporcionados en la carga útil. Al proporcionar una propiedad `$ref` establecida en `https://ns.adobe.com/xdm/data/adhoc` en la matriz `allOf`, esta clase hereda el comportamiento `adhoc`. La solicitud también define un objeto `_adhoc`, que contiene los campos personalizados para la clase.

>[!NOTE]
>
>Los campos personalizados definidos en `_adhoc` varían según el caso de uso del esquema ad hoc. Consulte el flujo de trabajo específico en el tutorial adecuado para los campos personalizados requeridos en función del caso de uso.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `$ref` | Comportamiento de los datos de la nueva clase. Para las clases ad hoc, este valor debe establecerse en `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Un objeto que contiene los campos personalizados para la clase, expresados como pares clave-valor de nombres de campo y tipos de datos. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la nueva clase y reemplaza el nombre del objeto `properties._adhoc` por un GUID que es un identificador único de sólo lectura generado por el sistema para la clase. El atributo `meta:datasetNamespace` también se genera automáticamente y se incluye en la respuesta.

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
    "imsOrg": "{ORG_ID}",
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
| `$id` | URI que sirve como identificador único de sólo lectura generado por el sistema para la nueva clase ad hoc. Este valor se utiliza en el siguiente paso para crear un esquema ad-hoc. |

{style="table-layout:auto"}

## Creación de un esquema ad hoc

Una vez creada una clase ad-hoc, puede crear un nuevo esquema que implemente esa clase realizando una solicitud del POST al extremo `/tenant/schemas`.

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La siguiente solicitud crea un nuevo esquema y proporciona una referencia (`$ref`) a `$id` de la clase ad-hoc creada anteriormente en su carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve los detalles del esquema recién creado, incluido su `$id` de solo lectura generado por el sistema.

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
    "imsOrg": "{ORG_ID}",
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

## Ver el esquema ad hoc completo

>[!NOTE]
>
>Este paso es opcional. Si no desea inspeccionar la estructura de campos del esquema ad-hoc, puede saltar a la sección [pasos siguientes](#next-steps) al final de este tutorial.

Una vez creado el esquema ad hoc, puede realizar una solicitud de consulta (GET) para ver el esquema en su forma expandida. Esto se realiza utilizando el encabezado Aceptar adecuado en la solicitud de GET, como se muestra a continuación.

**Formato de API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` con codificación de dirección URL o `meta:altId` del esquema ad hoc al que desea tener acceso. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud utiliza el encabezado Aceptar `application/vnd.adobe.xed-full+json; version=1`, que devuelve la forma expandida del esquema. Tenga en cuenta que al recuperar un recurso específico de [!DNL Schema Registry], el encabezado Aceptar de la solicitud debe incluir la versión principal del recurso en cuestión.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Al seguir este tutorial, ha creado correctamente un nuevo esquema ad hoc. Si ha llegado a este documento como parte de otro tutorial, ahora puede utilizar `$id` de su esquema ad-hoc para completar el flujo de trabajo como se le ha indicado.

Para obtener más información sobre cómo trabajar con la API [!DNL Schema Registry], consulte la [guía para desarrolladores](../api/getting-started.md).
