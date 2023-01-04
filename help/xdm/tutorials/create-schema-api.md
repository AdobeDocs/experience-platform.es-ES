---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;esquema;esquema;esquemas;esquemas;crear esquemas
solution: Experience Platform
title: Creación de un esquema mediante la API del Registro de Esquemas
topic-legacy: tutorial
type: Tutorial
description: Este tutorial utiliza la API del Registro de esquemas para guiarle por los pasos necesarios para componer un esquema con una clase estándar.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 2%

---

# Cree un esquema utilizando la variable [!DNL Schema Registry] API

La variable [!DNL Schema Registry] se utiliza para acceder a la variable [!DNL Schema Library] en Adobe Experience Platform. La variable [!DNL Schema Library] contiene los recursos disponibles por Adobe, [!DNL Experience Platform] socios y proveedores cuyas aplicaciones utilice. El registro proporciona una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles.

Este tutorial utiliza la variable [!DNL Schema Registry] API para guiarle por los pasos para componer un esquema con una clase estándar. Si prefiere usar la interfaz de usuario en [!DNL Experience Platform], el [Tutorial del Editor de esquemas](create-schema-ui.md) proporciona instrucciones paso a paso para realizar acciones similares en el editor de esquemas.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Antes de iniciar este tutorial, revise la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar correctamente llamadas a la función [!DNL Schema Registry] API. Esto incluye el `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).

Este tutorial explica los pasos para componer un esquema de miembros de fidelidad que describe los datos relacionados con los miembros de un programa de fidelidad de minorista. Antes de comenzar, es posible que desee previsualizar el [esquema miembro de fidelidad completo](#complete-schema) en el apéndice.

## Componer un esquema con una clase estándar

Un esquema se puede considerar como el modelo para los datos en los que se desea introducir [!DNL Experience Platform]. Cada esquema está compuesto por una clase y cero o más grupos de campos de esquema. En otras palabras, no es necesario agregar un grupo de campos para definir un esquema, pero en la mayoría de los casos se utiliza al menos un grupo de campos.

### Asignar una clase

El proceso de composición del esquema comienza con la selección de una clase. La clase define los aspectos de comportamiento clave de los datos (registro frente a serie temporal), así como los campos mínimos necesarios para describir los datos que se van a introducir.

El esquema que está creando en este tutorial utiliza la variable [!DNL XDM Individual Profile] Clase . [!DNL XDM Individual Profile] es una clase estándar proporcionada por Adobe para definir el comportamiento del registro. Encontrará más información sobre el comportamiento en [conceptos básicos de la composición del esquema](../schema/composition.md).

Para asignar una clase, se realiza una llamada a la API para crear (POST) un nuevo esquema en el contenedor de inquilinos. Esta llamada incluye la clase que el esquema va a implementar. Cada esquema solo puede implementar una clase.

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La solicitud debe incluir un `allOf` que hace referencia a la variable `$id` de una clase. Este atributo define la &quot;clase base&quot; que implementará el esquema. En este ejemplo, la clase base es la [!DNL XDM Individual Profile] Clase . La variable `$id` del [!DNL XDM Individual Profile] se usa como valor de la clase `$ref` en el campo `allOf` a continuación.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "object",
  "title": "Loyalty Members",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile"
    }
  ]
}'
```

**Respuesta**

Una solicitud correcta devuelve el Estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del esquema recién creado, incluido el `$id`, `meta:altIt`y `version`. Estos valores son de solo lectura y los asigna la variable [!DNL Schema Registry].

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551836845496,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Buscar un esquema

Para ver el esquema recién creado, realice una solicitud de consulta (GET) utilizando la variable `meta:altId` o la URL codificada `$id` URI del esquema.

**Formato de API**

