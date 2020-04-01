---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definir una relación entre dos esquemas mediante la API de Registro de Esquema
topic: tutorials
translation-type: tm+mt
source-git-commit: 7e867ee12578f599c0c596decff126420a9aca01

---


# Definir una relación entre dos esquemas mediante la API de Registro de Esquema


La capacidad de comprender las relaciones entre sus clientes y sus interacciones con su marca en diversos canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de los esquemas del Modelo de datos de experiencia (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes.

Este documento proporciona un tutorial para definir una relación uno a uno entre dos esquemas definidos por su organización mediante la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquemas.

## Primeros pasos

Este tutorial requiere un conocimiento práctico del Modelo de datos de experiencia (XDM) y el sistema XDM. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en la plataforma](../home.md)de experiencias: Información general sobre XDM y su implementación en la plataforma de experiencias.
   * [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Introducción de los componentes básicos de los esquemas XDM.
* [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, consulte la guía [para](../api/getting-started.md) desarrolladores para obtener información importante que necesita conocer a fin de realizar correctamente llamadas a la API del Registro de Esquema. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).

## Definir un esquema de origen y destino {#define-schemas}

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Este tutorial crea una relación entre los miembros del actual programa de lealtad de una organización (definido en un esquema de &quot;miembros de la lealtad&quot;) y sus hoteles favoritos (definido en un esquema de &quot;hoteles&quot;).

Las relaciones de Esquema están representadas por un esquema **de** origen que tiene un campo que hace referencia a otro campo dentro de un esquema **de** destino. En los pasos siguientes, &quot;Miembros de la Lealtad&quot; será el esquema de origen, mientras que &quot;Hoteles&quot; actuará como el esquema de destino.

Para definir una relación entre dos esquemas, primero debe adquirir los `$id` valores de ambos esquemas. Si conoce los nombres para mostrar (`title`) de los esquemas, puede encontrar sus `$id` valores realizando una solicitud GET al `/tenant/schemas` extremo en la API del Registro de Esquema.

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

>[!NOTE] El encabezado Aceptar `application/vnd.adobe.xed-id+json` devuelve solo los títulos, ID y versiones de los esquemas resultantes.

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

## Definición de campos de referencia para ambos esquemas

En el Registro de Esquemas, los descriptores de relaciones funcionan de manera similar a las claves externas en las tablas SQL: un campo del esquema de origen actúa como referencia a un campo de un esquema de destino. Al definir una relación, cada esquema debe tener un campo específico para utilizarse como referencia al otro esquema.

>[!IMPORTANT] Si los esquemas se van a habilitar para su uso en Perfil [de cliente en tiempo](../../profile/home.md)real, el campo de referencia para el esquema de destino debe ser su identidad **** principal. Esto se explica con más detalle más adelante en este tutorial.

Si ninguno de los esquemas tiene un campo para este fin, es posible que tenga que crear una mezcla con el nuevo campo y agregarlo al esquema. Este nuevo campo debe tener un `type` valor de &quot;cadena&quot;.

A efectos de este tutorial, el esquema de destino &quot;Hoteles&quot; ya contiene un campo para este fin: `hotelId`. Sin embargo, el esquema de origen &quot;Miembros de la lealtad&quot; no tiene ese campo y debe recibir una nueva mezcla que añada un nuevo campo, `favoriteHotel`bajo su `TENANT_ID` Área de nombres.

### Crear una nueva mezcla

Para agregar un nuevo campo a un esquema, primero debe definirse en una mezcla. Puede crear una nueva mezcla haciendo una solicitud POST al `/tenant/mixins` extremo.

**Formato API**

```http
POST /tenant/mixins
```

**Solicitud**

La siguiente solicitud crea una nueva mezcla que agrega un `favoriteHotel` campo bajo la `TENANT_ID` Área de nombres de cualquier esquema al que se añada.

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

Una vez que haya creado una mezcla, puede agregarla al esquema de origen haciendo una solicitud PATCH al punto final del `/tenant/schemas/{SCHEMA_ID}` .

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | El `$id` URI con codificación URL o `meta:altId` del esquema de origen. |

**Solicitud**

La siguiente solicitud agrega la mezcla &quot;Hotel Favorito&quot; al esquema &quot;Miembros de la Lealtad&quot;.

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
| `op` | La operación PATCH que se va a realizar. Esta solicitud utiliza la `add` operación. |
| `path` | Ruta al campo esquema donde se agregará el nuevo recurso. Al agregar mezclas a esquemas, el valor debe ser `/allOf/-`. |
| `value.$ref` | El contenido `$id` de la mezcla que se va a añadir. |

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

## Definir campos de identidad principales para ambos esquemas

>[!NOTE] Este paso solo es necesario para esquemas que se habilitarán para su uso en el Perfil [del cliente en tiempo](../../profile/home.md)real. Si no desea que esquema participe en una unión o si sus esquemas ya tienen identidades principales definidas, puede pasar al siguiente paso de [crear un descriptor](#create-descriptor) de identidad de referencia para el esquema de destino.

Para que los esquemas se puedan habilitar para su uso en el Perfil del cliente en tiempo real, deben tener una identidad principal definida. Además, el esquema de destino de una relación debe utilizar su identidad principal como campo de referencia.

A efectos de este tutorial, el esquema de origen ya tiene una identidad principal definida, pero el esquema de destino no. Puede marcar un campo de esquema como un campo de identidad principal creando un descriptor de identidad. Esto se realiza realizando una solicitud POST al `/tenant/descriptors` extremo.

**Formato API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud crea un nuevo descriptor de identidad que define el `hotelId` campo del esquema de destino &quot;Hoteles&quot; como campo de identidad principal.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se va a crear. El `@type` valor de los descriptores de identidad es `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | El `$id` valor del esquema de destino, obtenido en el paso [](#define-schemas)anterior. |
| `xdm:sourceVersion` | Número de versión del esquema. |
| `sourceProperty` | Ruta al campo específico que servirá como identidad principal del esquema. Esta ruta debe comenzar con un &quot;/&quot; y no debe terminar con uno, al tiempo que excluye cualquier Área de nombres de &quot;propiedades&quot;. Por ejemplo, la solicitud anterior utiliza `/_{TENANT_ID}/hotelId` en lugar de `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | Área de nombres de identidad para el campo de identidad. `hotelId` es un valor ECID en este ejemplo, por lo que se utiliza la Área de nombres &quot;ECID&quot;. Consulte la descripción general [de la Área de nombres de](../../identity-service/home.md) identidad para ver una lista de las Áreas de nombres disponibles. |
| `xdm:isPrimary` | Propiedad booleana que determina si el campo de identidad será la identidad principal del esquema. Dado que esta solicitud define una identidad principal, el valor se establece en true. |

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor de identidad recién creado.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Creación de un descriptor de identidad de referencia

Los campos de Esquema deben tener aplicado un descriptor de identidad de referencia si se utilizan como referencia de otros esquemas de una relación. Dado que el `favoriteHotel` campo de &quot;Miembros de la Lealtad&quot; se referirá al `hotelId` campo de &quot;Hoteles&quot;, `hotelId` debe proporcionarse un descriptor de identidad de referencia.

Cree un descriptor de referencia para el esquema de destino realizando una solicitud POST al `/tenant/descriptors` extremo.

**Formato API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud crea un descriptor de referencia para el `hotelId` campo en el esquema de destino &quot;Hoteles&quot;.

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
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `xdm:sourceSchema` | La `$id` URL del esquema de destino. |
| `xdm:sourceVersion` | Número de versión del esquema de destino. |
| `sourceProperty` | Ruta al campo de identidad principal del esquema de destino. |
| `xdm:identityNamespace` | Área de nombres de identidad del campo de referencia. `hotelId` es un valor ECID en este ejemplo, por lo que se utiliza la Área de nombres &quot;ECID&quot;. Consulte la descripción general [de la Área de nombres de](../../identity-service/home.md) identidad para ver una lista de las Áreas de nombres disponibles. |

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor de referencia recién creado para el esquema de destino.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Crear un descriptor de relación {#create-descriptor}

Los descriptores de relación establecen una relación uno a uno entre un esquema de origen y un esquema de destino. Puede crear un nuevo descriptor de relación realizando una solicitud POST al `/tenant/descriptors` extremo.

**Formato API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud crea un nuevo descriptor de relación, con &quot;Miembros de lealtad&quot; como esquema de origen y &quot;Miembros de lealtad heredados&quot; como esquema de destino.

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
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se va a crear. El `@type` valor de los descriptores de relación es `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | La `$id` URL del esquema de origen. |
| `xdm:sourceVersion` | Número de versión del esquema de origen. |
| `sourceProperty`: | Ruta al campo de referencia en el esquema de origen. |
| `xdm:destinationSchema` | La `$id` URL del esquema de destino. |
| `xdm:destinationVersion` | Número de versión del esquema de destino. |
| `destinationProperty`: | Ruta al campo de referencia en el esquema de destino. |

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

Siguiendo este tutorial, ha creado correctamente una relación uno a uno entre dos esquemas. Para obtener más información sobre cómo trabajar con descriptores mediante la API del Registro de Esquemas, consulte la guía [para desarrolladores de](../api/getting-started.md)Esquema Registry. Para ver los pasos sobre cómo definir relaciones de esquema en la interfaz de usuario, consulte el tutorial sobre la [definición de relaciones de esquema mediante el Editor](relationship-ui.md)de Esquemas.