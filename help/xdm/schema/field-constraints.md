---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;mezcla;Mezcla;Mezclas;Mezclas;mezclas;tipo de datos;tipos de datos;Tipo de datos;Tipo de datos;Tipo de datos;Tipo de datos;Tipo de datos;Tipo de datos;esquemas;Esquemas;Diseño de Esquema;mapa;Mapa;
solution: Experience Platform
title: Restricciones de tipo de campo XDM
topic: overview
description: Referencia para restricciones de tipo de campo XDM, incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 6%

---


# Restricciones de tipo de campo XDM

Los tipos de campo XDM que se seleccionan para los esquemas restringen los tipos de datos que dichos campos pueden contener. Este documento proporciona una visión general de cada tipo de campo principal, incluidos los otros formatos de serialización a los que se pueden asignar y cómo definir sus propios tipos de campo en la API para aplicar diferentes restricciones.

## Primeros pasos

Antes de utilizar esta guía, consulte los [conceptos básicos de la composición del esquema](./composition.md) para obtener una introducción a los esquemas, clases y mezclas XDM.

Si planea definir sus propios tipos de campo, se recomienda enfáticamente que inicio con la [guía para desarrolladores de Esquema Registry](../api/getting-started.md) para aprender a crear mezclas y tipos de datos para incluir los campos personalizados.

## Asignación de tipos XDM a otros formatos

La tabla siguiente describe la asignación entre cada tipo XDM (`meta:xdmType`) y otros formatos de serialización.