```http
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**Respuesta**

El formato de respuesta depende del encabezado Accept enviado con la solicitud. Intente experimentar con diferentes encabezados Accept para ver cuál se adapta mejor a sus necesidades.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551836845496,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Agregar un grupo de campos {#add-a-field-group}

Ahora que se ha creado y confirmado el esquema miembros de lealtad, se pueden añadir grupos de campos.

Hay diferentes grupos de campos estándar disponibles para su uso, según la clase de esquema seleccionada. Cada grupo de campos contiene un `intendedToExtend` campo que define las clases con las que es compatible ese grupo de campos.

Los grupos de campos definen conceptos, como &quot;nombre&quot; o &quot;dirección&quot;, que se pueden reutilizar en cualquier esquema que necesite capturar la misma información.

**Formato de API**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**Solicitud**

Esta solicitud actualiza (PATCH) el esquema de miembros de lealtad para incluir los campos dentro del grupo de campos &quot;profile-person-details&quot;.

Al agregar el grupo de campos &quot;profile-person-details&quot;, el esquema miembros de fidelidad ahora captura información sobre los miembros del programa de fidelidad, como su nombre, apellido y cumpleaños.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**Respuesta**

La respuesta muestra el grupo de campos recién agregado en la variable `meta:extends` matriz y contiene un `$ref` al grupo de campos de la variable `allOf` atributo.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551837227497,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Añadir otro grupo de campos

Ahora puede agregar otro grupo de campos estándar repitiendo los pasos utilizando otro grupo de campos.

>[!TIP]
>
>Vale la pena revisar todos los grupos de campo disponibles para familiarizarse con los campos incluidos en cada uno. Puede enumerar (en GET) todos los grupos de campos disponibles para usar con una clase en particular realizando una solicitud con cada uno de los contenedores &quot;global&quot; y &quot;tenant&quot;, devolviendo solo aquellos grupos de campos en los que el campo &quot;meta:requiredToExtend&quot; coincide con la clase que está utilizando. En este caso, es el [!DNL XDM Individual Profile] Clase, así que la variable [!DNL XDM Individual Profile] `$id` se utiliza:

```http
GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

**Formato de API**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**Solicitud**

Esta solicitud actualiza (PATCH) el esquema miembros de lealtad para incluir los campos dentro del grupo de campos &quot;profile-personal-details&quot;, añadiendo los campos &quot;dirección de inicio&quot;, &quot;dirección de correo electrónico&quot; y &quot;teléfono de inicio&quot; al esquema.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}}
      ]'  
```

**Respuesta**

La respuesta muestra el grupo de campos recién agregado en la variable `meta:extends` matriz y contiene un `$ref` al grupo de campos de la variable `allOf` atributo.

El esquema de miembros de fidelidad ahora debe contener tres `$ref` en la variable `allOf` matriz: &quot;profile&quot;, &quot;profile-person-details&quot; y &quot;profile-personal-details&quot;, como se muestra a continuación.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551837356241,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Definir un nuevo grupo de campos

El esquema miembros de fidelidad debe capturar información que sea única para el programa de fidelidad. Esta información no se incluye en ninguno de los grupos de campos estándar.

La variable [!DNL Schema Registry] para esto, permite definir sus propios grupos de campos dentro del contenedor de inquilinos. Estos grupos de campos son exclusivos de su organización y no son visibles ni editables por nadie fuera de su organización IMS.

Para crear (POST) un nuevo grupo de campos, la solicitud debe incluir un `meta:intendedToExtend` campo que contiene la variable `$id` para las clases base con las que es compatible el grupo de campos, junto con las propiedades que incluye el grupo de campos.

Todas las propiedades personalizadas deben estar anidadas bajo su `TENANT_ID` para evitar conflictos con otros grupos de campos o campos.

**Formato de API**

```http
POST /tenant/fieldgroups
```

**Solicitud**

Esta solicitud crea un nuevo grupo de campos que tiene un objeto &quot;lealtad&quot; que contiene cuatro campos específicos del programa de fidelidad: &quot;loyaltyId&quot;, &quot;loyaltyLevel&quot;, &quot;loyaltyPoints&quot; y &quot;memberSince&quot;.

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Member Details",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Loyalty Program Field Group.",
        "definitions": {
            "loyalty": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "loyalty": {
                      "type": "object",
                      "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier."
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total."
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program."
                        }
                      }
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyalty"
            }
        ]
      }'
```

**Respuesta**

