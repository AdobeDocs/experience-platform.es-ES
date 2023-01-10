---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;esquema;esquema;esquemas;esquemas;crear esquemas
solution: Experience Platform
title: Creación de un esquema mediante la API del Registro de Esquemas
type: Tutorial
description: Este tutorial utiliza la API del Registro de esquemas para guiarle por los pasos necesarios para componer un esquema con una clase estándar.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 6a69dd0bf8945dfef5ac73ee11a0ed6603ee4b9b
workflow-type: tm+mt
source-wordcount: '2558'
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

Antes de iniciar este tutorial, revise la [guía para desarrolladores](../api/getting-started.md) para obtener información importante que necesita conocer para realizar correctamente llamadas a la función [!DNL Schema Registry] API. Esto incluye el `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al `Accept` y sus posibles valores).

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
    "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310304048,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_tenantId"
}
```

### Buscar un esquema

Para ver el esquema recién creado, realice una solicitud de consulta (GET) utilizando la variable `meta:altId` o la URL codificada `$id` URI del esquema.

**Formato de API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema que desea buscar. |

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

El formato de respuesta depende de la variable `Accept` encabezado enviado con la solicitud. Intente experimentar con diferentes `Accept` encabezados para ver cuál se adapta mejor a sus necesidades.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310304048,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:allFieldAccess": true
}
```

### Agregar un grupo de campos {#add-a-field-group}

Ahora que se ha creado y confirmado el esquema miembros de lealtad, se pueden añadir grupos de campos.

Hay diferentes grupos de campos estándar disponibles para su uso, según la clase de esquema seleccionada. Cada grupo de campos contiene un `intendedToExtend` campo que define las clases con las que es compatible ese grupo de campos.

Los grupos de campos definen conceptos, como &quot;nombre&quot; o &quot;dirección&quot;, que se pueden reutilizar en cualquier esquema que necesite capturar la misma información.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema al que va a añadir el grupo de campos. |

**Solicitud**

Esta solicitud actualiza el esquema de miembros de lealtad para incluir los campos dentro de la variable [[!UICONTROL Detalles demográficos] grupo de campos](../field-groups/profile/demographic-details.md) (`profile-person-details`).

Al agregar la variable `profile-person-details` grupo de campos, el esquema miembros de lealtad ahora captura información demográfica para los miembros del programa de fidelidad como su nombre, apellido y cumpleaños.

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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310912096,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Agregar más grupos de campos

Los esquemas de miembros de lealtad requieren dos grupos de campos estándar más, que se pueden agregar repitiendo los pasos que se dan con otro grupo de campos.

>[!TIP]
>
>Vale la pena revisar todos los grupos de campo disponibles para familiarizarse con los campos incluidos en cada uno. Puede enumerar (en GET) todos los grupos de campos disponibles para usar con una clase en particular realizando una solicitud con cada uno de los contenedores &quot;global&quot; y &quot;tenant&quot;, devolviendo solo aquellos grupos de campos en los que el campo &quot;meta:requiredToExtend&quot; coincide con la clase que está utilizando. En este caso, es el [!DNL XDM Individual Profile] Clase, así que la variable [!DNL XDM Individual Profile] `$id` se utiliza:
>
>
```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema que está actualizando. |

**Solicitud**

Esta solicitud actualiza el esquema de miembros de lealtad para incluir los campos dentro de los siguientes grupos de campos estándar:

* [[!UICONTROL Detalles de contacto personal]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`): Agrega información de contacto, como la dirección de inicio, la dirección de correo electrónico y el teléfono de inicio.
* [[!UICONTROL Detalles de fidelidad]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`): Agrega información de contacto, como la dirección de inicio, la dirección de correo electrónico y el teléfono de inicio.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**Respuesta**

La respuesta muestra los grupos de campos recién añadidos en la variable `meta:extends` matriz y contiene un `$ref` al grupo de campos de la variable `allOf` atributo.

