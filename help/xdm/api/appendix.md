---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Apéndice para desarrolladores de Esquema Registry
topic: developer guide
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# Apéndice

Este documento proporciona información adicional relacionada con el trabajo con la API del Registro de Esquemas.

## Modo de compatibilidad

El modelo de datos de experiencia (XDM) es una especificación documentada públicamente, impulsada por Adobe para mejorar la interoperabilidad, la expresividad y el poder de las experiencias digitales. Adobe mantiene el código fuente y las definiciones XDM formales en un proyecto de código [abierto en GitHub](https://github.com/adobe/xdm/). Estas definiciones se escriben en notación estándar XDM, utilizando JSON-LD (JavaScript Object Notation for Linked Data) y Esquema JSON como gramática para definir esquemas XDM.

Al consultar las definiciones XDM formales en el repositorio público, puede ver que el XDM estándar difiere de lo que ve en Adobe Experience Platform. Lo que se ve en la plataforma de experiencia se llama Modo de compatibilidad y proporciona una asignación sencilla entre el XDM estándar y la forma en que se utiliza dentro de la plataforma.

### Funcionamiento del modo de compatibilidad

El modo de compatibilidad permite que el modelo JSON-LD de XDM funcione con la infraestructura de datos existente alterando los valores dentro del XDM estándar manteniendo la semántica igual. Utiliza una estructura JSON anidada, que muestra esquemas en un formato de árbol.

La principal diferencia que notará entre el modo XDM estándar y el modo de compatibilidad es la eliminación del prefijo &quot;xdm:&quot; para los nombres de campo.

A continuación se muestra una comparación paralela que muestra los campos relacionados con el cumpleaños (con los atributos &quot;description&quot; eliminados) tanto en el modo XDM estándar como en el modo de compatibilidad. Observe que los campos Modo de compatibilidad incluyen una referencia al campo XDM y su tipo de datos en los atributos &quot;meta:xdmField&quot; y &quot;meta:xdmType&quot;.

<table>
  <th>XDM estándar</th>
  <th>Modo de compatibilidad</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title": "Fecha de nacimiento", "tipo": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Fecha de nacimiento", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Año de nacimiento", "tipo": "integer", "Minimum": 1, "máximo": 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Fecha de nacimiento", "tipo": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Fecha de nacimiento", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Año de nacimiento", "tipo": "integer", "Minimum": 1, "máximo": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### ¿Por qué es necesario el modo de compatibilidad?

Adobe Experience Platform está diseñado para trabajar con múltiples soluciones y servicios, cada uno con sus propios desafíos y limitaciones técnicos (por ejemplo, cómo ciertas tecnologías manejan caracteres especiales). Para superar estas limitaciones, se desarrolló el Modo de compatibilidad.

La mayoría de los servicios de la plataforma de experiencia, incluidos Catálogo, Data Lake y Perfil del cliente en tiempo real, utilizan el modo de compatibilidad en lugar del XDM estándar. La API del Registro de Esquema también utiliza el Modo de compatibilidad y todos los ejemplos de este documento se muestran mediante el Modo de compatibilidad.

Vale la pena saber que se produce una asignación entre el XDM estándar y la manera en que se realiza en la plataforma de experiencia, pero no debería afectar al uso de los servicios de plataforma.

El proyecto de código abierto está disponible para usted, pero cuando se trata de interactuar con los recursos a través del Registro de Esquemas, los ejemplos de API de este documento proporcionan las mejores prácticas que debe conocer y seguir.

## Definición de tipos de campo XDM en la API {#field-types}

Los esquemas XDM se definen utilizando estándares de Esquema JSON y tipos de campo básicos, con restricciones adicionales para los nombres de campo que se aplican en Experience Platform. XDM permite definir tipos de campo adicionales mediante el uso de formatos y restricciones opcionales. Los tipos de campo XDM están expuestos por el atributo de nivel de campo `meta:xdmType`.

>[!NOTE] `meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario agregar esta propiedad al JSON para el campo. Lo mejor es utilizar tipos de Esquemas JSON (como cadena e entero) con las restricciones mínimas/máximas adecuadas, tal como se define en la tabla siguiente.

En la tabla siguiente se describe el formato adecuado para definir tipos de campos escalares y tipos de campos más específicos mediante propiedades opcionales. Puede obtener más información sobre las propiedades opcionales y las palabras clave específicas del tipo a través de la documentación [del Esquema](https://json-schema.org/understanding-json-schema/reference/type.html)JSON.

Para empezar, busque el tipo de campo deseado y utilice el código de muestra proporcionado para generar la solicitud de API.

<table>
  <tr>
    <th>Tipo<br/>deseado(meta:xdmType)</th>
    <th>JSON<br/>(Esquema JSON)</th>
    <th>Ejemplo de código</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type:<br/><br/><strong>stringPropiedades opcionales:</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type: formato<br/>de cadena: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type:<br/><br/><strong>stringOptional, propiedad:</strong><br/>
      <ul>
        <li>predeterminada</li>
      </ul>
    </td>
    <td>Especifique las etiquetas de opciones orientadas al cliente mediante "meta:enum":
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "enum": [ "valor1", "valor2", "valor3" ], "meta:enum": { "value1": "Valor 1", "valor2": "Valor 2", "valor3": "Valor 3" }, "predeterminado": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>number</td>
    <td>type:<br/>número mínimo: ±2,23 × 10^308<br/>máximo: ±1,80 × 10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type:<br/>entero máximo:2^53+1<br>mínimo:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -9007199254740992, "máximo": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type:<br/>entero máximo:2^31<br>mínimo:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -2147483648, "máximo": 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type:<br/>entero máximo:2^15<br>mínimo:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -32768, "máximo": 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type:<br/>entero máximo:2^7<br>mínimo:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -128, "máximo": 128 }
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
        "sampleField": { "type": "boolean", "default": false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type: formato<br/>de cadena: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date", "samples": ["2004-10-23"] }
      </pre>
      Fecha tal como se define en <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sección 5.6</a>, donde "full-date" = date-fullyear "-" date-month "-" date-mday (AAAA-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type: formato<br/>de cadena: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date-time", "ejemplos": ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Fecha y hora tal como se define en <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sección 5.6</a>, donde "fecha y hora" = fecha completa "T" a tiempo completo:<br/>(AAAA-MM-DD'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type se puede definir con cualquier tipo escalar:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "type": "string" } }
      </pre>
      Matriz de objetos definida por otro esquema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "$ref": "id" } }
      </pre>
      Donde "id" es el {id} del esquema de referencia.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>propiedades de contenidos.{field}.type se puede definir con cualquier tipo escalar:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } } }
      </pre>
      Campo de tipo "objeto" definido por un esquema de referencia:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "$ref": "id" }
      </pre>
      Donde "id" es el {id} del esquema de referencia.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type:<br/><br/><strong>objectNota:</strong><br/>El uso del tipo de datos 'map' está reservado para el uso de esquemas del sector y del proveedor y no está disponible para su uso en campos definidos por el inquilino. Se utiliza en esquemas estándar cuando los datos se representan como claves que se asignan a algún valor, o cuando las claves no pueden incluirse razonablemente en un esquema estático y deben tratarse como valores de datos.</td>
    <td>UN 'mapa' NO DEBE definir ninguna propiedad. DEBE definir un solo esquema "extraProperties" para describir el tipo de valores contenidos en el "mapa". Un 'mapa' en XDM puede contener un solo tipo de datos. Los valores pueden ser cualquier definición de esquema XDM válida, incluyendo una matriz o un objeto, o como referencia a otro esquema (mediante $ref).<br/><br/>Campo de mapa con valores de tipo 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "extraProperties":{ "type": "string" } }
      </pre>
    Campo de asignación con valores como matriz de cadenas:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "extraProperties":{ "type": "array", "items": { "type": "string" } } } }
      </pre>
    Campo de mapa que hace referencia a otro esquema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "extraProperties":{ "$ref": "id" } }
      </pre>
      Donde "id" es el {id} del esquema de referencia.
    </td>
  </tr>
</table>


## Asignación de tipos XDM a otros formatos

La tabla siguiente describe la asignación entre &quot;meta:xdmType&quot; y otros formatos de serialización.

| Tipo<br>XDM(meta:xdmType) | JSON<br>(Esquema JSON) | Parquet<br>(tipo/anotación) | Spark SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Cadena | System.String | Cadena | string | Cadena | string |
| number | type:number | DOBLE | DoubleType | java.lang.Doble | Duplicada | System.Doble | Número | doble | Duplicada | doble |
| long | tipo:<br>entero máximo:2^53+1<br>mínimo:-2^53+1 | INT64 | LongType | java.lang.Long | Largo | System.Int64 | Número | long | Número entero | int64 |
| int | tipo:<br>entero máximo:2^31<br>mínimo:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Número | int | Número entero | int32 |
| short | tipo:<br>entero máximo:2^15<br>mínimo:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Corto | System.Int16 | Número | int | Número entero | int32 |
| byte | tipo:<br>entero máximo:2^7<br>mínimo:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Número | int | Número entero | int32 |
| Booleano | type:boolean | BOOLEAN | BooleanType | java.lang.Boolean | Booleano | System.Boolean | Booleano | bool | Número entero | Número entero | bool |
| date | type:<br>stringformat:date<br>(RFC 3339, sección 5.6) | INT32/FECHA | DateType | java.util.Date | java.util.Date | System.DateTime | Cadena | date | Entero<br>(milis unix) | int64<br>(milisegundos unix) |
| date-time | type:<br>stringformat:date-time<br>(RFC 3339, sección 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Cadena | timestamp | Entero<br>(milis unix) | int64<br>(milisegundos unix) |
| map | object | El grupo<br><br>anotado MAP&lt;<span>key_type</span>> DEBE ser STRING<br><br>&lt;<span>value_type</span>> tipo de valores de mapa | MapType<br><br>&quot;keyType&quot; DEBE ser StringType<br><br>&quot;valueType&quot; es el tipo de valores de asignación. | java.util.Map | Mapa | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |
