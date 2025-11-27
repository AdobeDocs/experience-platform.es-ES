---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;grupo de campos;grupos de campos;grupos de campos;grupos de campos;tipo de datos;tipos de datos;Tipos de datos;Tipo de datos;Diseño de esquema;tipo de datos;Tipo de datos;esquemas;Diseño de esquema;Mapa;
solution: Experience Platform
title: Restricciones de tipo de campo XDM
description: Una referencia para las restricciones de tipo de campo en el Experience Data Model (XDM), incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 8ddedb5ff8c12b05cdf39fa8dc2b59258389e522
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# Restricciones de tipo de campo XDM

En esquemas XDM (Experience Data Model), el tipo de campo restringe el tipo de datos que puede contener el campo. Este documento proporciona información general de cada tipo de campo principal, incluidos los demás formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API para aplicar diferentes restricciones.

## Introducción

Antes de usar esta guía, revise los [conceptos básicos de la composición de esquemas](./composition.md) para obtener una introducción a los esquemas XDM, las clases y los grupos de campos de esquema.

Si planea definir sus propios tipos de campo en la API, se recomienda comenzar con la [Guía para desarrolladores de Schema Registry](../api/getting-started.md) para aprender a crear grupos de campos y tipos de datos para incluir sus campos personalizados en. Si está usando la interfaz de usuario de Experience Platform para crear los esquemas, consulte la guía sobre [definición de campos en la interfaz de usuario](../ui/fields/overview.md) para obtener información sobre cómo implementar restricciones en campos que defina dentro de grupos de campos personalizados y tipos de datos.

## Estructura base y ejemplos {#basic-types}

XDM se basa en el esquema JSON y, por lo tanto, los campos XDM heredan una sintaxis similar al definir su tipo. Comprender cómo se representan los distintos tipos de campo en el esquema JSON puede ayudar a indicar las restricciones base de cada tipo. Los nombres de los campos personalizados no distinguen entre mayúsculas y minúsculas y deben tener nombres diferentes en el mismo nivel del esquema.

>[!NOTE]
>
>Consulte la [guía de aspectos básicos de la API](../../landing/api-fundamentals.md#json-schema) para obtener más información sobre el esquema JSON y otras tecnologías subyacentes en las API de Experience Platform.

En la siguiente tabla se describe cómo se representa cada tipo XDM en el esquema JSON, junto con un valor de ejemplo que se ajusta al tipo:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>Tipo de XDM</th>
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
      <td>[!UICONTROL Number]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "tipo": "entero",
  "maximum": 9007199254740991,
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
  "tipo": "entero",
  "maximum": 2147483648,
  "mínimo": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "tipo": "entero",
  "maximum": 32767,
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
  "tipo": "entero",
  "máximo": 128,
  mínimo: -128
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
  "format": "date"
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
  "format": "date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "boolean"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Todas las cadenas con formato de fecha deben cumplir con el estándar ISO 8601 ([RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Asignación de tipos XDM a otros formatos

Las secciones siguientes describen cómo cada tipo XDM se asigna a otros formatos de serialización comunes:

* [Parquet, Spark SQL y Java](#parquet)
* [Scala, .NET y CosmosDB](#scala)
* [MongoDB, Aerospike y Protobuf 2](#mongo)

>[!NOTE]
>
>Entre los tipos XDM estándar enumerados en las tablas siguientes, también se incluye el tipo [!UICONTROL Map]. Los mapas se utilizan en esquemas estándar cuando los datos se representan como claves que se asignan a determinados valores o cuando las claves no se pueden incluir razonablemente en un esquema estático y deben tratarse como valores de datos.
>
>Muchos componentes XDM estándar usan tipos de asignación, y también puede [definir campos de asignación personalizados](../tutorials/custom-fields-api.md#custom-maps) si lo desea. La inclusión del tipo de mapa en las tablas siguientes pretende ayudarle a determinar cómo asignar los datos existentes a XDM si actualmente están almacenados en cualquiera de los formatos enumerados a continuación.

### Parquet, Spark SQL y Java {#parquet}

| Tipo de XDM | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Tipo: `BYTE_ARRAY`<br>Anotación: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Number] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Tipo: `INT32`<br>Anotación: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Tipo: `INT32`<br>Anotación: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Anotación: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Tipo: `INT32`<br>Anotación: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Anotación: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`: el grupo <br><br> anotado (`<key-type>` debe ser `STRING`) | `MapType`<br><br>(`keyType` debe ser `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET y CosmosDB {#scala}

| Tipo de XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Number] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (N/D) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike y Protobuf 2 {#mongo}

| Tipo de XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Number] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(milisegundos de Unix) | `int64`<br>(milisegundos de Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(milisegundos de Unix) | `int64`<br>(milisegundos de Unix) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(binario 0/1) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## Definición de tipos de campo XDM en la API {#define-fields}

La API de Registro de esquemas permite definir campos personalizados mediante el uso de formatos y restricciones opcionales. Consulte la guía [definición de campos personalizados en la API del Registro de esquemas](../tutorials/custom-fields-api.md) para obtener más información.
