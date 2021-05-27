---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;grupo de campos;grupo de campos;grupos de campos;grupos de campos;tipo de datos;tipos de datos;tipo de datos;diseño de esquema;tipo de datos;tipo de datos;tipo de datos;esquemas;esquemas;diseño de esquema;mapa;mapa;
solution: Experience Platform
title: Restricciones de tipo de campo XDM
topic-legacy: overview
description: Una referencia para restricciones de tipo de campo en Experience Data Model (XDM), incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 61025ada3a900a5bd7682e3bb7d4f6cd23347231
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 3%

---

# Restricciones de tipo de campo XDM

En los esquemas del Modelo de datos de experiencia (XDM), el tipo de campo limita qué tipo de datos puede contener el campo. Este documento proporciona información general sobre cada tipo de campo principal, incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API para aplicar diferentes restricciones.

## Primeros pasos

Antes de utilizar esta guía, revise los [conceptos básicos de la composición del esquema](./composition.md) para obtener una introducción a los esquemas XDM, las clases y los grupos de campos de esquema.

Si planea definir sus propios tipos de campo en la API, se recomienda encarecidamente que comience con la [guía para desarrolladores del Registro de esquemas](../api/getting-started.md) para aprender a crear grupos de campos y tipos de datos para incluir los campos personalizados en. Si utiliza la IU de Experience Platform para crear sus esquemas, consulte la guía sobre la [definición de campos en la IU](../ui/fields/overview.md) para aprender a implementar restricciones en campos que defina dentro de grupos de campos personalizados y tipos de datos.

## Estructura base y ejemplos

XDM se basa en el esquema JSON y, por lo tanto, los campos XDM heredan una sintaxis similar al definir su tipo. Comprender cómo se representan los distintos tipos de campos en el esquema JSON puede ayudar a indicar las restricciones de base de cada tipo.