El esquema de miembros de lealtad ahora debe contener cuatro `$ref` en la variable `allOf` matriz: `profile`, `profile-person-details`, `profile-personal-details`y `profile-loyalty-details` como se muestra a continuación.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.2",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673311559934,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Definir un nuevo grupo de campos

Mientras que el estándar [!UICONTROL Detalles de fidelidad] grupo de campos proporciona al esquema campos útiles relacionados con la lealtad; hay campos de lealtad adicionales que no se incluyen en ningún grupo de campos estándar.

Para agregar estos campos, puede definir sus propios grupos de campos personalizados dentro de la variable `tenant` contenedor. Estos grupos de campos son exclusivos de su organización y no son visibles ni editables por nadie fuera de su organización.

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
        "title": "Loyalty Tier",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
            "loyaltyTier": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "loyaltyTier": {
                      "type": "object",
                      "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier."
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier."
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier."
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
            "$ref": "#/definitions/loyaltyTier"
            }
        ]
    }'
```

**Respuesta**

Una solicitud correcta devuelve el Estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del grupo de campos recién creado, incluido el `$id`, `meta:altIt`y `version`. Estos valores son de solo lectura y los asigna la variable [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Captures info about the current loyalty tier of a customer.",
    "definitions": {
        "loyaltyTier": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyTier": {
                            "type": "object",
                            "properties": {
                                "id": {
                                    "title": "Loyalty Tier Identifier",
                                    "type": "string",
                                    "description": "Loyalty Tier Identifier.",
                                    "meta:xdmType": "string"
                                },
                                "effectiveDate": {
                                    "title": "Effective Date",
                                    "type": "string",
                                    "format": "date-time",
                                    "description": "Date the member joined their current loyalty tier.",
                                    "meta:xdmType": "date-time"
                                },
                                "currentThreshold": {
                                    "title": "Current Point Threshold",
                                    "type": "integer",
                                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                                    "meta:xdmType": "int"
                                },
                                "nextThreshold": {
                                    "title": "Next Point Threshold",
                                    "type": "integer",
                                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                                    "meta:xdmType": "int"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673313004645,
        "repo:lastModifiedDate": 1673313004645,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Añadir el grupo de campos personalizados al esquema

Ahora puede seguir los mismos pasos para [adición de un grupo de campos estándar](#add-a-field-group) para añadir este grupo de campos recién creado al esquema.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema. |

**Solicitud**

Esta solicitud actualiza (PATCH) el esquema de miembros de fidelidad para incluir los campos dentro del nuevo grupo de campos &quot;Nivel de fidelidad&quot;.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**Respuesta**

Puede ver que el grupo de campos se ha agregado correctamente porque la respuesta ahora muestra el grupo de campos recién agregado en la variable `meta:extends` matriz y contiene una `$ref` al grupo de campos de la variable `allOf` atributo.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Ver el esquema actual

Ahora puede realizar una solicitud de GET para ver el esquema actual y ver cómo los grupos de campos añadidos han contribuido a la estructura general del esquema.

**Formato de API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema. |

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Respuesta**

Usando la variable `application/vnd.adobe.xed-full+json; version=1` `Accept` , puede ver el esquema completo que muestra todas las propiedades. Estas propiedades son los campos contribuidos por los grupos de clases y campos que se han utilizado para componer el esquema. En la respuesta de ejemplo siguiente, solo se muestran los campos agregados recientemente para el espacio. Puede ver el esquema completo, incluidas todas las propiedades y sus atributos, en la [apéndice](#appendix) al final de este documento.

En `"properties"`, puede ver el `_{TENANT_ID}` espacio de nombres que se creó al agregar el grupo de campos personalizados. Dentro de ese espacio de nombres está el objeto &quot;loyalty&quot; y los campos que se definieron cuando se creó el grupo de campos.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "properties": {
        "_{TENANT_ID}": {
            "type": "object",
            "properties": {
                "loyaltyTier": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier.",
                            "meta:xdmType": "string"
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier.",
                            "meta:xdmType": "date-time"
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                            "meta:xdmType": "int"
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                            "meta:xdmType": "int"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "meta:xdmType": "object"
        }
    },
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:allFieldAccess": true
}
```

