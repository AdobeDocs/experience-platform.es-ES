---
title: Definir campos XDM en la API del Registro de esquemas
description: Obtenga información sobre cómo definir diferentes campos al crear recursos de modelo de datos de experiencia (XDM) personalizados en la API de registro de esquemas.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Defina campos XDM en la API del Registro de esquemas

Todos los campos del Modelo de datos de experiencia (XDM) se definen con las restricciones estándar del [esquema JSON](https://json-schema.org/) que se aplican a su tipo de campo, con restricciones adicionales para los nombres de campo que aplica Adobe Experience Platform. La API de Registro de esquemas permite definir campos personalizados en los esquemas mediante el uso de formatos y restricciones opcionales. El atributo de nivel de campo `meta:xdmType` expone los tipos de campo XDM.

>[!NOTE]
>
>`meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario que agregue esta propiedad al archivo JSON para su campo al utilizar la API (excepto cuando [se crean tipos de mapas personalizados](#custom-maps)). La práctica recomendada es utilizar tipos de esquemas JSON (como `string` y `integer`) con las restricciones mín./máx. adecuadas, tal como se definen en la tabla siguiente.

Esta guía describe el formato adecuado para definir distintos tipos de campo, incluidos los que tienen propiedades opcionales. Encontrará más información sobre propiedades opcionales y palabras clave específicas del tipo en la [documentación del esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para empezar, encuentre el tipo de campo deseado y use el código de ejemplo proporcionado para generar su solicitud de API para [crear un grupo de campos](../api/field-groups.md#create) o [crear un tipo de datos](../api/data-types.md#create).

## [!UICONTROL Cadena] {#string}

Los campos [!UICONTROL Cadena] están indicados por `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Si lo desea, puede restringir qué tipos de valores se pueden introducir para la cadena mediante las siguientes propiedades adicionales:

* `pattern`: un patrón regex para restringir.
* `minLength`: una longitud mínima para la cadena.
* `maxLength`: una longitud máxima para la cadena.

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

`type: string` indica los campos [!UICONTROL URI] con una propiedad `format` establecida en `uri`. No se aceptan otras propiedades.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enumeración] {#enum}

Los campos [!UICONTROL Enum] deben usar `type: string`, con los valores de enumeración proporcionados en una matriz `enum`:

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

Opcionalmente, puede proporcionar etiquetas dirigidas al cliente para cada valor bajo una propiedad de `meta:enum`, con cada etiqueta dirigida a un valor correspondiente bajo `enum`.

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
>El valor `meta:enum` no declara **ni** una enumeración ni controla ninguna validación de datos por sí solo. En la mayoría de los casos, las cadenas proporcionadas en `meta:enum` también se proporcionan en `enum` para garantizar que los datos estén restringidos. Sin embargo, hay algunos casos de uso en los que se proporciona `meta:enum` sin la matriz `enum` correspondiente. Consulte el tutorial sobre [definición de valores sugeridos](../tutorials/suggested-values.md) para obtener más información.

Opcionalmente, puede proporcionar una propiedad `default` para indicar el valor `enum` predeterminado que utilizará el campo si no se proporciona ningún valor.

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
>Si no se proporciona ningún valor `default` y el campo de enumeración está establecido en `required`, cualquier registro al que le falte un valor aceptado para este campo no superará la validación tras la ingesta.

## [!UICONTROL Número] {#number}

Los campos numéricos están indicados por `type: number` y no tienen otras propiedades requeridas.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>Los tipos `number` se utilizan para cualquier tipo numérico, ya sean números enteros o números de coma flotante, mientras que los tipos [`integer`](#integer) se utilizan específicamente para números enteros. Consulte la [documentación del esquema JSON en tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obtener más información sobre los casos de uso de cada tipo.

## [!UICONTROL Entero] {#integer}

[!UICONTROL Los campos enteros] están indicados por `type: integer` y no tienen otros campos obligatorios.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Aunque los tipos `integer` hacen referencia específicamente a números enteros, los tipos [`number` ](#number) se utilizan para cualquier tipo numérico, ya sean números enteros o números de coma flotante. Consulte la [documentación del esquema JSON en tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obtener más información sobre los casos de uso de cada tipo.

Si lo desea, puede restringir el intervalo del entero agregando las propiedades `minimum` y `maximum` a la definición. Otros tipos numéricos admitidos por la interfaz de usuario del generador de esquemas son solo `integer` tipos con restricciones `minimum` y `maximum` específicas, como [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short) y [[!UICONTROL Byte]](#byte).

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

El equivalente de un campo [!UICONTROL Long] creado a través de la interfaz de usuario del generador de esquemas es un campo de tipo [`integer`](#integer) con valores específicos de `minimum` y `maximum` (`-9007199254740992` y `9007199254740992`, respectivamente).

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

El equivalente de un campo [!UICONTROL Short] creado a través de la interfaz de usuario del generador de esquemas es un campo de tipo [`integer`](#integer) con valores específicos de `minimum` y `maximum` (`-32768` y `32768`, respectivamente).

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

El equivalente de un campo [!UICONTROL Byte] creado a través de la interfaz de usuario del generador de esquemas es un campo de tipo [`integer`](#integer) con valores específicos de `minimum` y `maximum` (`-128` y `128`, respectivamente).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Booleano] {#boolean}

Los campos [!UICONTROL Boolean] están indicados por `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Opcionalmente, puede proporcionar un valor `default` que el campo utilizará cuando no se proporcione ningún valor explícito durante la ingesta.

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
>Si no se proporciona ningún valor `default` y el campo booleano está establecido en `required`, cualquier registro al que le falte un valor aceptado para este campo no superará la validación tras la ingesta.

## [!UICONTROL Fecha] {#date}

Los campos [!UICONTROL Date] están indicados por `type: string` y `format: date`. Opcionalmente, también puede proporcionar una matriz de `examples` para aprovecharla en los casos en que desee mostrar una cadena de fecha de muestra para los usuarios que introduzcan los datos manualmente.

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

Los campos [!UICONTROL DateTime] están indicados por `type: string` y `format: date-time`. Opcionalmente, también puede proporcionar una matriz de `examples` para aprovecharla en los casos en que desee mostrar una cadena de fecha y hora de muestra para los usuarios que escriban los datos manualmente.

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

Los campos [!UICONTROL Array] están indicados por `type: array` y un objeto `items` que define el esquema de los elementos que aceptará la matriz.

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

También puede definir los elementos de matriz basados en un tipo de datos existente haciendo referencia al `$id` del tipo de datos a través de una propiedad `$ref`. A continuación se muestra una matriz de [!UICONTROL objetos Elemento de pago]:

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

Los campos [!UICONTROL Object] están indicados por `type: object` y un objeto `properties` que define subpropiedades para el campo de esquema.

Cada subcampo definido bajo `properties` se puede definir usando cualquier tipo de datos primitivo `type` o haciendo referencia a un tipo de datos existente a través de una propiedad `$ref` que señala al `$id` del tipo de datos en cuestión:

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

Un campo de asignación es esencialmente un campo de tipo [`object` ](#object) con un conjunto de claves no restringido. Al igual que los objetos, las asignaciones tienen un valor `type` de `object`, pero su `meta:xdmType` se ha establecido explícitamente en `map`.

Un mapa **no debe** definir ninguna propiedad. **debe** definir un solo esquema `additionalProperties` para describir el tipo de valores contenidos en el mapa (cada mapa solo puede contener un único tipo de datos). El valor `type` debe ser `string` o `integer`.

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

Para admitir datos &quot;de tipo mapa&quot; de forma eficaz en XDM, los objetos pueden anotarse con un `meta:xdmType` establecido en `map` para dejar claro que un objeto debe administrarse como si el conjunto de claves no estuviera restringido. Los datos que se incorporan a los campos de asignación deben utilizar claves de cadena y solo valores de cadena o enteros (determinados por `additionalProperties.type`).

XDM impone las siguientes restricciones al uso de esta sugerencia de almacenamiento:

* Los tipos de mapa DEBEN ser del tipo `object`.
* Los tipos de mapa NO DEBEN tener propiedades definidas (es decir, definen objetos &quot;vacíos&quot;).
* Los tipos de mapa DEBEN incluir un campo `additionalProperties.type` que describa los valores que se pueden colocar en el mapa, ya sea `string` o `integer`.

Asegúrese de utilizar únicamente campos de tipo mapa cuando sea absolutamente necesario, ya que presentan los siguientes inconvenientes de rendimiento:

* El tiempo de respuesta de [Adobe Experience Platform Query Service](../../query-service/home.md) se degrada de tres a diez segundos para 100 millones de registros.
* Los mapas deben tener menos de 16 claves o se arriesgarán a una mayor degradación.

La interfaz de usuario de Platform también tiene limitaciones en la forma de extraer las claves de los campos de tipo mapa. Mientras que los campos de tipo objeto se pueden expandir, los mapas se muestran como un único campo.

## Pasos siguientes

En esta guía se explica cómo definir diferentes tipos de campos en la API. Para obtener más información sobre el formato de los tipos de campo XDM, consulte la guía sobre [restricciones de tipo de campo XDM](../schema/field-constraints.md).
