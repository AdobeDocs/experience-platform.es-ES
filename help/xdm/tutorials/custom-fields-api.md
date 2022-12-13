---
title: Definición de campos XDM en la API del Registro de Esquema
description: Obtenga información sobre cómo definir distintos campos al crear recursos del Modelo de datos de experiencia (XDM) personalizados en la API del Registro de esquemas.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 0947eb38bdb18cb3783723cb11be79d3d32a3b76
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 1%

---

# Definición de campos XDM en la API del Registro de Esquema

Todos los campos del Modelo de datos de experiencia (XDM) se definen mediante el [Esquema JSON](https://json-schema.org/) restricciones que se aplican a su tipo de campo, con restricciones adicionales para nombres de campo que son aplicadas por Adobe Experience Platform. La API del Registro de esquemas permite definir campos personalizados en los esquemas mediante el uso de formatos y restricciones opcionales. Los tipos de campo XDM se exponen mediante el atributo de nivel de campo. `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario que agregue esta propiedad al JSON para su campo al utilizar la API (excepto cuando [creación de tipos de mapa personalizados](#custom-maps)). Una práctica recomendada es utilizar tipos de esquema JSON (como `string` y `integer`) con las restricciones de mínimo/máximo adecuadas, tal como se definen en la siguiente tabla.

Esta guía describe el formato adecuado para definir diferentes tipos de campos, incluidos los que tienen propiedades opcionales. Encontrará más información sobre las propiedades opcionales y las palabras clave específicas del tipo en la [Documentación del esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para empezar, busque el tipo de campo deseado y utilice el código de ejemplo proporcionado para crear la solicitud de API de [creación de un grupo de campos](../api/field-groups.md#create) o [creación de un tipo de datos](../api/data-types.md#create).

## [!UICONTROL Cadena] {#string}

[!UICONTROL Cadena] los campos se indican mediante `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Opcionalmente, puede restringir los tipos de valores que se pueden introducir para la cadena mediante las siguientes propiedades adicionales:

* `pattern`: Un patrón regex por el que restringir.
* `minLength`: Longitud mínima de la cadena.
* `maxLength`: Longitud máxima de la cadena.

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

[!UICONTROL URI] los campos se indican mediante `type: string` con un `format` propiedad establecida en `uri`. No se aceptan otras propiedades.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] los campos deben utilizar `type: string`, con los propios valores de enumeración proporcionados en un `enum` matriz:

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

Puede proporcionar etiquetas opcionales de cara al cliente para cada valor en una `meta:enum` con cada etiqueta tecleada a una `enum` valor.

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
>La variable `meta:enum` value does **not** declare una enumeración o conduzca cualquier validación de datos por su cuenta. En la mayoría de los casos, las cadenas proporcionadas en `meta:enum` también se proporcionan en `enum` para garantizar que los datos estén restringidos. Sin embargo, hay algunos casos de uso en los que `meta:enum` se proporciona sin `enum` matriz. Consulte el tutorial en [definición de valores sugeridos](../tutorials/suggested-values.md) para obtener más información.

Si lo desea, puede proporcionar un `default` para indicar el valor predeterminado `enum` que utilizará el campo si no se proporciona ningún valor.

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
>Si no `default` se proporciona y el campo enum se define como `required`, cualquier registro que falte un valor aceptado para este campo no se validará correctamente al ingerirlo.

## [!UICONTROL Número] {#number}

Los campos numéricos se indican mediante `type: number` y no tienen otras propiedades requeridas.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` se utilizan para cualquier tipo numérico, números enteros o números de coma flotante, mientras que [`integer` tipos](#integer) se utilizan específicamente para números enteros. Consulte la [Documentación del esquema JSON para tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obtener más información sobre los casos de uso de cada tipo.

## [!UICONTROL Número entero] {#integer}

[!UICONTROL Número entero] los campos se indican mediante `type: integer` y no tienen otros campos obligatorios.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>While `integer` los tipos hacen referencia específicamente a números enteros, [`number` tipos](#number) se utilizan para cualquier tipo numérico, números enteros o números de coma flotante. Consulte la [Documentación del esquema JSON para tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obtener más información sobre los casos de uso de cada tipo.

Opcionalmente, puede restringir el rango del entero añadiendo `minimum` y `maximum` a la definición. Otros tipos numéricos admitidos por la interfaz de usuario del Generador de esquemas solo son `integer` tipos específicos `minimum` y `maximum` restricciones, como [[!UICONTROL Largo]](#long), [[!UICONTROL Corto]](#short)y [[!UICONTROL Byte]](#byte).

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

El equivalente de un [!UICONTROL Largo] el campo creado a través de la interfaz de usuario del Generador de esquemas es un [`integer` campo de tipo](#integer) con específico `minimum` y `maximum` valores (`-9007199254740992` y `9007199254740992`, respectivamente).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Corto] {#short}

El equivalente de un [!UICONTROL Corto] el campo creado a través de la interfaz de usuario del Generador de esquemas es un [`integer` campo de tipo](#integer) con específico `minimum` y `maximum` valores (`-32768` y `32768`, respectivamente).

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

El equivalente de un [!UICONTROL Byte] el campo creado a través de la interfaz de usuario del Generador de esquemas es un [`integer` campo de tipo](#integer) con específico `minimum` y `maximum` valores (`-128` y `128`, respectivamente).

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

[!UICONTROL Booleano] los campos se indican mediante `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Si lo desea, puede proporcionar un `default` que el campo utilizará cuando no se proporcione ningún valor explícito durante la ingesta.

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
>Si no `default` se proporciona y el campo booleano se define como `required`, cualquier registro que falte un valor aceptado para este campo no se validará correctamente al ingerirlo.

## [!UICONTROL Fecha] {#date}

[!UICONTROL Fecha] los campos se indican mediante `type: string` y `format: date`. También puede proporcionar una matriz de `examples` para aprovechar los casos en los que desea mostrar una cadena de fecha de muestra para los usuarios que introducen los datos manualmente.

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

[!UICONTROL DateTime] los campos se indican mediante `type: string` y `format: date-time`. También puede proporcionar una matriz de `examples` para aprovechar los casos en los que desea mostrar una cadena de fecha y hora de muestra para los usuarios que introducen los datos manualmente.

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

[!UICONTROL Matriz] los campos se indican mediante `type: array` y `items` objeto que define el esquema de los elementos que aceptará la matriz.

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

También puede definir los elementos de la matriz en función de un tipo de datos existente haciendo referencia a la variable `$id` del tipo de datos a través de un `$ref` propiedad. A continuación se muestra una matriz de [!UICONTROL Artículo de pago] objetos:

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

[!UICONTROL Objeto] los campos se indican mediante `type: object` y `properties` objeto que define subpropiedades para el campo de esquema.

Cada subcampo definido en `properties` se puede definir con cualquier `type` o haciendo referencia a un tipo de datos existente a través de una `$ref` propiedad que señala a la variable `$id` del tipo de datos en cuestión:

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

También puede definir todo el objeto haciendo referencia a un tipo de datos, siempre que el tipo de datos en cuestión se defina como `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Mapa] {#map}

Un campo de mapa es esencialmente un [`object`campo -type](#object) con un conjunto de claves sin restricciones. Al igual que los objetos, los mapas tienen un `type` valor de `object`, pero sus `meta:xdmType` se configura explícitamente como `map`.

Un mapa **no debe** defina cualquier propiedad. It **must** definir una sola `additionalProperties` para describir el tipo de valores contenidos en el mapa (cada mapa solo puede contener un tipo de datos). La variable `type` debe ser `string` o `integer`.

Por ejemplo, un campo de asignación con valores de tipo cadena se definiría de la siguiente manera:

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

Consulte la sección siguiente para obtener más información sobre la creación de campos de asignación personalizados.

### Creación de tipos de mapa personalizados {#custom-maps}

Para admitir datos &quot;similares a mapas&quot; de forma eficaz en XDM, los objetos se pueden anotar con un `meta:xdmType` configure como `map` para dejar claro que un objeto debe administrarse como si el conjunto de claves no estuviera limitado. Los datos que se incorporan en los campos de asignación deben utilizar claves de cadena y solo valores de cadena o entero (tal y como determinan `additionalProperties.type`).

XDM impone las siguientes restricciones al uso de esta sugerencia de almacenamiento:

* Los tipos de mapa DEBEN ser del tipo `object`.
* Los tipos de mapa NO DEBEN tener propiedades definidas (en otras palabras, definen objetos &quot;vacíos&quot;).
* Los tipos de mapa DEBEN incluir un `additionalProperties.type` campo que describe los valores que pueden colocarse dentro del mapa, ya sea `string` o `integer`.

Asegúrese de que solo está utilizando campos de tipo mapa cuando es absolutamente necesario, ya que presentan los siguientes inconvenientes de rendimiento:

* Tiempo de respuesta desde [Servicio de consultas de Adobe Experience Platform](../../query-service/home.md) se degrada de tres segundos a diez segundos para 100 millones de registros.
* Los mapas deben tener menos de 16 claves o, de lo contrario, pueden degradarse aún más.

La interfaz de usuario de Platform también tiene limitaciones en la forma en que puede extraer las claves de los campos de tipo mapa. Mientras que los campos de tipo objeto se pueden expandir, los mapas se muestran como un solo campo en su lugar.

## Pasos siguientes

Esta guía explica cómo definir diferentes tipos de campos en la API. Para obtener más información sobre el formato de los tipos de campo XDM, consulte la guía de [Restricciones de tipo de campo XDM](../schema/field-constraints.md).
