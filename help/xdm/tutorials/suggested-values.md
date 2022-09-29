---
title: Administrar los valores sugeridos en la API
description: Aprenda a añadir valores sugeridos a un campo de cadena en la API del Registro de esquemas.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 2f916ea4b05ca67c2b9e603512d732a2a3f7a3b2
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Administrar valores sugeridos en la API

Para cualquier campo de cadena del Modelo de datos de experiencia (XDM), puede definir una **enum** que restringe los valores que el campo puede introducir a un conjunto predefinido. Si intenta introducir datos en un campo de enumeración y el valor no coincide con ninguno de los definidos en su configuración, se denegará la ingesta.

A diferencia de las enumeraciones, agregue **valores sugeridos** a un campo de cadena no restringe los valores que puede introducir. En su lugar, los valores sugeridos afectan a los valores predefinidos disponibles en la variable [Interfaz de usuario de segmentación](../../segmentation/ui/overview.md) al incluir el campo de cadena como atributo.

>[!NOTE]
>
>Se produce un retraso aproximado de cinco minutos para que los valores sugeridos actualizados de un campo se reflejen en la interfaz de usuario de segmentación.

Esta guía explica cómo administrar los valores sugeridos mediante el [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Para ver los pasos sobre cómo hacerlo en la interfaz de usuario de Adobe Experience Platform, consulte la [Guía de la interfaz de usuario sobre enumeraciones y valores sugeridos](../ui/fields/enum.md).

## Requisitos previos

En esta guía se asume que está familiarizado con los elementos de la composición de esquema en XDM y cómo utilizar la API de registro de esquema para crear y editar recursos XDM. Consulte la siguiente documentación si necesita una introducción:

* [Aspectos básicos de la composición del esquema](../schema/composition.md)
* [Guía de API del Registro de Esquemas](../api/overview.md)

También es muy recomendable que revise la [reglas de evolución para enumeraciones y valores sugeridos](../ui/fields/enum.md#evolution) si va a actualizar campos existentes. Si está administrando valores sugeridos para esquemas que participan en una unión, consulte la [reglas para combinar enumeraciones y valores sugeridos](../ui/fields/enum.md#merging).

## Composición

En la API, los valores restringidos para un **enum** los campos se representan mediante un `enum` matriz, mientras que un `meta:enum` proporciona nombres descriptivos para mostrar para esos valores:

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Para los campos enum, el Registro de esquemas no permite `meta:enum` se extenderán más allá de los valores previstos en el `enum`, ya que intentar introducir valores de cadena fuera de esas restricciones no pasaría la validación.

También puede definir un campo de cadena que no contenga `enum` y solo usa el `meta:enum` objeto que se va a denotar **valores sugeridos**:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Dado que la cadena no tiene un valor `enum` matriz para definir restricciones, su `meta:enum` se puede ampliar para incluir nuevos valores.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Añadir valores sugeridos a un campo estándar {#add-suggested-standard}

Para ampliar el `meta:enum` de un campo de cadena estándar, puede crear un [descriptor de nombre descriptivo](../api/descriptors.md#friendly-name) para el campo en cuestión en un esquema determinado.

>[!NOTE]
>
>Los valores sugeridos para campos de cadena solo se pueden añadir en el nivel de esquema. En otras palabras, ampliar el `meta:enum` de un campo estándar en un esquema no afecta a otros esquemas que emplean el mismo campo estándar.

La siguiente solicitud agrega valores sugeridos al estándar `eventType` (proporcionado por la variable [Clase XDM ExperienceEvent](../classes/experienceevent.md)) para el esquema identificado en `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

Después de aplicar el descriptor, el Registro de esquemas responde con lo siguiente al recuperar el esquema (respuesta truncada para el espacio):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Si el campo estándar ya contiene valores en `meta:enum`, los nuevos valores del descriptor no sobrescriben los campos existentes y se añaden en su lugar:
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## Administrar valores sugeridos para un campo personalizado {#suggested-custom}

Para administrar el `meta:enum` de un campo personalizado, se puede actualizar la clase principal, el grupo de campos o el tipo de datos del campo mediante una solicitud del PATCH.

>[!WARNING]
>
>A diferencia de los campos estándar, la actualización de la variable `meta:enum` de un campo personalizado afecta a todos los demás esquemas que emplean ese campo. Si no desea que los cambios se propaguen entre esquemas, considere la posibilidad de crear un nuevo recurso personalizado en su lugar:
>
>* [Crear una clase personalizada](../api/classes.md#create)
>* [Crear un grupo de campos personalizado](../api/field-groups.md#create)
>* [Crear un tipo de datos personalizado](../api/data-types.md#create)


La siguiente solicitud actualiza el `meta:enum` de un campo &quot;nivel de lealtad&quot; proporcionado por un tipo de datos personalizado:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

Después de aplicar el cambio, el Registro de esquemas responde con lo siguiente al recuperar el esquema (respuesta truncada para el espacio):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Pasos siguientes

Esta guía explica cómo administrar los valores sugeridos para los campos de cadena en la API del Registro de esquemas. Consulte la guía de [definición de campos personalizados en la API](./custom-fields-api.md) para obtener más información sobre cómo crear distintos tipos de campos.