Una solicitud correcta devuelve el Estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del grupo de campos recién creado, incluido el `$id`, `meta:altIt`y `version`. Estos valores son de solo lectura y los asigna la variable [!DNL Schema Registry].

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Field Group.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyalty": {
                            "type": "object",
                            "properties": {
                                "loyaltyId": {
                                    "title": "Loyalty Identifier",
                                    "type": "string",
                                    "description": "Loyalty Identifier.",
                                    "meta:xdmType": "string"
                                },
                                "loyaltyLevel": {
                                    "title": "Loyalty Level",
                                    "type": "string",
                                    "meta:xdmType": "string"
                                },
                                "loyaltyPoints": {
                                    "title": "Loyalty Points",
                                    "type": "integer",
                                    "description": "Loyalty points total.",
                                    "meta:xdmType": "int"
                                },
                                "memberSince": {
                                    "title": "Member Since",
                                    "type": "string",
                                    "format": "date-time",
                                    "description": "Date the member joined the Loyalty Program.",
                                    "meta:xdmType": "date-time"
                                }
                            },
                            "meta:xdmType": "object"
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
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551838135803,
        "repo:lastModifiedDate": 1552078296885,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Agregar grupo de campos personalizados al esquema

Ahora puede seguir los mismos pasos para [adición de un grupo de campos estándar](#add-a-field-group) para añadir este grupo de campos recién creado al esquema.

**Formato de API**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**Solicitud**

Esta solicitud actualiza (PATCH) el esquema de miembros socio para incluir los campos dentro del nuevo grupo de campos &quot;Detalles de miembros socio&quot;.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"}}
      ]'
```

**Respuesta**

Puede ver que el grupo de campos se ha agregado correctamente porque la respuesta ahora muestra el grupo de campos recién agregado en la variable `meta:extends` matriz y contiene una `$ref` al grupo de campos de la variable `allOf` atributo.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.3",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551838484129,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Ver el esquema actual

Ahora puede realizar una solicitud de GET para ver el esquema actual y ver cómo los grupos de campos añadidos han contribuido a la estructura general del esquema.

**Formato de API**

```http
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Respuesta**

Usando la variable `application/vnd.adobe.xed-full+json; version=1` Aceptar encabezado, puede ver el esquema completo mostrando todas las propiedades. Estas propiedades son los campos contribuidos por los grupos de clases y campos que se han utilizado para componer el esquema. En esta respuesta de ejemplo, se han minimizado los atributos de propiedad individuales para el espacio. Puede ver el esquema completo, incluidas todas las propiedades y sus atributos, en la [apéndice](#appendix) al final de este documento.

En `"properties"`, puede ver el `_{TENANT_ID}` espacio de nombres que se creó al agregar el grupo de campos personalizados. Dentro de ese espacio de nombres está el objeto &quot;loyalty&quot; y los campos que se definieron cuando se creó el grupo de campos.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": { },
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Crear un tipo de datos

El grupo de campos Lealtad que ha creado contiene propiedades de lealtad específicas que pueden resultar útiles en otros esquemas. Por ejemplo, los datos se pueden ingerir como parte de un evento de experiencia o ser utilizados por un esquema que implemente una clase diferente. En este caso, tiene sentido guardar la jerarquía de objetos como un tipo de datos para facilitar la reutilización de la definición en otro lugar.

Los tipos de datos permiten definir una jerarquía de objetos una vez y hacer referencia a ella en un campo de la misma manera que lo haría para cualquier otro tipo escalar.

En otras palabras, los tipos de datos permiten el uso coherente de estructuras de varios campos, con más flexibilidad que los grupos de campos, ya que se pueden incluir en cualquier parte de un esquema al agregarlos como el &quot;tipo&quot; de un campo.

**Formato de API**

```http
POST /tenant/datatypes
```

**Solicitud**

La definición de un tipo de datos no requiere `meta:extends` o `meta:intendedToExtend` no es necesario anidar los campos para evitar conflictos.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Details",
        "type": "object",
        "description": "Loyalty Member Details data type",
        "definitions": {
            "loyalty": {
                "type": "object",
                "properties": {
                    "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier."
                    },
                    "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string"
                    },
                    "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total."
                    },
                    "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program."
                    }
                }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyalty"
            }
        ]
      }'