| Tipo XDM<br>(meta:xdmType) | JSON<br>(Esquema JSON) | Parquet<br>(tipo/anotación) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Cadena | System.String | Cadena | string | Cadena | string |
| entero | type:number | DOBLE | DoubleType | java.lang.Double | Duplicada | System.Double | Número | doble | Duplicada | doble |
| long | tipo:integer<br>máximo:2^53+1<br>mínimo:-2^53+1 | INT64 | LongType | java.lang.Long | Largo | System.Int64 | Número | long | Número entero | int64 |
| int | tipo:integer<br>máximo:2^31<br>mínimo:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Número | int | Número entero | int32 |
| short | tipo:integer<br>máximo:2^15<br>mínimo:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Corto | System.Int16 | Número | int | Número entero | int32 |
| byte | type:integer<br>máximo:2^7<br>mínimo:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Número | int | Número entero | int32 |
| Booleano | type:boolean | BOOLEAN | BooleanType | java.lang.Boolean | Booleano | System.Boolean | Booleano | bool | Número entero | Número entero | bool |
| date | type:string<br>format:date<br>(RFC 3339, sección 5.6) | INT32/FECHA | DateType | java.util.Date | java.util.Date | System.DateTime | Cadena | date | Entero<br>(milis unix) | int64<br>(milis unix) |
| date-time | type:string<br>format:date-time<br>(RFC 3339, sección 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Cadena | timestamp | Entero<br>(milis unix) | int64<br>(milis unix) |
| map | object | El grupo con anotaciones MAP<br><br>&lt;<span>key_type</span>> DEBE ser STRING<br><br>&lt;<span>value_type</span>> tipo de valores de mapa | MapType<br><br>&quot;keyType&quot; DEBE ser StringType<br><br>&quot;valueType&quot; es el tipo de valores de asignación. | java.util.Map | Mapa | — | object | object | map | map&lt;<span>key_type, valor_type</span>> |

## Definición de tipos de campo XDM en la API {#define-fields}

Los esquemas XDM se definen utilizando estándares [Esquema JSON](https://json-schema.org/) y tipos de campo básicos, con restricciones adicionales para nombres de campo que se aplican mediante [!DNL Experience Platform]. La [API del Registro de Esquema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) permite definir tipos de campo adicionales mediante el uso de formatos y restricciones opcionales. Los tipos de campo XDM están expuestos por el atributo de nivel de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario agregar esta propiedad al JSON para el campo. Lo mejor es utilizar tipos de Esquemas JSON (como cadena e entero) con las restricciones mínimas/máximas adecuadas, tal como se define en la tabla siguiente.

En la tabla siguiente se describe el formato adecuado para definir tipos de campos escalares y tipos de campos más específicos mediante propiedades opcionales. Encontrará más información sobre las propiedades opcionales y las palabras clave específicas del tipo en la [documentación de Esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para comenzar, busque el tipo de campo deseado y utilice el código de muestra proporcionado para generar la solicitud de API para [crear una mezcla](../api/mixins.md#create) o [crear un tipo de datos](../api/data-types.md#create).

<table>
  <tr>
    <th>Tipo deseado<br/>(meta:xdmType)</th>
    <th>JSON<br/>(Esquema JSON)</th>
    <th>Ejemplo de código</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type: string<br/><br/><strong>Propiedades opcionales:</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type: string<br/>format: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type: string<br/><br/><strong>Propiedad opcional:</strong><br/>
      <ul>
        <li>predeterminada</li>
      </ul>
    </td>
    <td>Especifique las etiquetas de opciones orientadas al cliente mediante "meta:enum":
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "enum": [
              "value1",
              "value2",
              "value3"
          ],
          "meta:enum": {
              "value1": "Valor 1",
              "value2": "Valor 2",
              "value3": "Valor 3"
          },
          "default": "value1"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>entero</td>
    <td>type: número<br/>mínimo: ±2,23 × 10^308<br/>máximo: ±1,80 × 10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type: entero<br/>máximo:2^53+1<br>mínimo:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "mínimo": -9007199254740992,
          "máximo": 9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type: entero<br/>máximo:2^31<br>mínimo:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "mínimo": -2147483648,
          "máximo": 2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type: entero<br/>máximo:2^15<br>mínimo:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "mínimo": -32768,
          "máximo": 32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type: integer<br/>máximo:2^7<br>mínimo:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "mínimo": -128,
          "máximo": 128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>Booleano</td>
    <td><br/>type: boolean<br/>{true, false}<br/><br/><strong>Propiedad opcional:</strong><br/>
      <ul>
        <li>predeterminada</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "boolean",
          "default": false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type: string<br/>format: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date",
          "ejemplos": ["2004-10-23"]
        }
      </pre>
      Fecha tal como se define en <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sección 5.6</a>, donde "full-date" = date-fullyear "-" date-month "-" date-mday (AAAA-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type: string<br/>format: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date-time",
          "ejemplos": ["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      Fecha y hora tal como se define en <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sección 5.6</a>, donde "fecha y hora" = fecha completa "T" a tiempo completo:<br/>(AAAA-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type se puede definir con cualquier tipo escalar:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      </pre>
      Matriz de objetos definida por otro esquema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "$ref": "id"
          }
        }
      </pre>
      Donde "id" es el {id} del esquema de referencia.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>propiedades de contenidos.{field}.type se puede definir con cualquier tipo escalar:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "properties": {
            "field1": {
              "type": "string"
            },
            "field2": {
              "type": "number"
            }
          }
        }
      </pre>
      Campo de tipo "objeto" definido por un esquema de referencia:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "$ref": "id"
        }
      </pre>
      Donde "id" es el {id} del esquema de referencia.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type: object<br/><br/><strong>Nota:</strong><br/>El uso del tipo de datos 'map' está reservado para el uso de esquemas del sector y del proveedor y no está disponible para utilizarse en campos definidos por el inquilino. Se utiliza en esquemas estándar cuando los datos se representan como claves que se asignan a algún valor, o cuando las claves no pueden incluirse razonablemente en un esquema estático y deben tratarse como valores de datos.</td>
    <td>UN 'mapa' NO DEBE definir ninguna propiedad. DEBE definir un único esquema "[!UICONTROL extraProperties]" para describir el tipo de valores contenidos en el 'mapa'. Un 'mapa' en XDM puede contener un solo tipo de datos. Los valores pueden ser cualquier definición de esquema XDM válida, incluyendo una matriz o un objeto, o como referencia a otro esquema (mediante $ref).<br/><br/>Campo de mapa con valores de tipo 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "extraProperties":{
            "type": "string"
          }
        }
      </pre>
    Campo de asignación con valores como matriz de cadenas:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "extraProperties":{
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      </pre>
    Campo de mapa que hace referencia a otro esquema:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "extraProperties":{
            "$ref": "id"
          }
        }
      </pre>
      Donde "id" es el {id} del esquema de referencia.
    </td>
  </tr>
</table>
