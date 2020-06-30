---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conceptos básicos de la API de Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


# Conceptos básicos de la API de Adobe Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías subyacentes y sintaxis que son importantes de comprender para administrar eficazmente los recursos basados en [!DNL Platform] JSON. Este documento ofrece una breve descripción general de estas tecnologías, así como enlaces a documentación externa para obtener más información.

## Puntero JSON {#json-pointer}

JSON Pointer es una sintaxis de cadena estandarizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos dentro de documentos JSON. Un puntero JSON es una cadena de tokens separados por `/` caracteres, que especifica claves de objeto o índices de matriz, y los tokens pueden ser una cadena o un número. Las cadenas de puntero JSON se utilizan en muchas operaciones PATCH para [!DNL Platform] API, como se describe más adelante en este documento. Para obtener más información sobre JSON Pointer, consulte la documentación [general de](https://rapidjson.org/md_doc_pointer.html)JSON Pointer.

### Ejemplo de objeto de esquema JSON

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
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
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Ejemplo de punteros JSON basados en el objeto esquema

| Puntero JSON | Resuelve en |
|--- | ---|
| `"/title"` | &quot;Detalles de miembros de lealtad&quot; |
| `"/definitions/loyalty"` | (Devuelve el contenido del `loyalty` objeto) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Nota]
>Al tratar con los `xdm:sourceProperty` atributos y `xdm:destinationProperty` de los descriptores [!DNL Experience Data Model] (XDM), cualquier `properties` clave debe ser **excluida** de la cadena de puntero JSON. Consulte la guía para desarrolladores de la API de registro de Esquema para obtener más información sobre [los descriptores](../xdm/api/descriptors.md) .

## Parche JSON

Existen muchas operaciones PATCH para [!DNL Platform] las API que aceptan objetos JSON Patch para sus cargas de solicitud. JSON Patch es un formato estandarizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para describir los cambios en un documento JSON. Le permite definir actualizaciones parciales a JSON sin necesidad de enviar el documento completo en un cuerpo de solicitud.

### Ejemplo de objeto JSON Patch

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:: Tipo de operación de parche. Aunque JSON Patch admite varios tipos de operación diferentes, no todas las operaciones PATCH en [!DNL Platform] las API son compatibles con todos los tipos de operación. Los tipos de operaciones disponibles son:
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

Este documento introdujo algunas de las tecnologías y sintaxis relacionadas con la administración de recursos basados en JSON para [!DNL Experience Platform]. Para obtener más información sobre el trabajo con [!DNL Platform] las API, incluidas las prácticas recomendadas y las respuestas a las preguntas más frecuentes, consulte la guía [de solución de problemas de](troubleshooting.md)Platform.