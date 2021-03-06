---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;específico;ad hoc;ad hoc;ad hoc;específico;tutorial;tutorial;crear;crear;esquema;esquema
solution: Experience Platform
title: Crear un esquema ad hoc
description: En circunstancias específicas, puede ser necesario crear un esquema del Modelo de datos de experiencia (XDM) con campos a los que solo se les asigna un nombre para su uso mediante un único conjunto de datos. Esto se denomina esquema "ad-hoc". Los esquemas específicos se utilizan en varios flujos de trabajo de ingesta de datos para el Experience Platform, incluida la ingesta de archivos CSV y la creación de ciertos tipos de conexiones de origen.
topic-legacy: tutorial
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 4%

---

# Crear un esquema ad hoc

En circunstancias específicas, puede ser necesario crear un [!DNL Experience Data Model] (XDM) con campos a los que se asigna un nombre para su uso solamente mediante un único conjunto de datos. Esto se denomina esquema &quot;ad-hoc&quot;. Los esquemas específicos se utilizan en varios flujos de trabajo de ingesta de datos para [!DNL Experience Platform], incluida la ingesta de archivos CSV y la creación de determinados tipos de conexiones de origen.

Este documento proporciona pasos generales para crear un esquema ad-hoc usando la variable [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Está previsto que se utilice junto con otros [!DNL Experience Platform] tutoriales que requieren la creación de un esquema ad-hoc como parte de su flujo de trabajo. Cada uno de esos documentos proporciona información detallada sobre cómo configurar correctamente un esquema ad hoc para su caso de uso específico.

## Primeros pasos

Este tutorial requiere una comprensión práctica de [!DNL Experience Data Model] (XDM). Antes de iniciar este tutorial, revise la siguiente documentación de XDM:

- [Información general del sistema XDM](../home.md): Información general de alto nivel sobre XDM y su implementación en [!DNL Experience Platform].
- [Aspectos básicos de la composición del esquema](../schema/composition.md): Información general sobre los componentes básicos de los esquemas XDM.

Antes de iniciar este tutorial, revise la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar correctamente llamadas a la función [!DNL Schema Registry] API. Esto incluye el `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).

## Crear una clase ad-hoc

El comportamiento de los datos de un esquema XDM está determinado por su clase subyacente. El primer paso para crear un esquema ad-hoc es crear una clase basada en la variable `adhoc` comportamiento. Para ello, realice una solicitud de POST al `/tenant/classes` punto final.

**Formato de API**

```http
POST /tenant/classes
```

**Solicitud**

La siguiente solicitud crea una nueva clase XDM, configurada por los atributos suministrados en la carga útil. Al proporcionar un `$ref` propiedad establecida en `https://ns.adobe.com/xdm/data/adhoc` en el `allOf` matriz, esta clase hereda el `adhoc` comportamiento. La solicitud también define un `_adhoc` , que contiene los campos personalizados de la clase .

>[!NOTE]
>
>Los campos personalizados definidos en `_adhoc` variarán según el caso de uso del esquema ad-hoc. Consulte el flujo de trabajo específico en el tutorial adecuado para los campos personalizados necesarios según el caso de uso.

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
| `$ref` | El comportamiento de los datos de la nueva clase. Para las clases ad-hoc, este valor debe establecerse en `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Objeto que contiene los campos personalizados de la clase, expresados como pares clave-valor de los nombres de campo y los tipos de datos. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la nueva clase, reemplazando la variable `properties._adhoc` nombre del objeto con un GUID que es un identificador único generado por el sistema y de solo lectura para la clase. La variable `meta:datasetNamespace` también se genera automáticamente y se incluye en la respuesta.

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
| `$id` | URI que sirve como identificador único generado por el sistema de solo lectura para la nueva clase ad hoc. Este valor se utiliza en el siguiente paso de la creación de un esquema ad-hoc. |

{style=&quot;table-layout:auto&quot;}

## Crear un esquema ad hoc

Una vez que haya creado una clase ad-hoc, puede crear un nuevo esquema que implemente esa clase realizando una solicitud de POST al `/tenant/schemas` punto final.

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La siguiente solicitud crea un nuevo esquema, que proporciona una referencia (`$ref`) a la variable `$id` de la clase ad hoc creada anteriormente en su carga útil.

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

Una respuesta correcta devuelve los detalles del esquema recién creado, incluido el generado por el sistema, de solo lectura `$id`.

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
>Este paso es opcional. Si no desea inspeccionar la estructura de campos del esquema ad-hoc, puede saltar al [pasos siguientes](#next-steps) al final de este tutorial.

Una vez creado el esquema ad hoc, puede realizar una solicitud de consulta (GET) para ver el esquema en su formulario expandido. Esto se realiza utilizando el encabezado Accept apropiado en la solicitud de GET, como se muestra a continuación.

**Formato de API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La dirección URL codificada `$id` URI o `meta:altId` del esquema ad hoc al que desea acceder. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud utiliza el encabezado Accept `application/vnd.adobe.xed-full+json; version=1`, que devuelve el formulario expandido del esquema. Tenga en cuenta que al recuperar un recurso específico desde la variable [!DNL Schema Registry], el encabezado Accept de la solicitud debe incluir la versión principal del recurso en cuestión.

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

Siguiendo este tutorial, ha creado correctamente un nuevo esquema ad hoc. Si se le ha traído a este documento como parte de otro tutorial, ahora puede usar la variable `$id` del esquema ad hoc para completar el flujo de trabajo como se indica.

Para obtener más información sobre cómo trabajar con la variable [!DNL Schema Registry] API, consulte la [guía para desarrolladores](../api/getting-started.md).
