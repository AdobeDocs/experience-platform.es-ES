---
title: Definición de campos XDM en la API del Registro de Esquema
description: Obtenga información sobre cómo definir distintos campos al crear recursos del Modelo de datos de experiencia (XDM) personalizados en la API del Registro de esquemas.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Definición de campos XDM en la API del Registro de Esquema

Todos los campos del Modelo de datos de experiencia (XDM) se definen mediante el [Esquema JSON](https://json-schema.org/) restricciones que se aplican a su tipo de campo, con restricciones adicionales para nombres de campo que son aplicadas por Adobe Experience Platform. La API del Registro de esquemas permite definir campos personalizados en los esquemas mediante el uso de formatos y restricciones opcionales. Los tipos de campo XDM se exponen mediante el atributo de nivel de campo. `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` es un valor generado por el sistema y, por lo tanto, no es necesario que agregue esta propiedad al JSON para su campo al utilizar la API (excepto cuando [creación de tipos de mapa personalizados](#maps)). Una práctica recomendada es utilizar tipos de esquema JSON (como `string` y `integer`) con las restricciones de mínimo/máximo adecuadas, tal como se definen en la siguiente tabla.

En la tabla siguiente se describe el formato adecuado para definir distintos tipos de campos, incluidos los que tienen propiedades opcionales. Encontrará más información sobre las propiedades opcionales y las palabras clave específicas del tipo en la [Documentación del esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para empezar, busque el tipo de campo deseado y utilice el código de ejemplo proporcionado para crear la solicitud de API de [creación de un grupo de campos](../api/field-groups.md#create) o [creación de un tipo de datos](../api/data-types.md#create).

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
"sampleField": { "type": "cadena", "patrón": "^[A-Z]{2}$", "maxLength": 2 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "uri" }</pre>
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
    <td>Los valores de enumeración restringidos se proporcionan en la sección <code>enum</code> , mientras que las etiquetas opcionales de cara al cliente para cada valor se pueden proporcionar en <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Value 1", "value2": "Value 2", "value3": "Valor 3" }, "predeterminado": "value1" }</pre>
    <br>Tenga en cuenta que <code>meta:enum</code> value does <strong>not</strong> declare una enumeración o conduzca cualquier validación de datos por su cuenta. En la mayoría de los casos, las cadenas proporcionadas en <code>meta:enum</code> también se proporcionan en <code>enum</code> para garantizar que los datos estén restringidos. Sin embargo, hay algunos casos de uso en los que <code>meta:enum</code> se proporciona sin <code>enum</code> matriz. Consulte el tutorial en <a href="../tutorials/suggested-values.md">definición de valores sugeridos</a> para obtener más información.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -9007199254740992, "máximo": 9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -2147483648, "máximo": 2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Cortocircuito]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -32768, "máximo": 32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -128, "máximo": 128 }</pre>
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
"sampleField": { "type": "booleano", "predeterminado": false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date", "example": ["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "ejemplos": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Una matriz de tipos escalares básicos (p. ej. cadenas):
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "matriz", "elementos": { "type": "string" } }</pre>
      Matriz de objetos definida por otro esquema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "matriz", "elementos": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL (objeto)</td>
    <td></td>
    <td>La variable <code>type</code> atributo de cada subcampo definido en <code>properties</code> se puede definir con cualquier tipo escalar:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "número" } } } }</pre>
      Los campos de tipo objeto se pueden definir haciendo referencia a la variable <code>$id</code> de un tipo de datos:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Un campo de tipo mapa es esencialmente un campo de tipo objeto con un conjunto de claves sin restricciones. Al igual que los objetos, los mapas tienen un <code>type</code> valor de <code>object</code>, pero sus <code>meta:xdmType</code> se configura explícitamente como <code>map</code>.<br><br>Un mapa <strong>no debe</strong> defina cualquier propiedad. It <strong>must</strong> definir una sola <code>additionalProperties</code> para describir el tipo de valores contenidos en el mapa (cada mapa solo puede contener un tipo de datos). La variable <code>type</code> debe ser <code>string</code> o <code>integer</code>.<br/><br/>Campo de asignación con valores de tipo cadena:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" } }</pre>
    Consulte la sección siguiente para obtener más información sobre la creación de tipos de mapa personalizados en XDM.
    </td>
  </tr>
</table>

## Creación de tipos de mapa personalizados {#maps}

Para admitir datos &quot;similares a mapas&quot; de forma eficaz en XDM, los objetos se pueden anotar con un `meta:xdmType` configure como `map` para dejar claro que un objeto debe administrarse como si el conjunto de claves no estuviera limitado. Los datos que se incorporan en los campos de asignación deben utilizar claves de cadena y solo valores de cadena o entero (tal y como determinan `additionalProperties.type`).

XDM impone las siguientes restricciones al uso de esta sugerencia de almacenamiento:

* Los tipos de mapa DEBEN ser del tipo `object`.
* Los tipos de mapa NO DEBEN tener propiedades definidas (en otras palabras, definen objetos &quot;vacíos&quot;).
* Los tipos de mapa DEBEN incluir un `additionalProperties.type` campo que describe los valores que pueden colocarse dentro del mapa, ya sea `string` o `integer`.

Asegúrese de que solo está utilizando campos de tipo mapa cuando es absolutamente necesario, ya que presentan los siguientes inconvenientes de rendimiento:

* El tiempo de respuesta del servicio de consulta de Adobe Experience Platform se degrada de tres segundos a diez segundos para 100 millones de registros.
* Los mapas deben tener menos de 16 claves o, de lo contrario, pueden degradarse aún más.

La interfaz de usuario de Platform también tiene limitaciones en la forma en que puede extraer las claves de los campos de tipo mapa. Mientras que los campos de tipo objeto se pueden expandir, los mapas se muestran como un solo campo en su lugar.

## Pasos siguientes

Esta guía explica cómo definir diferentes tipos de campos en la API. Para obtener más información sobre el formato de los tipos de campo XDM, consulte la guía de [Restricciones de tipo de campo XDM](../schema/field-constraints.md).
