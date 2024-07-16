---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;xdm;modelo de datos de experiencia;área de nombres;áreas de nombres;modo de compatibilidad;xed;
solution: Experience Platform
title: Espaciado de nombres en el modelo de datos de experiencia (XDM)
description: Descubra cómo el espacio de nombres en el Modelo de datos de experiencia (XDM) le permite ampliar los esquemas y evitar conflictos de campos a medida que se reúnen distintos componentes de esquema.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Espaciado de nombres en el modelo de datos de experiencia (XDM)

>[!IMPORTANT]
>
>En XDM, el área de nombres (el tema de esta página) se utiliza para distinguir los campos de un esquema. Esto es diferente al concepto de área de nombres de identidad en el servicio de identidad, donde el área de nombres se utiliza para distinguir los valores de identidad. Lea la documentación sobre el espacio de nombres [en el servicio de identidad](../../identity-service/features/namespaces.md) para obtener más información.

Todos los campos de los esquemas XDM (Experience Data Model) tienen un área de nombres asociada. Estas áreas de nombres le permiten ampliar los esquemas y evitar conflictos de campos a medida que se reúnen distintos componentes de esquema. Este documento proporciona información general sobre los espacios de nombres en XDM y cómo se representan en la [API de Registro de esquemas](../api/overview.md).

El espacio de nombres permite definir un campo en un área de nombres para que signifique algo diferente que el mismo campo en una área de nombres diferente. En la práctica, el área de nombres de un campo indica quién creó el campo (como un XDM estándar (Adobe), un proveedor o su organización).

Por ejemplo, considere un esquema XDM que use el grupo de campos [[!UICONTROL Datos personales de contacto]](../field-groups/profile/demographic-details.md), que tiene un campo `mobilePhone` estándar que existe en el área de nombres `xdm`. En el mismo esquema, también puede crear un campo `mobilePhone` independiente en un área de nombres diferente (su [ID de inquilino](../api/getting-started.md#know-your-tenant_id)). Ambos campos pueden coexistir juntos mientras tienen diferentes significados o restricciones subyacentes.

## Sintaxis de espacio de nombres

Las secciones siguientes muestran cómo se asignan los espacios de nombres en la sintaxis XDM.

### XDM estándar {#standard}

La sintaxis XDM estándar proporciona una perspectiva de cómo se representan los espacios de nombres en los esquemas (incluido [cómo se traducen en Adobe Experience Platform](#compatibility)).

El XDM estándar utiliza la sintaxis [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) para asignar áreas de nombres a los campos. Este espacio de nombres se presenta en forma de URI (como `https://ns.adobe.com/xdm` para el espacio de nombres `xdm`) o como prefijo abreviado que se configura en el atributo `@context` de un esquema.

El siguiente es un esquema de ejemplo para un producto con sintaxis XDM estándar. Con la excepción de `@id` (el identificador único definido por la especificación JSON-LD), cada campo bajo `properties` comienza con un área de nombres y termina con el nombre del campo. Si se usa un prefijo abreviado definido en `@context`, el espacio de nombres y el nombre de campo se separarán mediante dos puntos (`:`). Si no se usa un prefijo, el espacio de nombres y el nombre de campo se separarán mediante una barra diagonal (`/`).

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
| `@context` | Un objeto que define los prefijos abreviados que se pueden usar en lugar de un URI de espacio de nombres completo en `properties`. |
| `@id` | Un identificador único para el registro según se define en la [especificación JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Ejemplo de un campo que utiliza un prefijo abreviado para denotar un espacio de nombres. En este caso, `xdm` es el espacio de nombres (`https://ns.adobe.com/xdm`) y `sku` es el nombre del campo. |
| `https://ns.adobe.com/xdm/channels/application` | Ejemplo de un campo que utiliza el URI de espacio de nombres completo. En este caso, `https://ns.adobe.com/xdm/channels` es el área de nombres y `application` es el nombre del campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Los campos proporcionados por los recursos del proveedor utilizan sus propias áreas de nombres únicas. En este ejemplo, `https://ns.adobe.com/vendorA/product` es el espacio de nombres del proveedor y `stockNumber` es el nombre del campo. |
| `tenantId:internalSku` | Los campos definidos por su organización utilizan su ID de inquilino único como área de nombres. En este ejemplo, `tenantId` es el espacio de nombres del inquilino (`https://ns.adobe.com/tenantId`) y `internalSku` es el nombre del campo. |

{style="table-layout:auto"}

### Modo de compatibilidad {#compatibility}

En Adobe Experience Platform, los esquemas XDM se representan con la sintaxis [Modo de compatibilidad](../api/appendix.md#compatibility), que no utiliza la sintaxis JSON-LD para representar áreas de nombres. En su lugar, Platform convierte el área de nombres en un campo principal (que comienza con un guion bajo) y anida los campos en él.

Por ejemplo, el XDM estándar `repo:createdDate` se convierte a `_repo.createdDate` y aparecería en la siguiente estructura en el modo de compatibilidad:

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

Los campos que utilizan el área de nombres `xdm` aparecen como campos raíz en `properties` y sueltan el prefijo `xdm:` que aparecería en [sintaxis XDM estándar](#standard). Por ejemplo, `xdm:sku` simplemente aparece como `sku`.

El siguiente JSON representa cómo se traduce el ejemplo de sintaxis XDM estándar que se muestra arriba al modo de compatibilidad.

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

Esta guía proporciona información general sobre las áreas de nombres XDM y cómo se representan en JSON. Para obtener más información sobre cómo configurar esquemas XDM mediante la API, consulte la [Guía de API del Registro de esquemas](../api/overview.md).
