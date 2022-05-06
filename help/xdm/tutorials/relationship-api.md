---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de Experience;modelo de datos;modelo de datos;registro de esquema;registro de esquema;esquema;esquema;esquemas;esquemas;relación;descriptor de relación;descriptor de relación;identidad de referencia;identidad de referencia;
solution: Experience Platform
title: Definir una relación entre dos esquemas con la API del Registro de esquemas
description: Este documento proporciona un tutorial para definir una relación "uno a uno" entre dos esquemas definidos por su organización mediante la API del Registro de esquemas.
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 3%

---

# Defina una relación entre dos esquemas con la variable [!DNL Schema Registry] API

La capacidad de comprender las relaciones entre los clientes y sus interacciones con la marca a través de varios canales es una parte importante de Adobe Experience Platform. Definición de estas relaciones dentro de la estructura del [!DNL Experience Data Model] Los esquemas (XDM) le permiten obtener perspectivas complejas sobre los datos de sus clientes.

Mientras que las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas pertenecientes a diferentes clases, se debe agregar un campo de relación dedicado a un esquema de origen que haga referencia a la identidad de un esquema de destino.

Este documento proporciona un tutorial para definir una relación &quot;uno a uno&quot; entre dos esquemas definidos por su organización mediante el [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Primeros pasos

Este tutorial requiere una comprensión práctica de [!DNL Experience Data Model] (XDM) y [!DNL XDM System]. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
   * [Aspectos básicos de la composición del esquema](../schema/composition.md): Introducción de los componentes básicos de los esquemas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, revise la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar correctamente llamadas a la función [!DNL Schema Registry] API. Esto incluye el `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al [!DNL Accept] y sus posibles valores).

## Definir un esquema de origen y destino {#define-schemas}

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Este tutorial crea una relación entre los miembros del programa de fidelidad actual de una organización (definido en un[!DNL Loyalty Members]&quot; esquema) y sus hoteles favoritos (definidos en un[!DNL Hotels]&quot; esquema).

Las relaciones de esquema se representan mediante una **esquema de origen** tener un campo que haga referencia a otro campo dentro de un **esquema de destino**. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como esquema de destino.

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener definidas identidades principales y estar habilitados para [!DNL Real-time Customer Profile]. Consulte la sección sobre [activación de un esquema para su uso en Perfil](./create-schema-api.md#profile) en el tutorial de creación de esquemas si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Para definir una relación entre dos esquemas, primero debe adquirir la variable `$id` para ambos esquemas. Si conoce los nombres para mostrar (`title`) de los esquemas, puede encontrar sus `$id` realizando una solicitud de GET a la variable `/tenant/schemas` en la variable [!DNL Schema Registry] API.

**Formato de API**

```http
GET /tenant/schemas
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>La variable [!DNL Accept] header `application/vnd.adobe.xed-id+json` solo devuelve los títulos, ID y versiones de los esquemas resultantes.

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

Registre el `$id` los valores de los dos esquemas que desea definir una relación entre. Estos valores se utilizarán en pasos posteriores.

## Definición de un campo de referencia para el esquema de origen

Dentro de [!DNL Schema Registry], los descriptores de relaciones funcionan de manera similar a las claves externas en las tablas de bases de datos relacionales: un campo del esquema de origen actúa como referencia del campo de identidad principal de un esquema de destino. Si el esquema de origen no tiene un campo para este fin, es posible que tenga que crear un grupo de campos de esquema con el nuevo campo y añadirlo al esquema. Este nuevo campo debe tener un `type` valor de &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>A diferencia del esquema de destino, el esquema de origen no puede utilizar su identidad principal como campo de referencia.

En este tutorial, el esquema de destino &quot;[!DNL Hotels]&quot; contiene un `hotelId` que sirve como identidad principal del esquema y, por lo tanto, también actúa como campo de referencia. Sin embargo, el esquema de origen &quot;[!DNL Loyalty Members]&quot; no tiene un campo específico para utilizarlo como referencia y debe recibir un nuevo grupo de campos que añada un nuevo campo al esquema: `favoriteHotel`.

>[!NOTE]
>
>Si el esquema de origen ya tiene un campo dedicado que planea utilizar como campo de referencia, puede avanzar al paso [creación de un descriptor de referencia](#reference-identity).

### Crear un nuevo grupo de campos

Para añadir un nuevo campo a un esquema, primero debe definirse en un grupo de campos. Puede crear un nuevo grupo de campos realizando una solicitud de POST al `/tenant/fieldgroups` punto final.

**Formato de API**

```http
POST /tenant/fieldgroups
```

**Solicitud**

La siguiente solicitud crea un nuevo grupo de campos que agrega un `favoriteHotel` en el campo `_{TENANT_ID}` área de nombres de cualquier esquema al que se añada.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
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

Una respuesta correcta devuelve los detalles del grupo de campos recién creado.

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
    "description": "Favorite hotel field group for the Loyalty Members schema.",
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
| `$id` | El sistema generó un identificador único de solo lectura del nuevo grupo de campos. Toma la forma de URI. |

{style=&quot;table-layout:auto&quot;}

Registre el `$id` URI del grupo de campos, que se utilizará en el siguiente paso de añadir el grupo de campos al esquema de origen.

### Añadir el grupo de campos al esquema de origen

Una vez creado un grupo de campos, puede agregarlo al esquema de origen realizando una solicitud de PATCH al `/tenant/schemas/{SCHEMA_ID}` punto final.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La dirección URL codificada `$id` URI o `meta:altId` del esquema de origen. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud agrega el[!DNL Favorite Hotel]&quot; grupo de campos a &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | La operación de PATCH que se va a realizar. Esta solicitud utiliza la variable `add` operación. |
| `path` | La ruta al campo de esquema donde se agregará el nuevo recurso. Al agregar grupos de campos a esquemas, el valor debe ser &quot;/allOf/-&quot;. |
| `value.$ref` | La variable `$id` del grupo de campos que se va a añadir. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles del esquema actualizado, que ahora incluye la variable `$ref` valor del grupo de campos añadidos en su `allOf` matriz.

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
    "imsOrg": "{ORG_ID}",
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

## Crear un descriptor de identidad de referencia {#reference-identity}

Los campos de esquema deben tener un descriptor de identidad de referencia aplicado si se utilizan como referencia de otros esquemas de una relación. Dado que la variable `favoriteHotel` en &quot;[!DNL Loyalty Members]&quot; se referirá a la `hotelId` en &quot;[!DNL Hotels]&quot;, `hotelId` debe tener un descriptor de identidad de referencia.

Cree un descriptor de referencia para el esquema de destino realizando una solicitud de POST al `/tenant/descriptors` punto final.

**Formato de API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud crea un descriptor de referencia para la variable `hotelId` en el esquema de destino &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está definiendo. Para los descriptores de referencia, el valor debe ser &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | La variable `$id` URL del esquema de destino. |
| `xdm:sourceVersion` | Número de versión del esquema de destino. |
| `sourceProperty` | Ruta al campo de identidad principal del esquema de destino. |
| `xdm:identityNamespace` | El área de nombres de identidad del campo de referencia. Debe ser el mismo espacio de nombres que se utiliza al definir el campo que la identidad principal del esquema. Consulte la [información general del área de nombres de identidad](../../identity-service/home.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor de referencia recién creado para el esquema de destino.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Crear un descriptor de relación {#create-descriptor}

Los descriptores de relación establecen una relación uno a uno entre un esquema de origen y un esquema de destino. Una vez definido un descriptor de referencia para el esquema de destino, puede crear un nuevo descriptor de relación realizando una solicitud de POST al `/tenant/descriptors` punto final.

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se va a crear. La variable `@type` para los descriptores de relación es &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | La variable `$id` URL del esquema de origen. |
| `xdm:sourceVersion` | Número de versión del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo de referencia en el esquema de origen. |
| `xdm:destinationSchema` | La variable `$id` URL del esquema de destino. |
| `xdm:destinationVersion` | Número de versión del esquema de destino. |
| `xdm:destinationProperty` | Ruta al campo de referencia en el esquema de destino. |

{style=&quot;table-layout:auto&quot;}

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

Al seguir este tutorial, ha creado correctamente una relación &quot;uno a uno&quot; entre dos esquemas. Para obtener más información sobre cómo trabajar con descriptores, use la variable [!DNL Schema Registry] API, consulte la [Guía para desarrolladores de Schema Registry](../api/descriptors.md). Para ver los pasos sobre cómo definir relaciones de esquema en la interfaz de usuario, consulte el tutorial sobre [definición de relaciones de esquema mediante el Editor de esquemas](relationship-ui.md).
