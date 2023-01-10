---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Aspectos básicos de la API del Experience Platform
description: Este documento proporciona una breve descripción general de algunas de las tecnologías subyacentes y sintaxis relacionadas con las API de Experience Platform.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 3%

---

# Aspectos básicos de la API del Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías subyacentes y sintaxis que son importantes de comprender para administrar de forma eficaz la base de JSON [!DNL Platform] recursos. Este documento proporciona una breve descripción general de estas tecnologías, así como enlaces a documentación externa para obtener más información.

## Puntero JSON {#json-pointer}

El puntero JSON es una sintaxis de cadena estandarizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos dentro de documentos JSON. Un puntero JSON es una cadena de tokens separados por `/` , que especifican claves de objeto o índices de matriz, y los tokens pueden ser una cadena o un número. Las cadenas de puntero JSON se utilizan en muchas operaciones de PATCH para [!DNL Platform] como se describe más adelante en este documento. Para obtener más información sobre el puntero JSON, consulte la [Documentación general de JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Ejemplo de objeto de esquema JSON

El siguiente JSON representa un esquema XDM simplificado cuyos campos pueden ser referenciados usando cadenas de puntero JSON. Tenga en cuenta que todos los campos que se han agregado utilizando grupos de campos de esquema personalizados (como `loyaltyLevel`) tienen un espacio de nombres dentro de un `_{TENANT_ID}` objetos, mientras que los campos que se han agregado utilizando grupos de campos principales (como `fullName`) no.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Ejemplo de punteros JSON basados en el objeto de esquema

| Puntero JSON | Resuelve como |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Devuelve una referencia a la variable `fullName` , proporcionado por un grupo de campos principal). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Devuelve una referencia a la variable `loyaltyLevel` , proporcionado por un grupo de campos personalizado.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Al tratar con el `xdm:sourceProperty` y `xdm:destinationProperty` atributos de [!DNL Experience Data Model] descriptores (XDM), cualquier `properties` las claves deben ser **Excluido** de la cadena de puntero JSON. Consulte la [!DNL Schema Registry] Guía para desarrolladores de API en [descriptores](../xdm/api/descriptors.md) para obtener más información.

## Parche JSON {#json-patch}

Hay muchas operaciones de PATCH para [!DNL Platform] API que aceptan objetos JSON Patch para sus cargas de solicitud. JSON Patch es un formato estandarizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para describir los cambios realizados en un documento JSON. Le permite definir actualizaciones parciales a JSON sin necesidad de enviar el documento completo en un cuerpo de solicitud.

### Ejemplo de objeto JSON Patch

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Tipo de operación de parche. Aunque JSON Patch admite varios tipos de operaciones diferentes, no todas las operaciones de PATCH en [!DNL Platform] Las API son compatibles con todos los tipos de operación. Los tipos de operación disponibles son:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Parte de la estructura JSON que se va a actualizar, identificar mediante [Puntero JSON](#json-pointer) notación.

Según el tipo de operación indicado en `op`, el objeto JSON Patch puede requerir propiedades adicionales. Para obtener más información sobre las distintas operaciones de parches JSON y su sintaxis requerida, consulte la [Documentación de parches JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Esquema JSON {#json-schema}

El esquema JSON es un formato utilizado para describir y validar la estructura de los datos JSON. [Modelo de datos de experiencia (XDM)](../xdm/home.md) aprovecha las capacidades del esquema JSON para imponer restricciones en la estructura y el formato de los datos de experiencia del cliente ingestados. Para obtener más información sobre el esquema JSON, consulte la [documentación oficial](https://json-schema.org/).

## Pasos siguientes

Este documento introdujo algunas de las tecnologías y sintaxis relacionadas con la administración de recursos basados en JSON para [!DNL Experience Platform]. Consulte la [guía de introducción](api-guide.md) para obtener más información sobre cómo trabajar con las API de Platform, incluidas las prácticas recomendadas. Para obtener respuestas a las preguntas más frecuentes, consulte la [Guía de solución de problemas de plataforma](troubleshooting.md).
