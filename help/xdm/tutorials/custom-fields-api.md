---
title: Definir campos XDM en la API del Registro de esquemas
description: Obtenga información sobre cómo definir diferentes campos al crear recursos de modelo de datos de experiencia (XDM) personalizados en la API de registro de esquemas.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---

# Defina campos XDM en la API del Registro de esquemas

Todos los campos del modelo de datos de experiencia (XDM) se definen con el estándar [Esquema JSON](https://json-schema.org/) restricciones que se aplican a su tipo de campo, con restricciones adicionales para los nombres de campo que exige Adobe Experience Platform. La API de Registro de esquemas permite definir campos personalizados en los esquemas mediante el uso de formatos y restricciones opcionales. Los tipos de campo XDM se exponen mediante el atributo de nivel de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario agregar esta propiedad al archivo JSON para el campo al utilizar la API (excepto cuando [crear tipos de mapas personalizados](#custom-maps)). Una práctica recomendada es utilizar tipos de esquemas JSON (como `string` y `integer`) con las restricciones mín./máx. apropiadas, tal como se definen en la tabla siguiente.

Esta guía describe el formato adecuado para definir distintos tipos de campo, incluidos los que tienen propiedades opcionales. Encontrará más información sobre propiedades opcionales y palabras clave específicas del tipo en el [Documentación del esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para empezar, busque el tipo de campo deseado y utilice el código de ejemplo proporcionado para crear su solicitud de API para [creación de un grupo de campos](../api/field-groups.md#create) o [creación de un tipo de datos](../api/data-types.md#create).

## [!UICONTROL Cadena] {#string}

[!UICONTROL Cadena] los campos están indicados por `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Si lo desea, puede restringir qué tipos de valores se pueden introducir para la cadena mediante las siguientes propiedades adicionales:

* `pattern`: un patrón regex con el que restringir.
* `minLength`: Una longitud mínima para la cadena.
* `maxLength`: Una longitud máxima para la cadena.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] los campos están indicados por `type: string` con un `format` propiedad establecida en `uri`. No se aceptan otras propiedades.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enumeración] {#enum}

[!UICONTROL Enumeración] los campos deben utilizar `type: string`, con los propios valores de enumeración proporcionados en una `enum` matriz:

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

Si lo desea, puede proporcionar etiquetas dirigidas al cliente para cada valor en una `meta:enum` , con cada etiqueta incrustada en un valor correspondiente en `enum`.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
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
  }
}
```

>[!NOTE]
>
>El `meta:enum` el valor sí **no** declare una enumeración o realice cualquier validación de datos por su cuenta. En la mayoría de los casos, las cadenas proporcionadas en `meta:enum` también se incluyen en `enum` para garantizar que los datos estén restringidos. Sin embargo, hay algunos casos de uso en los que `meta:enum` se proporciona sin un correspondiente `enum` matriz. Consulte el tutorial sobre [definición de valores sugeridos](../tutorials/suggested-values.md) para obtener más información.

Si lo desea, puede proporcionar un `default` para indicar el valor predeterminado `enum` valor que el campo utilizará si no se proporciona ningún valor.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
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

>[!IMPORTANT]
>
>Si no `default` se proporciona el valor y el campo de enumeración se establece en `required`, cualquier registro al que le falte un valor aceptado para este campo no superará la validación tras la ingesta.

## [!UICONTROL Número] {#number}

Los campos de número se indican mediante `type: number` y no tienen otras propiedades requeridas.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` Los tipos se utilizan para cualquier tipo numérico, ya sean números enteros o números de coma flotante, mientras que [`integer` tipos](#integer) se utilizan específicamente para números enteros. Consulte la [Documentación del esquema JSON sobre tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obtener más información sobre los casos de uso de cada tipo.

## [!UICONTROL Número entero] {#integer}

[!UICONTROL Entero] los campos están indicados por `type: integer` y no tienen otros campos obligatorios.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>While `integer` Los tipos hacen referencia específicamente a números enteros. [`number` tipos](#number) se utilizan para cualquier tipo numérico, ya sean números enteros o números de coma flotante. Consulte la [Documentación del esquema JSON sobre tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obtener más información sobre los casos de uso de cada tipo.

Si lo desea, puede restringir el intervalo del entero añadiendo `minimum` y `maximum` propiedades a la definición. Otros tipos numéricos admitidos por la IU del Generador de esquemas son solo `integer` tipos con específicos `minimum` y `maximum` restricciones, como [[!UICONTROL Largo]](#long), [[!UICONTROL Corto]](#short), y [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Largo] {#long}

El equivalente de a [!UICONTROL Largo] El campo creado mediante la interfaz de usuario del Generador de esquemas es un [`integer` campo de tipo](#integer) con específico `minimum` y `maximum` values (`-9007199254740992` y `9007199254740992`, respectivamente).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL corto] {#short}

El equivalente de a [!UICONTROL Corto] El campo creado mediante la interfaz de usuario del Generador de esquemas es un [`integer` campo de tipo](#integer) con específico `minimum` y `maximum` values (`-32768` y `32768`, respectivamente).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Byte] {#byte}

El equivalente de a [!UICONTROL Byte] El campo creado mediante la interfaz de usuario del Generador de esquemas es un [`integer` campo de tipo](#integer) con específico `minimum` y `maximum` values (`-128` y `128`, respectivamente).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Booleana] {#boolean}

[!UICONTROL Booleano] los campos están indicados por `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Si lo desea, puede proporcionar un `default` valor que el campo utilizará cuando no se proporcione ningún valor explícito durante la ingesta.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Si no `default` se proporciona un valor y el campo booleano se establece en `required`, cualquier registro al que le falte un valor aceptado para este campo no superará la validación tras la ingesta.

## [!UICONTROL Fecha] {#date}

[!UICONTROL Fecha] los campos están indicados por `type: string` y `format: date`. También puede proporcionar una matriz de `examples` para aprovecharlo en los casos en los que desee mostrar una cadena de fecha de ejemplo para los usuarios que introducen los datos manualmente.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] los campos están indicados por `type: string` y `format: date-time`. También puede proporcionar una matriz de `examples` para aprovecharlo en los casos en los que desee mostrar una cadena de fecha y hora de ejemplo para los usuarios que introduzcan los datos manualmente.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Matriz] {#array}

[!UICONTROL Matriz] los campos están indicados por `type: array` y un `items` que define el esquema de los elementos que aceptará la matriz.

Puede definir elementos de matriz utilizando tipos primitivos, como una matriz de cadenas:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

También puede definir los elementos de la matriz en función de un tipo de datos existente haciendo referencia a `$id` del tipo de datos mediante una `$ref` propiedad. La siguiente es una matriz de [!UICONTROL Elemento de pago] objetos:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Objeto] {#object}

[!UICONTROL Objeto] los campos están indicados por `type: object` y una `properties` que define subpropiedades para el campo de esquema.

Los subcampos definidos en `properties` se puede definir con cualquier primitivo `type` o haciendo referencia a un tipo de datos existente a través de una `$ref` propiedad que señala a `$id` del tipo de datos en cuestión:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

También puede definir todo el objeto mediante referencia a un tipo de datos, siempre que el tipo de datos en cuestión se defina como `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Mapa] {#map}

Un campo de mapa es esencialmente un [`object`Campo de tipo](#object) con un conjunto de claves sin restricciones. Al igual que los objetos, los mapas tienen un `type` valor de `object`, pero sus `meta:xdmType` se establece explícitamente como `map`.

Un mapa **no debe** defina cualquier propiedad. It **debe** definir un único `additionalProperties` para describir el tipo de valores contenidos en la asignación (cada asignación solo puede contener un único tipo de datos). El `type` el valor debe ser `string` o `integer`.

Por ejemplo, un campo de asignación con valores de tipo cadena se definiría de esta manera:

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Consulte la sección siguiente para obtener más información sobre la creación de campos de mapa personalizados.

### Creación de tipos de mapas personalizados {#custom-maps}

Para admitir datos &quot;de tipo mapa&quot; de forma eficaz en XDM, los objetos se pueden anotar con un `meta:xdmType` establezca en `map` para dejar claro que un objeto debe administrarse como si el conjunto de claves no estuviera restringido. Los datos que se incorporan a los campos de asignación deben utilizar claves de cadena y solo valores de cadena o enteros (según lo determinado por `additionalProperties.type`).

XDM impone las siguientes restricciones al uso de esta sugerencia de almacenamiento:

* Los tipos de mapa DEBEN ser del tipo `object`.
* Los tipos de mapa NO DEBEN tener propiedades definidas (es decir, definen objetos &quot;vacíos&quot;).
* Los tipos de mapa DEBEN incluir un `additionalProperties.type` que describe los valores que se pueden colocar en el mapa, ya sea `string` o `integer`.

Asegúrese de utilizar únicamente campos de tipo mapa cuando sea absolutamente necesario, ya que presentan los siguientes inconvenientes de rendimiento:

* Tiempo de respuesta de [Adobe Experience Platform Query Service](../../query-service/home.md) se degrada de 3 a 10 segundos por 100 millones de registros.
* Los mapas deben tener menos de 16 claves o se arriesgarán a una mayor degradación.

La interfaz de usuario de Platform también tiene limitaciones en la forma de extraer las claves de los campos de tipo mapa. Mientras que los campos de tipo objeto se pueden expandir, los mapas se muestran como un único campo.

## Pasos siguientes

En esta guía se explica cómo definir diferentes tipos de campos en la API. Para obtener más información sobre el formato de los tipos de campo XDM, consulte la guía sobre [Restricciones de tipo de campo XDM](../schema/field-constraints.md).
