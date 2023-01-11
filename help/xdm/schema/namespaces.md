---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;xdm;modelo de datos de experiencia;espacio de nombres;espacios de nombres;modo de compatibilidad;fijo;
solution: Experience Platform
title: Espaciado de nombres en el modelo de datos de experiencia (XDM)
description: Descubra cómo el espaciado de nombres en Experience Data Model (XDM) le permite ampliar sus esquemas y evitar conflictos de campos a medida que se unen diferentes componentes de esquema.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# Espaciado de nombres en el modelo de datos de experiencia (XDM)

Todos los campos de los esquemas del Modelo de datos de experiencia (XDM) tienen un área de nombres asociada. Estas áreas de nombres le permiten ampliar los esquemas y evitar conflictos de campos a medida que se unen diferentes componentes de esquema. Este documento proporciona información general sobre áreas de nombres en XDM y cómo se representan en la variable [API del Registro de esquemas](../api/overview.md).

El espacio de nombres permite definir un campo en un espacio de nombres como algo diferente al mismo campo en un espacio de nombres diferente. En la práctica, el área de nombres de un campo indica quién creó el campo (como XDM estándar (Adobe), un proveedor o su organización).

Por ejemplo, considere un esquema XDM que utilice el [[!UICONTROL Detalles de contacto personal] grupo de campos](../field-groups/profile/demographic-details.md), que tiene un `mobilePhone` que existe en la variable `xdm` espacio de nombres. En el mismo esquema, también puede crear una `mobilePhone` campo en un área de nombres diferente (su [ID de inquilino](../api/getting-started.md#know-your-tenant_id)). Ambos campos pueden coexistir mientras tienen diferentes significados o restricciones subyacentes.

## Sintaxis del espaciado de nombres

Las siguientes secciones muestran cómo se asignan áreas de nombres en la sintaxis XDM.

### XDM estándar {#standard}

La sintaxis XDM estándar proporciona una perspectiva sobre cómo se representan los espacios de nombres en los esquemas (incluido [cómo se traducen en Adobe Experience Platform](#compatibility)).

Uso de XDM estándar [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) sintaxis para asignar áreas de nombres a campos. Este espacio de nombres se presenta en forma de URI (como `https://ns.adobe.com/xdm` para el `xdm` espacio de nombres) o como prefijo abreviado que está configurado en la variable `@context` de un esquema.

El siguiente es un ejemplo de esquema para un producto con sintaxis XDM estándar. Con excepción de `@id` (el identificador único definido por la especificación JSON-LD), cada campo de `properties` comienza con un área de nombres y termina con el nombre del campo. Si utiliza un prefijo de forma abreviada definido en `@context`, el área de nombres y el nombre del campo están separados por dos puntos (`:`). Si no se utiliza un prefijo, el área de nombres y el nombre del campo se separan con una barra diagonal (`/`).

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `@context` | Un objeto que define los prefijos de método abreviado que se pueden usar en lugar de un URI de área de nombres completo en `properties`. |
| `@id` | Un identificador único para el registro tal como se define en la variable [Especificación JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Ejemplo de un campo que utiliza un prefijo shorthand para denotar un área de nombres. En este caso, `xdm` es el espacio de nombres (`https://ns.adobe.com/xdm`) y `sku` es el nombre del campo. |
| `https://ns.adobe.com/xdm/channels/application` | Ejemplo de un campo que utiliza el URI completo del área de nombres. En este caso, `https://ns.adobe.com/xdm/channels` es el área de nombres y `application` es el nombre del campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Los campos proporcionados por los recursos del proveedor utilizan sus propias áreas de nombres únicas. En este ejemplo, `https://ns.adobe.com/vendorA/product` es el área de nombres del proveedor y `stockNumber` es el nombre del campo. |
| `tenantId:internalSku` | Los campos definidos por su organización utilizan su ID de inquilino único como su área de nombres. En este ejemplo, `tenantId` es el espacio de nombres del inquilino (`https://ns.adobe.com/tenantId`) y `internalSku` es el nombre del campo. |

{style=&quot;table-layout:auto&quot;}

### Modo de compatibilidad {#compatibility}

En Adobe Experience Platform, los esquemas XDM se representan en [Modo de compatibilidad](../api/appendix.md#compatibility) que no utiliza la sintaxis JSON-LD para representar espacios de nombres. En su lugar, Platform convierte el área de nombres en un campo principal (comenzando por un guión bajo) y anida los campos debajo de él.

Por ejemplo, el XDM estándar `repo:createdDate` se convierte en `_repo.createdDate` y aparecería bajo la siguiente estructura en modo de compatibilidad:

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Los campos que utilizan la variable `xdm` el área de nombres aparece como campos raíz en `properties` y suelte el `xdm:` prefijo que aparecería en [sintaxis XDM estándar](#standard). Por ejemplo, `xdm:sku` simplemente aparece como `sku` en su lugar.

El siguiente JSON representa cómo el ejemplo de sintaxis XDM estándar que se muestra arriba se traduce al modo de compatibilidad.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Pasos siguientes

Esta guía proporciona una descripción general de las áreas de nombres XDM y cómo se representan en JSON. Para obtener más información sobre cómo configurar esquemas XDM mediante la API, consulte la [Guía de API del Registro de Esquemas](../api/overview.md).
