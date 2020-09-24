---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;relationship;Relationship;relationship descriptor;Relationship descriptor;reference identity;Reference identity;
solution: Experience Platform
title: Definir una relación entre dos esquemas mediante la API de Registro de Esquema
description: Este documento proporciona un tutorial para definir una relación uno a uno entre dos esquemas definidos por su organización mediante la API del Registro de Esquemas.
topic: tutorial
type: Tutorials
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---


# Definir una relación entre dos esquemas mediante la [!DNL Schema Registry] API

La capacidad de comprender las relaciones entre sus clientes y sus interacciones con su marca en diversos canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de sus esquemas [!DNL Experience Data Model] (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes.

Aunque las relaciones de esquema pueden inferirse mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto sólo se aplica a esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas que pertenecen a diferentes clases, se debe agregar un campo **de** relación dedicado a un esquema de origen que haga referencia a la identidad de un esquema de destino.

Este documento proporciona un tutorial para definir una relación uno a uno entre dos esquemas definidos por su organización mediante la [[!DNL Esquema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de [!DNL Experience Data Model] (XDM) y [!DNL XDM System]. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
   * [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Introducción de los componentes básicos de los esquemas XDM.
* [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la guía [del](../api/getting-started.md) desarrollador para obtener información importante que necesita conocer a fin de realizar correctamente llamadas a la [!DNL Schema Registry] API. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al [!DNL Accept] encabezado y sus posibles valores).

## Definir un esquema de origen y destino {#define-schemas}

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Este tutorial crea una relación entre los miembros del programa de lealtad actual de una organización (definido en un esquema &quot;[!DNL Loyalty Members]&quot;) y sus hoteles favoritos (definidos en un esquema &quot;[!DNL Hotels]&quot;).

Las relaciones de esquema están representadas por un esquema **de** origen que tiene un campo que hace referencia a otro campo dentro de un esquema **de** destino. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como el esquema de destino.

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener identidades primarias definidas y estar habilitados para [!DNL Real-time Customer Profile]. Consulte la sección sobre la [activación de un esquema para su uso en Perfil](./create-schema-api.md#profile) en el tutorial de creación de esquema si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Para definir una relación entre dos esquemas, primero debe adquirir los `$id` valores de ambos esquemas. Si conoce los nombres para mostrar (`title`) de los esquemas, puede encontrar sus `$id` valores realizando una solicitud de GET al `/tenant/schemas` extremo en la [!DNL Schema Registry] API.

**Formato API**

```http
GET /tenant/schemas
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>El [!DNL Accept] encabezado `application/vnd.adobe.xed-id+json` devuelve solo los títulos, ID y versiones de los esquemas resultantes.

**Respuesta**

Una respuesta correcta devuelve una lista de esquemas definidos por su organización, incluidos sus `name`, `$id`, `meta:altId`y `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Registre los `$id` valores de los dos esquemas entre los que desea definir una relación. Estos valores se utilizarán en pasos posteriores.

## Definir un campo de referencia para el esquema de origen

Dentro de la [!DNL Schema Registry], los descriptores de relación funcionan de manera similar a las claves externas en las tablas de bases de datos relacionales: un campo del esquema de origen actúa como referencia al campo de identidad **** principal de un esquema de destino. Si el esquema de origen no tiene un campo para este fin, puede que necesite crear una mezcla con el nuevo campo y agregarlo al esquema. Este nuevo campo debe tener un `type` valor de &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>A diferencia del esquema de destino, el esquema de origen no puede utilizar su identidad principal como campo de referencia.

En este tutorial, el esquema de destino &quot;[!DNL Hotels]&quot; contiene un `email` campo que sirve como identidad principal del esquema y, por lo tanto, también actuará como campo de referencia. Sin embargo, el esquema de origen &quot;[!DNL Loyalty Members]&quot; no tiene un campo específico para utilizarse como referencia y debe recibir una nueva mezcla que añada un nuevo campo al esquema: `favoriteHotel`.

>[!NOTE]
>
>Si el esquema de origen ya tiene un campo dedicado que se va a utilizar como campo de referencia, puede avanzar en el paso para [crear un descriptor](#reference-identity)de referencia.

### Crear una nueva mezcla

Para agregar un nuevo campo a un esquema, primero debe definirse en una mezcla. Puede crear una nueva mezcla haciendo una solicitud de POST al `/tenant/mixins` punto final.

**Formato API**

```http
POST /tenant/mixins
```

**Solicitud**

La siguiente solicitud crea una nueva mezcla que agrega un `favoriteHotel` campo bajo la `_{TENANT_ID}` Área de nombres de cualquier esquema al que se añada.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la mezcla recién creada.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `$id` | El identificador único de la nueva mezcla generado por el sistema y de sólo lectura. Toma la forma de un URI. |

Registre el `$id` URI de la mezcla, que se utilizará en el siguiente paso de añadir la mezcla al esquema de origen.

### Añadir la mezcla en el esquema de origen

Una vez que haya creado una mezcla, puede agregarla al esquema de origen haciendo una solicitud de PATCH al extremo del `/tenant/schemas/{SCHEMA_ID}` .

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El `$id` URI con codificación URL o `meta:altId` del esquema de origen. |

**Solicitud**

La siguiente solicitud agrega la mezcla &quot;[!DNL Favorite Hotel]&quot; al esquema &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `op` | La operación de PATCH que se va a realizar. Esta solicitud utiliza la `add` operación. |
| `path` | Ruta al campo esquema donde se agregará el nuevo recurso. Al agregar mezclas a esquemas, el valor debe ser &quot;/allOf/-&quot;. |
| `value.$ref` | El `$id` de la mezcla que se va a añadir. |

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado, que ahora incluye el `$ref` valor de la mezcla agregada en su `allOf` matriz.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Creación de un descriptor de identidad de referencia {#reference-identity}

Los campos de esquema deben tener aplicado un descriptor de identidad de referencia si se utilizan como referencia de otros esquemas de una relación. Dado que el `favoriteHotel` campo de &quot;[!DNL Loyalty Members]&quot; hará referencia al `email` campo de &quot;[!DNL Hotels]&quot;, se debe dar un descriptor de identidad de referencia `email` .

Cree un descriptor de referencia para el esquema de destino realizando una solicitud de POST al `/tenant/descriptors` extremo.

**Formato API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud crea un descriptor de referencia para el `email` campo en el esquema de destino &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está definiendo. Para los descriptores de referencia, el valor debe ser &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | La `$id` URL del esquema de destino. |
| `xdm:sourceVersion` | Número de versión del esquema de destino. |
| `sourceProperty` | Ruta al campo de identidad principal del esquema de destino. |
| `xdm:identityNamespace` | Área de nombres de identidad del campo de referencia. Debe ser la misma Área de nombres utilizada al definir el campo que la identidad principal del esquema. Consulte la descripción general [de la Área de nombres de](../../identity-service/home.md) identidad para obtener más información. |

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor de referencia recién creado para el esquema de destino.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Crear un descriptor de relación {#create-descriptor}

Los descriptores de relación establecen una relación uno a uno entre un esquema de origen y un esquema de destino. Una vez definido un descriptor de referencia para el esquema de destino, puede crear un nuevo descriptor de relación realizando una solicitud de POST al extremo `/tenant/descriptors` .

**Formato API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud crea un nuevo descriptor de relación, con &quot;[!DNL Loyalty Members]&quot; como esquema de origen y &quot;[!DNL Legacy Loyalty Members]&quot; como esquema de destino.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/email"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se va a crear. El `@type` valor de los descriptores de relación es &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | La `$id` URL del esquema de origen. |
| `xdm:sourceVersion` | Número de versión del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo de referencia en el esquema de origen. |
| `xdm:destinationSchema` | La `$id` URL del esquema de destino. |
| `xdm:destinationVersion` | Número de versión del esquema de destino. |
| `xdm:destinationProperty` | Ruta al campo de referencia en el esquema de destino. |

### Respuesta

Una respuesta correcta devuelve los detalles del descriptor de relación recién creado.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente una relación uno a uno entre dos esquemas. Para obtener más información sobre cómo trabajar con descriptores mediante la [!DNL Schema Registry] API, consulte la guía [para desarrolladores de](../api/descriptors.md)Esquema Registry. Para ver los pasos sobre cómo definir relaciones de esquema en la interfaz de usuario, consulte el tutorial sobre la [definición de relaciones de esquema mediante el Editor](relationship-ui.md)de Esquemas.
