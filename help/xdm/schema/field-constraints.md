---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;grupo de campos;grupo de campos;grupos de campos;grupos de campos;tipo de datos;tipos de datos;tipo de datos;diseño de esquema;tipo de datos;tipo de datos;tipo de datos;esquemas;esquemas;diseño de esquema;mapa;mapa;
solution: Experience Platform
title: Restricciones de tipo de campo XDM
description: Una referencia para restricciones de tipo de campo en Experience Data Model (XDM), incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 7%

---

# Restricciones de tipo de campo XDM

En los esquemas del Modelo de datos de experiencia (XDM), el tipo de campo limita qué tipo de datos puede contener el campo. Este documento proporciona información general sobre cada tipo de campo principal, incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API para aplicar diferentes restricciones.

## Primeros pasos

Antes de usar esta guía, revise la [conceptos básicos de la composición del esquema](./composition.md) para obtener una introducción a los esquemas XDM, las clases y los grupos de campos de esquema.

Si planea definir sus propios tipos de campo en la API, se recomienda encarecidamente que comience con la variable [Guía para desarrolladores de Schema Registry](../api/getting-started.md) para aprender a crear grupos de campos y tipos de datos para incluir sus campos personalizados en. Si utiliza la interfaz de usuario del Experience Platform para crear sus esquemas, consulte la guía de [definición de campos en la interfaz de usuario](../ui/fields/overview.md) para aprender a implementar restricciones en campos definidos dentro de grupos de campos personalizados y tipos de datos.

## Estructura base y ejemplos {#basic-types}

XDM se basa en el esquema JSON y, por lo tanto, los campos XDM heredan una sintaxis similar al definir su tipo. Comprender cómo se representan los distintos tipos de campos en el esquema JSON puede ayudar a indicar las restricciones de base de cada tipo.

>[!NOTE]
>
>Consulte la [Guía de fundamentos de API](../../landing/api-fundamentals.md#json-schema) para obtener más información sobre el esquema JSON y otras tecnologías subyacentes en las API de plataforma.

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
{ "type": "integer", "maximum": 9007199254740991, "mínimo": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "mínimo": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Cortocircuito]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "mínimo": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "mínimo": -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
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

**Todas las cadenas con formato de fecha deben cumplir la norma ISO 8601 ([RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Asignación de tipos XDM a otros formatos

Las secciones siguientes describen cómo cada tipo XDM se asigna a otros formatos de serialización comunes:

* [Parquet, Spark SQL y Java](#parquet)
* [Scala, .NET y CosmosDB](#scala)
* [MongoDB, Aerospike y Protobuf 2](#mongo)

>[!NOTE]
>
>Entre los tipos XDM estándar que se enumeran en las tablas siguientes, la variable [!UICONTROL Mapa] también se incluye. Los mapas se utilizan en esquemas estándar cuando los datos se representan como claves que se asignan a determinados valores o cuando las claves no se pueden incluir razonablemente en un esquema estático y deben tratarse como valores de datos.
>
>Muchos componentes XDM estándar utilizan tipos de asignación y también puede [definir campos de asignación personalizados](../tutorials/custom-fields-api.md#custom-maps) si lo desea. La inclusión del tipo de mapa en las tablas siguientes pretende ayudarle a determinar cómo asignar los datos existentes a XDM si actualmente se almacenan en cualquiera de los formatos que se enumeran a continuación.

### Parquet, Spark SQL y Java {#parquet}

| Tipo XDM | Parqué | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL Cadena] | Tipo: `BYTE_ARRAY`<br>Anotación: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Doble] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Largo] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Número entero] | Tipo: `INT32`<br>Anotación: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL corto] | Tipo: `INT32`<br>Anotación: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Anotación: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Fecha] | Tipo: `INT32`<br>Anotación: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Anotación: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Booleana] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Mapa] | `MAP`-grupo anotado<br><br>(`<key-type>` debe `STRING`) | `MapType`<br><br>(`keyType` debe `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET y CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Cadena] | `String` | `System.String` | `String` |
| [!UICONTROL Doble] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Largo] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Número entero] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL corto] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Fecha] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booleana] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Mapa] | `Map` | (N/A) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike y Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Cadena] | `string` | `String` | `string` |
| [!UICONTROL Doble] | `double` | `Double` | `double` |
| [!UICONTROL Largo] | `long` | `Integer` | `int64` |
| [!UICONTROL Número entero] | `int` | `Integer` | `int32` |
| [!UICONTROL corto] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Fecha] | `date` | `Integer`<br>(milisegundos de Unix) | `int64`<br>(milisegundos de Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(milisegundos de Unix) | `int64`<br>(milisegundos de Unix) |
| [!UICONTROL Booleana] | `bool` | `Integer`<br>(0/1 binario) | `bool` |
| [!UICONTROL Mapa] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definición de tipos de campo XDM en la API {#define-fields}

La API del Registro de esquemas permite definir campos personalizados mediante el uso de formatos y restricciones opcionales. Consulte la guía de [definición de campos personalizados en la API del Registro de esquemas](../tutorials/custom-fields-api.md) para obtener más información.
