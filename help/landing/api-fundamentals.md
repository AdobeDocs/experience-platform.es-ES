---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Conceptos básicos de la API de Experience Platform
topic: getting started
description: Este documento ofrece una breve descripción general de algunas de las tecnologías subyacentes y sintaxis relacionadas con las API de Experience Platform.
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# Conceptos básicos de la API de Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías subyacentes y sintaxis que son importantes de comprender para administrar eficazmente los [!DNL Platform] recursos basados en JSON. Este documento ofrece una breve descripción general de estas tecnologías, así como enlaces a documentación externa para obtener más información.

## Puntero JSON {#json-pointer}

El puntero JSON es una sintaxis de cadena estandarizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos dentro de documentos JSON. Un puntero JSON es una cadena de tokens separados por `/` caracteres, que especifican claves de objeto o índices de matriz, y los tokens pueden ser una cadena o un número. Las cadenas de puntero JSON se utilizan en muchas operaciones de PATCH para API [!DNL Platform], como se describe más adelante en este documento. Para obtener más información sobre JSON Pointer, consulte la [documentación general de JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Ejemplo de objeto de esquema JSON

El siguiente JSON representa un esquema XDM simplificado a cuyos campos se puede hacer referencia mediante cadenas de puntero JSON. Tenga en cuenta que todos los campos que se han agregado usando mezclas personalizadas (como `loyaltyLevel`) tienen un espacio de nombres dentro de un objeto `_{TENANT_ID}`, mientras que los campos que se han agregado usando mezclas principales (como `fullName`) no lo tienen.

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

### Ejemplo de punteros JSON basados en el objeto esquema

| Puntero JSON | Resuelve en |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Devuelve una referencia al campo `fullName`, proporcionada por una mezcla de núcleo). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Devuelve una referencia al campo `loyaltyLevel`, proporcionada por una mezcla personalizada). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Al tratar con los atributos `xdm:sourceProperty` y `xdm:destinationProperty` de los descriptores [!DNL Experience Data Model] (XDM), cualquier clave `properties` debe estar **excluida** de la cadena del puntero JSON. Consulte la [!DNL Schema Registry] guía para desarrolladores de API en la guía [descriptores](../xdm/api/descriptors.md) para obtener más información.

## Parche JSON {#json-patch}

Existen muchas operaciones de PATCH para las API [!DNL Platform] que aceptan objetos JSON Patch para sus cargas de solicitud. JSON Patch es un formato estandarizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para describir los cambios en un documento JSON. Le permite definir actualizaciones parciales a JSON sin necesidad de enviar el documento completo en un cuerpo de solicitud.

### Ejemplo de objeto JSON Patch

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:: Tipo de operación de parche. Aunque JSON Patch admite varios tipos de operaciones diferentes, no todas las operaciones de PATCH en las API [!DNL Platform] son compatibles con cada tipo de operación. Los tipos de operaciones disponibles son:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:: Parte de la estructura JSON que se va a actualizar e identificar usando la  [notación ](#json-pointer) JSON.

Según el tipo de operación indicado en `op`, el objeto JSON Patch puede requerir propiedades adicionales. Para obtener más información sobre las distintas operaciones de JSON Patch y su sintaxis requerida, consulte la [documentación de JSON Patch](http://jsonpatch.com/).

## Esquema JSON

Esquema JSON es un formato que se utiliza para describir y validar la estructura de los datos JSON. [El modelo de datos de experiencia (XDM)](../xdm/home.md) aprovecha las capacidades de Esquema JSON para imponer restricciones en la estructura y el formato de los datos de experiencia del cliente ingestados. Para obtener más información sobre el Esquema JSON, consulte la [documentación oficial](https://json-schema.org/).

## Pasos siguientes

Este documento introdujo algunas de las tecnologías y sintaxis que implican la administración de recursos basados en JSON para [!DNL Experience Platform]. Para obtener más información sobre cómo trabajar con las [!DNL Platform] API, incluidas las mejores prácticas y las respuestas a las preguntas más frecuentes, consulte la [Guía de solución de problemas de la plataforma](troubleshooting.md).