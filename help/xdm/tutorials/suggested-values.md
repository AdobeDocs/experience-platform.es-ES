---
title: Agregar valores sugeridos a un campo
description: Aprenda a añadir valores sugeridos a un campo de cadena en la API del Registro de esquemas.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Añadir valores sugeridos a un campo

En el Modelo de datos de experiencia (XDM), un campo de enumeración representa un campo de cadena limitado a un subconjunto de valores predefinido. Los campos de enumeración pueden proporcionar una validación para garantizar que los datos introducidos se ajustan a un conjunto de valores aceptados. Sin embargo, también puede definir un conjunto de valores sugeridos para un campo de cadena sin aplicarlos como restricciones.

En el [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/), los valores restringidos para un campo de enumeración se representan mediante un `enum` matriz, mientras que un `meta:enum` proporciona nombres descriptivos para mostrar para esos valores:

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

También puede definir un campo de cadena que no contenga `enum` y solo usa el `meta:enum` para denotar valores sugeridos:

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

Dado que la cadena no tiene un valor `enum` matriz para definir restricciones, su `meta:enum` se puede ampliar para incluir nuevos valores. Este tutorial explica cómo agregar valores sugeridos a campos de cadena estándar y personalizados en la API del Registro de esquemas.

## Requisitos previos

En esta guía se asume que está familiarizado con los elementos de la composición de esquema en XDM y cómo utilizar la API de registro de esquema para crear y editar recursos XDM. Consulte la siguiente documentación si necesita una introducción:

* [Aspectos básicos de la composición del esquema](../schema/composition.md)
* [Guía de API del Registro de Esquemas](../api/overview.md)

## Añadir valores sugeridos a un campo estándar

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

## Añadir valores sugeridos a un campo personalizado

Para ampliar el `meta:enum` de un campo personalizado, se puede actualizar la clase principal, el grupo de campos o el tipo de datos del campo mediante una solicitud del PATCH.

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

Esta guía explica cómo añadir valores sugeridos a campos de cadena en la API del Registro de esquemas. Consulte la guía de [definición de campos personalizados en la API](./custom-fields-api.md) para obtener más información sobre cómo crear distintos tipos de campos.
