---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conceptos básicos de la API de Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: b6d62492a60494deb848a88a9334e3ef20a93919
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 2%

---


# Conceptos básicos de la API de Adobe Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías subyacentes y sintaxis que son importantes de comprender para administrar eficazmente los recursos basados en [!DNL Platform] JSON. Este documento ofrece una breve descripción general de estas tecnologías, así como enlaces a documentación externa para obtener más información.

## Puntero JSON {#json-pointer}

JSON Pointer es una sintaxis de cadena estandarizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos dentro de documentos JSON. Un puntero JSON es una cadena de tokens separados por `/` caracteres, que especifica claves de objeto o índices de matriz, y los tokens pueden ser una cadena o un número. Las cadenas de puntero JSON se utilizan en muchas operaciones de PATCH para [!DNL Platform] API, como se describe más adelante en este documento. Para obtener más información sobre JSON Pointer, consulte la documentación [general de](https://rapidjson.org/md_doc_pointer.html)JSON Pointer.

### Ejemplo de objeto de esquema JSON

El siguiente JSON representa un esquema XDM simplificado a cuyos campos se puede hacer referencia mediante cadenas de puntero JSON. Tenga en cuenta que todos los campos que se han agregado con mezclas personalizadas (por ejemplo, `loyaltyLevel`) tienen un espacio de nombres bajo un `_{TENANT_ID}` objeto, mientras que los campos que se han agregado con mezclas principales (por ejemplo, `fullName`) no lo tienen.

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
| `"/properties/person/properties/name/properties/fullName"` | (Devuelve una referencia al `fullName` campo, proporcionada por una mezcla de núcleo). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Devuelve una referencia al `loyaltyLevel` campo, proporcionada por una mezcla personalizada). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Al tratar con los `xdm:sourceProperty` atributos y `xdm:destinationProperty` de los descriptores [!DNL Experience Data Model] (XDM), cualquier `properties` clave debe ser **excluida** de la cadena de puntero JSON. Para obtener más información, consulte la guía para desarrolladores de [!DNL Schema Registry] API en la subguía de [descriptores](../xdm/api/descriptors.md) .

## Parche JSON {#json-patch}

Hay muchas operaciones de PATCH para [!DNL Platform] API que aceptan objetos JSON Patch para sus cargas de solicitud. JSON Patch es un formato estandarizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para describir los cambios en un documento JSON. Le permite definir actualizaciones parciales a JSON sin necesidad de enviar el documento completo en un cuerpo de solicitud.

### Ejemplo de objeto JSON Patch

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:: Tipo de operación de parche. Aunque JSON Patch admite varios tipos de operaciones diferentes, no todas las operaciones de PATCH en [!DNL Platform] las API son compatibles con cada tipo de operación. Los tipos de operaciones disponibles son:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:: Parte de la estructura JSON que se va a actualizar e identificar usando notación de puntero [JSON](#json-pointer) .

Según el tipo de operación indicado en `op`, el objeto JSON Patch puede requerir propiedades adicionales. Para obtener más información sobre las distintas operaciones de parche JSON y su sintaxis requerida, consulte la documentación [de parche](http://jsonpatch.com/)JSON.

## Esquema JSON

Esquema JSON es un formato que se utiliza para describir y validar la estructura de los datos JSON. [El modelo de datos de experiencia (XDM)](../xdm/home.md) aprovecha las capacidades de Esquema JSON para imponer restricciones en la estructura y el formato de los datos de experiencia del cliente ingestados. Para obtener más información sobre el Esquema JSON, consulte la documentación [oficial](https://json-schema.org/).

## Pasos siguientes

Este documento introdujo algunas de las tecnologías y sintaxis relacionadas con la administración de recursos basados en JSON para [!DNL Experience Platform]. Para obtener más información sobre el trabajo con [!DNL Platform] las API, incluidas las prácticas recomendadas y las respuestas a las preguntas más frecuentes, consulte la guía de solución de problemas de la [plataforma](troubleshooting.md).