```

**Respuesta**

Una solicitud correcta devuelve el Estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del tipo de datos recién creado, incluido el `$id`, `meta:altIt`y `version`. Estos valores son de solo lectura y los asigna la variable [!DNL Schema Registry].

```JSON
{
    "title": "Loyalty Details",
    "type": "object",
    "description": "Loyalty Member Details data type",
    "definitions": {
        "loyalty": {
            "properties": {
                "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier.",
                    "meta:xdmType": "string"
                },
                "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total.",
                    "meta:xdmType": "int"
                },
                "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program.",
                    "meta:xdmType": "date-time"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.datatypes.49b594dabe6bec545c8a6d1a0991a4dd",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1551840599469,
        "repo:lastModifiedDate": 1551840599469,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Puede realizar una solicitud de búsqueda (GET) utilizando la URL codificada `$id` URI para ver el nuevo tipo de datos directamente. Asegúrese de incluir la variable `version` en el encabezado Accept para una solicitud de consulta.

### Uso del tipo de datos en el esquema

Ahora que se ha creado el tipo de datos Detalles de lealtad , puede actualizar (PATCH) el campo &quot;lealtad&quot; en el grupo de campos que ha creado para hacer referencia al tipo de datos en lugar de los campos que antes estaban allí.

**Formato de API**

```http
PATCH /tenant/fieldgroups/{field group meta:altId or URL encoded $id URI}
```

**Solicitud**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      [
        {
            "op": "replace",
            "path": "/definitions/loyalty/properties/_{TENANT_ID}/properties",
            "value": {
                "loyalty": {
                    "title": "Loyalty",
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "description": "Loyalty Info"
                }
            }
        }
      ]'
```

**Respuesta**

La respuesta ahora incluye una referencia a (`$ref`) al tipo de datos en el objeto &quot;lealtad&quot; en lugar de los campos definidos previamente.

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Field Group.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyalty": {
                            "title": "Loyalty",
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                            "description": "Loyalty Info"
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
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62",
    "version": "1.2",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551838135803,
        "repo:lastModifiedDate": 1552080570051,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Al realizar una solicitud de GET para buscar en el esquema, ahora se muestra la referencia al tipo de datos en &quot;properties/_{TENANT_ID}&quot;, como se ve aquí:

```JSON
"_{TENANT_ID}": {
    "type": "object",
    "meta:xdmType": "object",
    "properties": {
        "loyalty": {
            "title": "Loyalty",
            "description": "Loyalty Info",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
            "properties": {
                "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier.",
                    "meta:xdmType": "string"
                },
                "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total.",
                    "meta:xdmType": "int"
                },
                "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program.",
                    "meta:xdmType": "date-time"
                }
            }
        }
    }
}
```

### Definir un descriptor de identidad

Los esquemas se utilizan para introducir datos en [!DNL Experience Platform]. Estos datos se utilizan finalmente en varios servicios para crear una única vista unificada de un individuo. Para ayudar con este proceso, los campos clave se pueden marcar como &quot;Identidad&quot; y, tras la ingesta de datos, los datos de esos campos se insertan en el &quot;Gráfico de identidad&quot; para esa persona. A continuación, se puede acceder a los datos del gráfico mediante [[!DNL Real-Time Customer Profile]](../../profile/home.md) y otros [!DNL Experience Platform] para proporcionar una vista unida de cada cliente individual.

Los campos que suelen marcarse como &quot;Identidad&quot; incluyen: dirección de correo electrónico, número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es), ID de CRM u otros campos de ID únicos.

Tenga en cuenta cualquier identificador único específico de su organización, ya que también puede ser buenos campos de identidad.

Los descriptores de identidad indican que &quot;sourceProperty&quot; de &quot;sourceSchema&quot; es un identificador único que debe considerarse como &quot;Identity&quot;.

Para obtener más información sobre cómo trabajar con descriptores, consulte la [Guía para desarrolladores de Schema Registry](../api/getting-started.md).

**Formato de API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud define un descriptor de identidad en el campo &quot;loyaltyId&quot;. Esto indica que [!DNL Experience Platform] para utilizar el identificador de miembro del programa de fidelidad único (en este caso, la dirección de correo electrónico del miembro) para ayudar a unir información sobre el individuo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE]
>
>Puede enumerar los valores disponibles de &quot;xdm:namespace&quot; o crear otros nuevos utilizando la variable [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). El valor de &quot;xdm:property&quot; puede ser &quot;xdm:code&quot; o &quot;xdm:id&quot;, en función del &quot;xdm:namespace&quot; utilizado.

**Respuesta**

Una respuesta correcta devuelve el Estado HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del descriptor recién creado, incluido su `@id`. La variable `@id` es un campo de solo lectura asignado por la variable [!DNL Schema Registry] y se utiliza para hacer referencia al descriptor en la API.

```JSON
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
    "xdm:namespace": "Email",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": false,
    "meta:containerId": "tenant",
    "@id": "e52fc732507e5aa9d63d00caa838d3c9fd97aa56"
}
```

## Habilitar esquema para utilizarlo en [!DNL Real-Time Customer Profile] {#profile}

Añadiendo la etiqueta &quot;unión&quot; al `meta:immutableTags` , puede habilitar el esquema miembros de lealtad para que lo use [!DNL Real-Time Customer Profile].

Para obtener más información sobre cómo trabajar con vistas de unión, consulte la sección sobre [sindicatos](../api/unions.md) en el [!DNL Schema Registry] guía para desarrolladores.

### Agregar la etiqueta &quot;unión&quot;

Para que un esquema se incluya en la vista de unión combinada, se debe agregar la etiqueta &quot;unión&quot; al `meta:immutableTags` del esquema. Esto se realiza a través de una solicitud del PATCH para actualizar el esquema y añadir la variable `meta:immutableTags` matriz con el valor &quot;union&quot;.

**Formato de API**

```http
PATCH /tenant/schemas/{meta:altId or the url encoded $id URI}
```

**Solicitud**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Respuesta**

La respuesta muestra que la operación se realizó correctamente y que el esquema ahora contiene un atributo de nivel superior. `meta:immutableTags`, que es una matriz que contiene el valor &quot;union&quot;.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Enumerar esquemas en una unión

Ahora ha agregado correctamente el esquema a la variable [!DNL XDM Individual Profile] unión. Para ver una lista de todos los esquemas que forman parte de la misma unión, puede realizar una solicitud de GET utilizando parámetros de consulta para filtrar la respuesta.

Al usar la variable `property` parámetro de consulta, puede especificar que solo los esquemas que contienen un `meta:immutableTags` campo que tiene un `meta:class` igual a la variable `$id` del [!DNL XDM Individual Profile] se devuelven.

**Formato de API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**Solicitud**

La solicitud de ejemplo siguiente devuelve todos los esquemas que forman parte de la variable [!DNL XDM Individual Profile] unión.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta es una lista filtrada de esquemas que contienen solo aquellos que cumplen ambos requisitos. Recuerde que cuando se utilizan varios parámetros de consulta, se asume una relación AND. El formato de la respuesta de la lista depende del encabezado Accept enviado en la solicitud.

```JSON
{
    "results": [
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
            "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
            "version": "1.4"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```

## Pasos siguientes

Al seguir este tutorial, ha compuesto correctamente un esquema utilizando grupos de campos estándar y un grupo de campos definido. Ahora puede utilizar este esquema para crear un conjunto de datos e introducir datos de registro en Adobe Experience Platform.

El esquema de miembros de fidelidad completo, tal como se ha creado a lo largo de este tutorial, está disponible en el apéndice que se muestra a continuación. Al observar el esquema, puede ver cómo los grupos de campos contribuyen a la estructura general y qué campos están disponibles para la ingesta de datos.

Una vez creado más de un esquema, puede definir las relaciones entre ellos mediante el uso de descriptores de relación. Consulte el tutorial para [definición de una relación entre dos esquemas](relationship-api.md) para obtener más información. Para obtener ejemplos detallados de cómo realizar todas las operaciones (GET, POST, PUT, PATCH y DELETE) en el registro, consulte la [Guía para desarrolladores de Schema Registry](../api/getting-started.md) mientras trabaja con la API.

## Apéndice {#appendix}

La siguiente información complementa el tutorial de API.

## Completar esquema de miembros de fidelidad {#complete-schema}

A lo largo de este tutorial, se compone un esquema para describir los miembros de un programa de fidelidad de minorista.

El esquema implementa el [!DNL XDM Individual Profile] y combina varios grupos de campos; incorporar información sobre los miembros de fidelidad mediante los grupos de campos estándar &quot;Detalles de persona&quot; y &quot;Detalles personales&quot;, así como mediante un grupo de campos &quot;Detalles de fidelidad&quot; que se define durante el tutorial.

A continuación, se muestra el esquema de miembros de lealtad completado en formato JSON:

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {
            "title": "Created by User Identifier",
            "type": "string",
            "description": "User id who has created the entity.",
            "meta:xdmField": "xdm:repositoryCreatedBy",
            "meta:xdmType": "string"
        },
        "repositoryLastModifiedBy": {
            "title": "Modified by User Identifier",
            "type": "string",
            "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
            "meta:xdmField": "xdm:repositoryLastModifiedBy",
            "meta:xdmType": "string"
        },
        "createdByBatchID": {
            "title": "Created by Batch Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
            "meta:xdmField": "xdm:createdByBatchID",
            "meta:xdmType": "string"
        },
        "modifiedByBatchID": {
            "title": "Modified by Batch Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
            "meta:xdmField": "xdm:modifiedByBatchID",
            "meta:xdmType": "string"
        },
        "_repo": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "createDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:immutable": true,
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmField": "repo:createDate",
                    "meta:xdmType": "date-time"
                },
                "modifyDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmField": "repo:modifyDate",
                    "meta:xdmType": "date-time"
                }
            }
        },
        "identityMap": {
            "type": "object",
            "meta:xdmType": "map",
            "meta:xdmField": "xdm:identityMap",
            "additionalProperties": {
                "type": "array",
                "meta:xdmType": "array",
                "items": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                    "properties": {
                        "id": {
                            "title": "Identifier",
                            "type": "string",
                            "description": "Identity of the consumer in the related namespace.",
                            "meta:xdmField": "xdm:id",
                            "meta:xdmType": "string"
                        },
                        "authenticatedState": {
                            "description": "The state this identity is authenticated as for this observed ExperienceEvent.",
                            "type": "string",
                            "default": "ambiguous",
                            "enum": [
                                "ambiguous",
                                "authenticated",
                                "loggedOut"
                            ],
                            "meta:enum": {
                                "ambiguous": "Ambiguous",
                                "authenticated": "User identified by a login or simular action that was valid at the time of the event observation.",
                                "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in."
                            },
                            "meta:xdmField": "xdm:authenticatedState",
                            "meta:xdmType": "string"
                        },
                        "primary": {
                            "title": "Primary",
                            "type": "boolean",
                            "default": false,
                            "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                            "meta:xdmField": "xdm:primary",
                            "meta:xdmType": "boolean"
                        }
                    }
                }
            }
        },
        "_id": {
            "title": "Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "A unique identifier for the record.",
            "meta:xdmField": "@id",
            "meta:xdmType": "string"
        },
        "timeSeriesEvents": {
            "title": "Time-series Events",
            "description": "List of time-series based events that relate to schemas based on record.",
            "type": "array",
            "meta:xdmField": "xdm:timeSeriesEvents",
            "meta:xdmType": "array",
            "items": {
                "type": "object",
                "meta:xdmType": "object",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/data/time-series",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "type": "string",
                        "format": "uri-reference",
                        "description": "A unique identifier for the time-series event.",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "timestamp": {
                        "title": "Timestamp",
                        "type": "string",
                        "format": "date-time",
                        "description": "The time when an event or observation occurred.",
                        "meta:xdmField": "xdm:timestamp",
                        "meta:xdmType": "date-time"
                    },
                    "eventType": {
                        "title": "Event Type",
                        "type": "string",
                        "description": "The primary event type for this timeseries record.",
                        "meta:enum": {
                            "advertising.completes": "Indicates if a timed media asset was watched to completion - this does not necessarily mean the viewer watched the whole video; viewer could have skipped ahead.",
                            "advertising.timePlayed": "Describes the amount of time spent by a user on a specific timed media asset.",
                            "advertising.federated": "Indicates if an experience event was created through data federation (data sharing between customers).",
                            "advertising.clicks": "Click(s) actions on an advertisement.",
                            "advertising.conversions": "A customer pre-defined action(s) which triggers an event for performance evaluation.",
                            "advertising.firstQuartiles": "A digital video ad has played through 25% of its duration at normal speed.",
                            "advertising.impressions": "Impression(s) of an advertisement to an end user with the potential of being viewed.",
                            "advertising.midpoints": "A digital video ad has played through 50% of its duration at normal speed.",
                            "advertising.starts": "A digital video ad has started playing.",
                            "advertising.thirdQuartiles": "A digital video ad has played through 75% of its duration at normal speed.",
                            "web.webpagedetails.pageViews": "View(s) of a webpage has occurred.",
                            "web.webinteraction.linkClicks": "Click of a web-link has occurred.",
                            "commerce.checkouts": "An action during a checkout process of a product list, there can be more than one checkout event if there are multiple steps in a checkout process. If there are multiple steps the event time information and referenced page or experience is used to identify the step individual events represent in order.",
                            "commerce.productListAdds": "Addition of a product to the product list. Example a product is added to a shopping cart.",
                            "commerce.productListOpens": "Initializations of a new product list. Example a shopping cart is created.",
                            "commerce.productListRemovals": "Removal(s) of a product entry from a product list. Example a product is removed from a shopping cart.",
                            "commerce.productListReopens": "A product list that was no longer accessible(abandoned) has been re-activated by the user. Example via a re-marketing activity.",
                            "commerce.productListViews": "View(s) of a product-list has occurred.",
                            "commerce.productViews": "View(s) of a product have occurred.",
                            "commerce.purchases": "An order has been accepted. Purchase is the only required action in a commerce conversion. Purchase must have a product list referenced.",
                            "commerce.saveForLaters": "Product list is saved for future use. Example a product wish list."
                        },
                        "meta:xdmField": "xdm:eventType",
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:xdmField": "xdm:person",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
            "properties": {
                "name": {
                    "title": "Full name",
                    "description": "The person's full name",
                    "meta:xdmField": "xdm:name",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
                    "properties": {
                        "firstName": {
                            "title": "First name",
                            "type": "string",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name.\n\nThe `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmField": "xdm:firstName",
                            "meta:xdmType": "string"
                        },
                        "lastName": {
                            "title": "Last name",
                            "type": "string",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name.\n\nThe `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmField": "xdm:lastName",
                            "meta:xdmType": "string"
                        },
                        "middleName": {
                            "title": "Middle name",
                            "type": "string",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name.",
                            "meta:xdmField": "xdm:middleName",
                            "meta:xdmType": "string"
                        },
                        "courtesyTitle": {
                            "title": "Courtesy title",
                            "type": "string",
                            "description": "Normally an abbreviation of a persons *title*, *honorific*, or *salutation*.\nThe `courtesyTitle` is used in front of full or last name in opening texts.\ne.g Mr. Miss. or Dr J. Smith.\n",
                            "meta:xdmField": "xdm:courtesyTitle",
                            "meta:xdmType": "string"
                        },
                        "fullName": {
                            "title": "Full name",
                            "type": "string",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
                            "meta:xdmField": "xdm:fullName",
                            "meta:xdmType": "string"
                        }
                    }
                },
                "birthDate": {
                    "title": "Birth Date",
                    "type": "string",
                    "format": "date",
                    "description": "The full date a person was born.",
                    "meta:xdmField": "xdm:birthDate",
                    "meta:xdmType": "date"
                },
                "birthDayAndMonth": {
                    "title": "Birth Date",
                    "type": "string",
                    "pattern": "[0-1][0-9]-[0-9][0-9]",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
                    "meta:xdmField": "xdm:birthDayAndMonth",
                    "meta:xdmType": "string"
                },
                "birthYear": {
                    "title": "Birth year",
                    "type": "integer",
                    "description": "The year a person was born including the century (yyyy, e.g 1983).  This field should be used when only the person's age is known, not the full birth date.",
                    "minimum": 1,
                    "maximum": 32767,
                    "meta:xdmField": "xdm:birthYear",
                    "meta:xdmType": "short"
                },
                "gender": {
                    "title": "Gender",
                    "type": "string",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Nonspecific"
                    },
                    "description": "Gender identity of the person.\n",
                    "default": "not_specified",
                    "meta:xdmField": "xdm:gender",
                    "meta:xdmType": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by User Identifier",
                    "type": "string",
                    "description": "User id who has created the entity.",
                    "meta:xdmField": "xdm:repositoryCreatedBy",
                    "meta:xdmType": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by User Identifier",
                    "type": "string",
                    "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy",
                    "meta:xdmType": "string"
                },
                "createdByBatchID": {
                    "title": "Created by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
                    "meta:xdmField": "xdm:createdByBatchID",
                    "meta:xdmType": "string"
                },
                "modifiedByBatchID": {
                    "title": "Modified by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmField": "xdm:modifiedByBatchID",
                    "meta:xdmType": "string"
                },
                "_repo": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:createDate",
                            "meta:xdmType": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:modifyDate",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        },
        "homeAddress": {
            "title": "Home Address",
            "description": "A home postal address.",
            "meta:xdmField": "xdm:homeAddress",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmField": "@id",
                    "meta:xdmType": "string"
                },
                "_schema": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmField": "schema:description",
                            "meta:xdmType": "string"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmField": "schema:latitude",
                            "meta:xdmType": "number"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmField": "schema:longitude",
                            "meta:xdmType": "number"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmField": "schema:elevation",
                            "meta:xdmType": "number"
                        }
                    }
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmField": "xdm:countryCode",
                    "meta:xdmType": "string"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the ISO 3166-2 (country and subdivision) standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmField": "xdm:stateProvince",
                    "meta:xdmType": "string"
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmField": "xdm:city",
                    "meta:xdmType": "string"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmField": "xdm:postalCode",
                    "meta:xdmType": "string"
                },
                "dmaID": {
                    "title": "Designated Market Area",
                    "type": "integer",
                    "description": "The Nielsen Media Research designated market area.",
                    "meta:xdmField": "xdm:dmaID",
                    "meta:xdmType": "int"
                },
                "msaID": {
                    "title": "Metropolitan Statistical Area",
                    "type": "integer",
                    "description": "The Metropolitan Statistical Area in the USA where the observation occurred.",
                    "meta:xdmField": "xdm:msaID",
                    "meta:xdmType": "int"
                },
                "repositoryCreatedBy": {
                    "title": "Created by User Identifier",
                    "type": "string",
                    "description": "User id who has created the entity.",
                    "meta:xdmField": "xdm:repositoryCreatedBy",
                    "meta:xdmType": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by User Identifier",
                    "type": "string",
                    "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy",
                    "meta:xdmType": "string"
                },
                "createdByBatchID": {
                    "title": "Created by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
                    "meta:xdmField": "xdm:createdByBatchID",
                    "meta:xdmType": "string"
                },
                "modifiedByBatchID": {
                    "title": "Modified by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmField": "xdm:modifiedByBatchID",
                    "meta:xdmType": "string"
                },
                "_repo": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:createDate",
                            "meta:xdmType": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:modifyDate",
                            "meta:xdmType": "date-time"
                        }
                    }
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A Profile can have only one `primary` address at a given point of time.\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmField": "xdm:label",
                    "meta:xdmType": "string"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary Street level information, apartment number, street number and street name.",
                    "meta:xdmField": "xdm:street1",
                    "meta:xdmType": "string"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmField": "xdm:street2",
                    "meta:xdmType": "string"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmField": "xdm:street3",
                    "meta:xdmType": "string"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmField": "xdm:street4",
                    "meta:xdmType": "string"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmField": "xdm:region",
                    "meta:xdmType": "string"
                },
                "postOfficeBox": {
                    "title": "Post Office Box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmField": "xdm:postOfficeBox",
                    "meta:xdmType": "string"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmField": "xdm:country",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending Verification",
                        "denylist": "Deny List",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "lastVerifiedDate": {
                    "title": "Last Verified Date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still belonging to the person.",
                    "meta:xdmField": "xdm:lastVerifiedDate",
                    "meta:xdmType": "date"
                }
            }
        },
        "personalEmail": {
            "title": "Personal Email",
            "description": "A personal email address.",
            "meta:xdmField": "xdm:personalEmail",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "address": {
                    "title": "Address",
                    "type": "string",
                    "format": "email",
                    "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                    "meta:xdmField": "xdm:address",
                    "meta:xdmType": "string"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Additional display information that maybe available, e.g MS Outlook rich address controls display 'John Smith smithjr@company.uk', the 'John Smith' part is data that would be placed in the label.",
                    "meta:xdmField": "xdm:label",
                    "meta:xdmType": "string"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The way the account relates to the person. e.g 'work' or 'personal'",
                    "meta:enum": {
                        "unknown": "Unknown",
                        "personal": "Personal",
                        "work": "Work",
                        "education": "Education"
                    },
                    "meta:xdmField": "xdm:type",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the email address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending Verification",
                        "denylist": "Deny List",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                }
            }
        },
        "homePhone": {
            "title": "Home Phone",
            "description": "Home phone number.",
            "meta:xdmField": "xdm:homePhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "denylist": "Deny List",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "mobilePhone": {
            "title": "Mobile Phone",
            "description": "Mobile phone number.",
            "meta:xdmField": "xdm:mobilePhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "denylist": "Deny List",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "faxPhone": {
            "title": "Fax Phone",
            "description": "Fax phone number.",
            "meta:xdmField": "xdm:faxPhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "denylist": "Deny List",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