### Crear un tipo de datos

El grupo de campos Nivel de fidelidad que ha creado contiene propiedades específicas que pueden resultar útiles en otros esquemas. Por ejemplo, los datos se pueden ingerir como parte de un evento de experiencia o ser utilizados por un esquema que implemente una clase diferente. En este caso, tiene sentido guardar la jerarquía de objetos como un tipo de datos para facilitar la reutilización de la definición en otro lugar.

Los tipos de datos permiten definir una jerarquía de objetos una vez y hacer referencia a ella en un campo de la misma manera que lo haría para cualquier otro tipo escalar.

En otras palabras, los tipos de datos permiten el uso coherente de estructuras de varios campos, con más flexibilidad que los grupos de campos, ya que se pueden incluir en cualquier parte de un esquema al agregarlos como el &quot;tipo&quot; de un campo.

**Formato de API**

```http
POST /tenant/datatypes
```

**Solicitud**

La definición de un tipo de datos no requiere `meta:extends` o `meta:intendedToExtend` no es necesario anidar los campos, campos y en el ID del inquilino para evitar conflictos.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
            "loyaltyTier": {
                "type": "object",
                "properties": {
                    "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                    },
                    "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                    },
                    "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                    },
                    "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                    }
                }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyaltyTier"
            }
        ]
      }'
```

**Respuesta**

Una solicitud correcta devuelve el Estado de respuesta HTTP 201 (Creado) con un cuerpo de respuesta que contiene los detalles del tipo de datos recién creado, incluido el `$id`, `meta:altIt`y `version`. Estos valores son de solo lectura y los asigna la variable [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
    "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
    "meta:resourceType": "datatypes",
    "version": "1.0",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Loyalty Tier data type",
    "definitions": {
        "loyaltyTier": {
            "type": "object",
            "properties": {
                "id": {
                    "title": "Loyalty Tier Identifier",
                    "type": "string",
                    "description": "Loyalty Tier Identifier.",
                    "meta:xdmType": "string"
                },
                "effectiveDate": {
                    "title": "Effective Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined their current loyalty tier.",
                    "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                    "title": "Current Point Threshold",
                    "type": "integer",
                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                    "meta:xdmType": "int"
                },
                "nextThreshold": {
                    "title": "Next Point Threshold",
                    "type": "integer",
                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                    "meta:xdmType": "int"
                }
            },
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673378256699,
        "repo:lastModifiedDate": 1673378256699,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Puede realizar una solicitud de búsqueda (GET) utilizando la URL codificada `$id` URI para ver el nuevo tipo de datos directamente. Asegúrese de incluir la variable `version` en su `Accept` para una solicitud de consulta.

### Uso del tipo de datos en el esquema

Ahora que se ha creado el tipo de datos Nivel de fidelidad, puede actualizar (PATCH) el `loyaltyTier` del grupo de campos que ha creado para hacer referencia al tipo de datos en lugar de los campos que anteriormente estaban allí.

**Formato de API**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{FIELD_GROUP_ID}` | La variable `meta:altId` o URL codificada `$id` del grupo de campos que se va a actualizar. |

**Solicitud**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "op": "replace",
            "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
            "value": {
                "loyaltyTier": {
                    "title": "Loyalty Tier",
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
                    "description": "Loyalty tier info"
                }
            }
        }
    ]
