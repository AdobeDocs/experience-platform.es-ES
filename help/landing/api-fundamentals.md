---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Fundamentos de API de Experience Platform
description: Este documento proporciona una breve descripción de algunas de las tecnologías y sintaxis subyacentes relacionadas con las API de Experience Platform.
role: Developer
feature: API
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Fundamentos de API de Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías y sintaxis subyacentes que son importantes de comprender para administrar de forma eficaz los recursos de [!DNL Platform] basados en JSON. Este documento proporciona una breve descripción general de estas tecnologías, así como vínculos a documentación externa para obtener más información.

## Puntero JSON {#json-pointer}

El puntero JSON es una sintaxis de cadena estandarizada ([RFC 6901](https://tools.ietf.org/html/rfc6901)) para identificar valores específicos dentro de documentos JSON. Un puntero JSON es una cadena de tokens separados por `/` caracteres, que especifican claves de objeto o índices de matriz, y los tokens pueden ser una cadena o un número. Las cadenas de puntero JSON se utilizan en muchas operaciones de PATCH para las API [!DNL Platform], tal como se describe más adelante en este documento. Para obtener más información sobre el puntero JSON, consulte la [documentación de información general sobre el puntero JSON](https://rapidjson.org/md_doc_pointer.html).

### Ejemplo de objeto de esquema JSON

El siguiente JSON representa un esquema XDM simplificado cuyos campos pueden referenciarse mediante cadenas de puntero JSON. Tenga en cuenta que todos los campos que se han agregado mediante grupos de campos de esquema personalizados (como `loyaltyLevel`) tienen un espacio de nombres en un objeto `_{TENANT_ID}`, mientras que los campos que se han agregado mediante grupos de campos principales (como `fullName`) no lo tienen.

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

| Puntero JSON | Se resuelve en |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Devuelve una referencia al campo `fullName` proporcionada por un grupo de campos principales). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Devuelve una referencia al campo `loyaltyLevel` proporcionada por un grupo de campos personalizados). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Al tratar con los atributos `xdm:sourceProperty` y `xdm:destinationProperty` de los descriptores [!DNL Experience Data Model] (XDM), cualquier clave `properties` debe ser **excluida** de la cadena de puntero JSON. Consulte la subguía [!DNL Schema Registry] API developer guide (Guía para desarrolladores de API) sobre [descriptores](../xdm/api/descriptors.md) para obtener más información.

## Parche de JSON {#json-patch}

Hay muchas operaciones de PATCH para las API de [!DNL Platform] que aceptan objetos de parche JSON para sus cargas útiles de solicitud. El parche JSON es un formato estandarizado ([RFC 6902](https://tools.ietf.org/html/rfc6902)) para describir cambios en un documento JSON. Permite definir actualizaciones parciales de JSON sin necesidad de enviar todo el documento en un cuerpo de solicitud.

### Ejemplo de objeto de parche de JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: tipo de operación de revisión. Aunque el parche JSON admite varios tipos de operaciones diferentes, no todas las operaciones del PATCH en las API [!DNL Platform] son compatibles con todos los tipos de operaciones. Los tipos de operación disponibles son:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: la parte de la estructura JSON que se va a actualizar, identificada con la notación [Puntero JSON](#json-pointer).

Según el tipo de operación indicado en `op`, el objeto de parche de JSON puede requerir propiedades adicionales. Para obtener más información sobre las distintas operaciones de parches de JSON y su sintaxis necesaria, consulte la [documentación de parches de JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Esquema JSON {#json-schema}

El esquema JSON es un formato que se utiliza para describir y validar la estructura de los datos JSON. [Experience Data Model (XDM)](../xdm/home.md) aprovecha las capacidades del esquema JSON para aplicar restricciones en la estructura y el formato de los datos de experiencia del cliente ingeridos. Para obtener más información sobre el esquema JSON, consulte la [documentación oficial](https://json-schema.org/).

## Pasos siguientes

Este documento introdujo algunas de las tecnologías y sintaxis involucradas en la administración de recursos basados en JSON para [!DNL Experience Platform]. Consulte la [guía de introducción](api-guide.md) para obtener más información sobre cómo trabajar con las API de Platform, incluidas las prácticas recomendadas. Para obtener respuestas a las preguntas más frecuentes, consulte la [Guía de solución de problemas de la plataforma](troubleshooting.md).