>[!NOTE]
>
>Consulte la [guía de fundamentos de API](../../landing/api-fundamentals.md#json-schema) para obtener más información sobre el esquema JSON y otras tecnologías subyacentes en las API de plataforma.

La siguiente tabla describe cómo se representa cada tipo XDM en el esquema JSON, junto con un valor de ejemplo que se ajusta al tipo:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>Tipo XDM</th>
      <th>Esquema JSON</th>
      <th>Ejemplo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Doble]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "número"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "máximo": 9007199254740991,
  "mínimo": -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "máximo": 2147483648,
  "mínimo": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Cortocircuito]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "máximo": 32768,
  "mínimo": -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "máximo": 128,
  "mínimo": -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "formato": "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "formato": "date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Todas las cadenas con formato de fecha deben cumplir la norma ISO 8601 ([RFC 339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Asignación de tipos XDM a otros formatos

Las secciones siguientes describen cómo cada tipo XDM se asigna a otros formatos de serialización comunes:

* [Parquet, Spark SQL y Java](#parquet)
* [Scala, .NET y CosmosDB](#scala)
* [MongoDB, Aerospike y Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Entre los tipos XDM estándar que se enumeran en las tablas siguientes, también se incluye el tipo [!UICONTROL Map]. Los mapas se utilizan en esquemas estándar cuando los datos se representan como claves que se asignan a determinados valores o cuando las claves no se pueden incluir razonablemente en un esquema estático y deben tratarse como valores de datos.
>
>Los campos de tipo Mapa están reservados para el uso del esquema del sector y del proveedor y, por lo tanto, no se pueden utilizar en los recursos personalizados que defina. La inclusión del tipo de mapa en las tablas siguientes solo pretende ayudarle a determinar cómo asignar los datos existentes a XDM si actualmente se almacenan en cualquiera de los formatos que se enumeran a continuación.

### Parquet, Spark SQL y Java {#parquet}

| Tipo XDM | Parqué | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL Cadena] | Tipo: `BYTE_ARRAY`<br>Anotación: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Duplicada] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Largo] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Número entero] | Tipo: `INT32`<br>Anotación: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Corto] | Tipo: `INT32`<br>Anotación: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Anotación: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Fecha ] | Tipo: `INT32`<br>Anotación: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Anotación: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Booleano] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Mapa] | `MAP`-grupo anotado<br><br> (`<key-type>` debe ser  `STRING`) | `MapType`<br><br>(`keyType` debe ser  `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET y CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Cadena] | `String` | `System.String` | `String` |
| [!UICONTROL Duplicada] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Largo] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Número entero] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Corto] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Fecha ] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booleano] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Mapa] | `Map` | (N/D) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike y Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Cadena] | `string` | `String` | `string` |
| [!UICONTROL Duplicada] | `double` | `Double` | `double` |
| [!UICONTROL Largo] | `long` | `Integer` | `int64` |
| [!UICONTROL Número entero] | `int` | `Integer` | `int32` |
| [!UICONTROL Corto] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Fecha ] | `date` | `Integer`<br>(milisegundos de Unix) | `int64`<br>(milisegundos de Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(milisegundos de Unix) | `int64`<br>(milisegundos de Unix) |
| [!UICONTROL Booleano] | `bool` | `Integer`<br>(0/1 binario) | `bool` |
| [!UICONTROL Mapa] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definición de tipos de campo XDM en la API {#define-fields}

Todos los campos XDM se definen utilizando las restricciones estándar [JSON Schema](https://json-schema.org/) que se aplican a su tipo de campo, con restricciones adicionales para los nombres de campo que aplican [!DNL Experience Platform]. La API del Registro de esquemas permite definir tipos de campos adicionales mediante el uso de formatos y restricciones opcionales. Los tipos de campo XDM se exponen mediante el atributo de nivel de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario que añada esta propiedad al JSON para su campo al utilizar la API de . Una práctica recomendada es utilizar tipos de esquema JSON (como `string` y `integer`) con las restricciones mínimas/máximas adecuadas, tal como se definen en la tabla siguiente.

En la tabla siguiente se describe el formato adecuado para definir distintos tipos de campos, incluidos los que tienen propiedades opcionales. Encontrará más información sobre propiedades opcionales y palabras clave específicas del tipo en la [documentación del esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para empezar, busque el tipo de campo deseado y utilice el código de ejemplo proporcionado para crear la solicitud de API para [crear un grupo de campos](../api/field-groups.md#create) o [crear un tipo de datos](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>Tipo XDM</th>
    <th>Propiedades opcionales</th>
    <th>Ejemplo</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
    "type": "string",
    "pattern": "^[A-Z]{2}$",
    "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "formato": "uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>Los valores de enumeración restringidos se proporcionan en la matriz <code>enum</code>, mientras que las etiquetas opcionales de cara al cliente para cada valor se pueden proporcionar en <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Valor 3"
  },
  "predeterminado": "value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "número"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "mínimo": -9007199254740992,
  "máximo": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "mínimo": -2147483648,
  "máximo": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Cortocircuito]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "mínimo": -32768,
  "máximo": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "mínimo": -128,
  "máximo": 128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "booleano",
  "predeterminado": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "formato": "date",
  "ejemplos": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "formato": "date-time",
  "ejemplos": ["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Una matriz de tipos escalares básicos (p. ej. cadenas):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "elementos": {
    "type": "string"
  }
}</pre>
      Una matriz de objetos definidos por otro esquema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "elementos": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL (objeto)</td>
    <td></td>
    <td>El atributo <code>type</code> de cada subcampo definido en <code>properties</code> se puede definir con cualquier tipo escalar:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "propiedades": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "type": "número"
    }
  }
}</pre>
      Los campos de tipo objeto se pueden definir haciendo referencia a <code>$id</code> de un tipo de datos:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Un mapa <strong>no debe</strong> definir ninguna propiedad. <strong>debe</strong> definir un esquema <code>additionalProperties</code> único para describir el tipo de valores contenidos en el mapa (cada mapa solo puede contener un tipo de datos). Los valores pueden ser cualquier atributo XDM <code>type</code> válido o una referencia a otro esquema mediante un atributo <code>$ref</code>.<br/><br/>Campo de asignación con valores de tipo cadena:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "type": "string"
  }
}</pre>
    Campo de mapa con matrices de cadenas para valores:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "type": "array",
    "elementos": {
      "type": "string"
    }
  }
}</pre>
    Campo de mapa que hace referencia a otro tipo de datos:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