```

**Respuesta**

La respuesta ahora incluye una referencia a (`$ref`) al tipo de datos en el objeto &quot;lealtad&quot; en lugar de los campos definidos previamente.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:resourceType": "mixins",
    "version": "1.1",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Captures info about the current loyalty tier of a customer.",
    "definitions": {
        "loyaltyTier": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyTier": {
                            "title": "Loyalty Tier",
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
                            "description": "Loyalty tier info",
                            "type": "object",
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673313004645,
        "repo:lastModifiedDate": 1673378970276,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

Si realiza una solicitud de GET para buscar el esquema ahora, la variable `loyaltyTier` muestra la referencia al tipo de datos en `meta:referencedFrom`:

```JSON
"_{TENANT_ID}": {
    "type": "object",
    "meta:xdmType": "object",
    "properties": {
        "loyaltyTier": {
            "title": "Loyalty Tier",
            "description": "Loyalty tier info",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "id": {
                    "title": "Loyalty Tier Identifier",
                    "type": "string",
                    "description": "Loyalty Tier Identifier.",
                    "meta:xdmType": "string"
                },
                "effectiveDate": {
                    "title": "Effective Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined their current loyalty tier.",
                    "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                    "title": "Current Point Threshold",
                    "type": "integer",
                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                    "meta:xdmType": "int"
                },
                "nextThreshold": {
                    "title": "Next Point Threshold",
                    "type": "integer",
                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                    "meta:xdmType": "int"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
    }
}
```

### Definir un descriptor de identidad

Los esquemas se utilizan para introducir datos en [!DNL Experience Platform]. Estos datos se utilizan finalmente en varios servicios para crear una única vista unificada de un individuo. Para ayudar con este proceso, los campos clave se pueden marcar como &quot;Identidad&quot; y, tras la ingesta de datos, los datos de esos campos se insertan en el &quot;Gráfico de identidad&quot; para esa persona. A continuación, se puede acceder a los datos del gráfico mediante [[!DNL Real-Time Customer Profile]](../../profile/home.md) y otros [!DNL Experience Platform] para proporcionar una vista unida de cada cliente individual.

Los campos que suelen marcarse como &quot;Identidad&quot; incluyen: dirección de correo electrónico, número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es), ID de CRM u otros campos de ID únicos. Tenga en cuenta cualquier identificador único específico de su organización, ya que también puede ser buenos campos de identidad.

Los descriptores de identidad indican que la variable `sourceProperty` del `sourceSchema` es un identificador único que debe considerarse como una identidad.

Para obtener más información sobre cómo trabajar con descriptores, consulte la [Guía para desarrolladores de Schema Registry](../api/getting-started.md).

**Formato de API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud define un descriptor de identidad en la variable `personalEmail.address` para el esquema miembros de lealtad. Esto indica que [!DNL Experience Platform] para utilizar la dirección de correo electrónico del miembro socio como identificador para ayudar a unir información sobre el individuo. Esta llamada también establece este campo como la identidad principal para el esquema estableciendo `xdm:isPrimary` a `true`, que es un requisito para [activación del esquema para su uso en Perfil del cliente en tiempo real](#profile).

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
    "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/personalEmail/address",
    "imsOrg": "{ORG_ID}",
    "version": "1",
    "xdm:namespace": "Email",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

## Habilitar esquema para utilizarlo en [!DNL Real-Time Customer Profile] {#profile}

Una vez que el esquema tiene aplicado un descriptor de identidad principal, puede habilitar el esquema de miembros de lealtad para que lo utilice [!DNL Real-Time Customer Profile] añadiendo un `union` para `meta:immutableTags` atributo.

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con vistas de unión, consulte la sección sobre [sindicatos](../api/unions.md) en el [!DNL Schema Registry] guía para desarrolladores.

### Agregue un `union` etiqueta

Para que un esquema se incluya en la vista de unión combinada, la variable `union` debe agregarse a la variable `meta:immutableTags` del esquema. Esto se realiza mediante una solicitud del PATCH para actualizar el esquema y añadir una `meta:immutableTags` matriz con un valor de `union`.

**Formato de API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SCHEMA_ID}` | La variable `meta:altId` o con codificación de URL `$id` del esquema que está habilitando para Perfil. |

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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673380280074,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:descriptorStatus": {
        "result": []
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

La respuesta es una lista filtrada de esquemas que contienen solo aquellos que cumplen ambos requisitos. Recuerde que cuando se utilizan varios parámetros de consulta, se asume una relación AND. El formato de la respuesta de la lista depende del `Accept` encabezado enviado en la solicitud.

```JSON
{
    "results": [
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
            "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
            "version": "1.2",
            "title": "Profile Schema"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
            "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
            "version": "1.3",
            "title": "CRM Onboarding"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
            "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
            "version": "1.1",
            "title": "Profile consents"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
            "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
            "version": "1.4",
            "title": "Loyalty Members"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 4
    },
    "_links": {
        "next": null,
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

El esquema implementa el [!DNL XDM Individual Profile] y combina varios grupos de campos. Captura información sobre los miembros de fidelidad usando el estándar [!DNL Demographic Details], [!UICONTROL Detalles de contacto personal]y [!UICONTROL Detalles de fidelidad] grupos de campos, así como a través de un grupo de campos de nivel de lealtad personalizado que se define durante el tutorial.

A continuación, se muestra el esquema de miembros de lealtad completado en formato JSON:

+++Ver esquema completo

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "properties": {
        "_{TENANT_ID}": {
            "type": "object",
            "properties": {
                "loyaltyTier": {
                    "title": "Loyalty Tier",
                    "description": "Loyalty tier info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier.",
                            "meta:xdmType": "string"
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier.",
                            "meta:xdmType": "date-time"
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                            "meta:xdmType": "int"
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                            "meta:xdmType": "int"
                        }
                    },
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
                }
            },
            "meta:xdmType": "object"
        },
        "_id": {
            "title": "Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "A unique identifier for the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "@id"
        },
        "_repo": {
            "properties": {
                "createDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:immutable": true,
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "repo:createDate"
                },
                "modifyDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "repo:modifyDate"
                }
            },
            "type": "object",
            "meta:xdmType": "object",
            "meta:xedConverted": true
        },
        "billingAddress": {
            "title": "Billing Address",
            "description": "Billing postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:billingAddress"
        },
        "createdByBatchID": {
            "title": "Created by batch identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The dataset files in Catalog which has been originating the creation of the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:createdByBatchID"
        },
        "faxPhone": {
            "title": "Fax Phone",
            "description": "Fax phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:faxPhone"
        },
        "homeAddress": {
            "title": "Home Address",
            "description": "A home postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:homeAddress"
        },
        "homePhone": {
            "title": "Home Phone",
            "description": "Home phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:homePhone"
        },
        "loyalty": {
            "type": "object",
            "description": "Captures details related to the customer's loyalty rewards.",
            "properties": {
                "joinDate": {
                    "title": "Program Join Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date which the visitor registered for the loyalty program.",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "xdm:joinDate"
                },
                "loyaltyID": {
                    "title": "Program ID",
                    "type": "array",
                    "items": {
                        "type": "string",
                        "meta:xdmType": "string"
                    },
                    "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
                    "meta:xdmType": "array",
                    "meta:xdmField": "xdm:loyaltyID"
                },
                "points": {
                    "title": "Program Points Balance",
                    "type": "number",
                    "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
                    "meta:xdmType": "number",
                    "meta:xdmField": "xdm:points"
                },
                "pointsExpiration": {
                    "title": "Points Expiration",
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "pointsExpirationDate": {
                                "type": "string",
                                "format": "date-time",
                                "description": "Date on which the given portion of the loyalty points expire.",
                                "meta:xdmType": "date-time",
                                "meta:xdmField": "xdm:pointsExpirationDate"
                            },
                            "pointsExpiring": {
                                "title": "Points Expiring",
                                "type": "number",
                                "description": "Point balance expiring as of the associated expiration date.",
                                "meta:xdmType": "number",
                                "meta:xdmField": "xdm:pointsExpiring"
                            }
                        },
                        "meta:xdmType": "object"
                    },
                    "meta:xdmType": "array",
                    "meta:xdmField": "xdm:pointsExpiration"
                },
                "pointsRedeemed": {
                    "title": "Points Redeemed",
                    "type": "number",
                    "description": "Amount of points applied toward a purchase or otherwise redeemed.",
                    "meta:xdmType": "number",
                    "meta:xdmField": "xdm:pointsRedeemed"
                },
                "program": {
                    "title": "Program Name",
                    "type": "string",
                    "description": "This should define the loyalty progam in which a visitor is enrolled.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:program"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "tier": {
                    "title": "Tier",
                    "type": "string",
                    "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:tier"
                },
                "upgradeDate": {
                    "title": "Program Name",
                    "type": "string",
                    "description": "Date which the customer was upgraded to the next tier level.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:upgradeDate"
                }
            },
            "meta:xdmType": "object",
            "meta:xdmField": "xdm:loyalty"
        },
        "mailingAddress": {
            "title": "Mailing Address",
            "description": "Mailing postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:mailingAddress"
        },
        "mobilePhone": {
            "title": "Mobile Phone",
            "description": "Mobile phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:mobilePhone"
        },
        "modifiedByBatchID": {
            "title": "Modified by batch identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "title": "Birth date(YYYY-MM-DD)",
                    "type": "string",
                    "format": "date",
                    "description": "The full date a person was born.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:birthDate"
                },
                "birthDayAndMonth": {
                    "title": "Birth date (MM-DD)",
                    "type": "string",
                    "pattern": "[0-1][0-9]-[0-9][0-9]",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:birthDayAndMonth"
                },
                "birthYear": {
                    "title": "Birth year",
                    "type": "integer",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
                    "minimum": 1,
                    "maximum": 32767,
                    "meta:xdmType": "short",
                    "meta:xdmField": "xdm:birthYear"
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
                        "non_specific": "Non-specific"
                    },
                    "description": "Gender identity of the person.\n",
                    "default": "not_specified",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:gender"
                },
                "maritalStatus": {
                    "title": "Marital Status",
                    "type": "string",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "married": "Married",
                        "single": "Single",
                        "divorced": "Divorced",
                        "widowed": "Widowed",
                        "not_specified": "Not Specified"
                    },
                    "description": "Describes a person's relationship with a significant other.",
                    "default": "not_specified",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:maritalStatus"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "title": "Courtesy title",
                            "type": "string",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:courtesyTitle"
                        },
                        "firstName": {
                            "title": "First name",
                            "type": "string",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:firstName"
                        },
                        "fullName": {
                            "title": "Full name",
                            "type": "string",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:fullName"
                        },
                        "lastName": {
                            "title": "Last name",
                            "type": "string",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:lastName"
                        },
                        "middleName": {
                            "title": "Middle name",
                            "type": "string",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:middleName"
                        },
                        "suffix": {
                            "title": "Suffix",
                            "type": "string",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:suffix"
                        }
                    },
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
                    "meta:xdmField": "xdm:name"
                },
                "nationality": {
                    "title": "Nationality",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:nationality"
                },
                "taxId": {
                    "title": "Tax ID",
                    "type": "string",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:taxId"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The type of individual in different business contexts like B2C.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:type"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
            "meta:xdmField": "xdm:person"
        },
        "personID": {
            "title": "Person ID",
            "description": "Unique identifier of Person/Profile fragment.",
            "type": "string",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:personID"
        },
        "personalEmail": {
            "title": "Personal Email",
            "description": "A personal email address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "address": {
                    "title": "Address",
                    "type": "string",
                    "format": "email",
                    "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:address",
                    "minLength": 1
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the email address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The way the account relates to the person for example 'work' or 'personal'.",
                    "meta:enum": {
                        "unknown": "Unknown",
                        "personal": "Personal",
                        "work": "Work",
                        "education": "Education"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:type"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
            "meta:xdmField": "xdm:personalEmail",
            "required": [
                "address"
            ]
        },
        "repositoryCreatedBy": {
            "title": "Created by user identifier",
            "type": "string",
            "description": "User ID of who created the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
            "title": "Modified by user identifier",
            "type": "string",
            "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "shippingAddress": {
            "title": "Shipping Address",
            "description": "Shipping postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:shippingAddress"
        }
    },
    "required": [
        "personalEmail"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673380280074,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:allFieldAccess": true
}
```

+++
