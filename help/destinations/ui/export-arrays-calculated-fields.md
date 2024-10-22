---
title: Utilice campos calculados para exportar matrices como cadenas
type: Tutorial
description: Aprenda a utilizar campos calculados para exportar matrices de Real-Time CDP a destinos de almacenamiento en la nube como cadenas.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 849d42e36921e60b6ac3a5e89336b954e64a35d7
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 7%

---

# Utilice campos calculados para exportar matrices como cadenas{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Compatibilidad con exportación de matrices"
>abstract="<p>Utilice el control **Añadir campo calculado** para exportar matrices de valores int, cadena, booleanos y objetos desde Experience Platform al destino de almacenamiento en la nube deseado.</p><p> Las matrices deben exportarse como cadenas utilizando la función `array_to_string`. Consulte la documentación para ver ejemplos exhaustivos y más funciones compatibles.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=es#examples" text="Ejemplos"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=es#known-limitations" text="Limitaciones conocidas"

>[!AVAILABILITY]
>
>* La funcionalidad para exportar matrices a través de campos calculados está disponible de forma general.

Obtenga información sobre cómo exportar matrices a través de campos calculados desde Real-Time CDP a [destinos de almacenamiento en la nube](/help/destinations/catalog/cloud-storage/overview.md) como cadenas. Lea este documento para comprender los casos de uso habilitados por esta funcionalidad.

Obtenga información detallada sobre los campos calculados, qué son y por qué importan. Lea las páginas vinculadas a continuación para obtener una introducción a los campos calculados en la preparación de datos y más información sobre todas las funciones disponibles:

* [Guía e información general de IU](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funciones de preparación de datos](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Matrices y otros tipos de objetos en Platform {#arrays-strings-other-objects}

En Experience Platform, puede utilizar [esquemas XDM](/help/xdm/home.md) para administrar diferentes tipos de campos. Antes de añadir compatibilidad con las exportaciones de matrices, podía exportar campos de tipo par clave-valor simples, como cadenas de Experience Platform a los destinos deseados. Un ejemplo de un campo de este tipo que se admitía para la exportación anteriormente es `personalEmail.address`:`johndoe@acme.org`.

Otros tipos de campo de Experience Platform incluyen campos de matriz. Obtenga más información acerca de [administrar campos de matriz en la interfaz de usuario del Experience Platform](/help/xdm/ui/fields/array.md). Además de los tipos de campo admitidos anteriormente, ahora puede exportar objetos de matriz como el ejemplo siguiente, concatenados en una cadena mediante la función `array_to_string`.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Vea más abajo [varios ejemplos](#examples) de cómo puede usar diversas funciones para obtener acceso a elementos de matrices, transformar y filtrar matrices, unir elementos de matrices en una cadena y mucho más.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones conocidas que actualmente se aplican a esta funcionalidad:

* En este momento no se admite la exportación a archivos JSON o Parquet *con esquemas jerárquicos*. Puede exportar matrices a archivos CSV, JSON y Parquet *solo como cadenas*, mediante la función `array_to_string`.

## Requisitos previos {#prerequisites}

[Conéctese](/help/destinations/ui/connect-destination.md) a un destino de almacenamiento en la nube deseado, avance en los [pasos de activación para los destinos de almacenamiento en la nube](/help/destinations/ui/activate-batch-profile-destinations.md) y vaya al paso [asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Cómo exportar campos calculados {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Habilite el esquema de salida jerárquico"
>abstract="Active esta opción si desea exportar estructuras jerárquicas como matrices."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Añadir campos calculados deshabilitado"
>abstract="Este control está deshabilitado porque ha seleccionado exportar estructuras planas al conectarse al destino."

En el paso de asignación del flujo de trabajo de activación para los destinos de almacenamiento en la nube, seleccione **[!UICONTROL Agregar campo calculado]**.

![Agregue el campo calculado resaltado en el paso de asignación del flujo de trabajo de activación por lotes.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Esto abre una ventana modal en la que se pueden seleccionar funciones y campos para exportar atributos fuera del Experience Platform.

![Ventana modal de la funcionalidad de campo calculado sin función seleccionada todavía.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Por ejemplo, utilice la función `array_to_string` en el campo `organizations` como se muestra a continuación para exportar la matriz de organizaciones como una cadena en un archivo CSV. Ver [más información sobre este y otros ejemplos más abajo](#array-to-string-function-export-arrays).

![Ventana modal de la funcionalidad de campo calculado con la función de matriz a cadena seleccionada.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Seleccione **[!UICONTROL Guardar]** para conservar el campo calculado y volver al paso de asignación.

![Ventana modal de la funcionalidad de campo calculado con la función matriz a cadena seleccionada y el control Guardar resaltado.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Cuando vuelva al paso de asignación del flujo de trabajo, rellene el **[!UICONTROL campo de destino]** con el valor del encabezado de columna que desee para este campo en los archivos exportados.

![Paso de asignación con el campo de destino resaltado.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleccionar campo de destino 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Cuando esté listo, seleccione **[!UICONTROL Siguiente]** para continuar con el siguiente paso del flujo de trabajo de activación.

![Paso de asignación con el campo de destino resaltado y un valor de destino rellenado.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funciones compatibles de ejemplo para exportar matrices {#supported-functions}

Todas las [funciones de preparación de datos](/help/data-prep/functions.md) documentadas son compatibles al activar datos en destinos basados en archivos.

Las funciones siguientes, específicas para gestionar exportaciones de matrices, se documentan junto con ejemplos.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Ejemplos de funciones utilizadas para exportar matrices {#examples}

Consulte los ejemplos y la información adicional en las secciones siguientes para ver algunas de las funciones enumeradas anteriormente. Para el resto de las funciones enumeradas, consulte la [documentación de funciones generales en la sección Preparación de datos](/help/data-prep/functions.md).

### Función `array_to_string` para exportar matrices {#array-to-string-function-export-arrays}

Utilice la función `array_to_string` para concatenar los elementos de una matriz en una cadena, utilizando un separador deseado, como `_` o `|`.

Por ejemplo, puede combinar los siguientes campos XDM a continuación, como se muestra en la captura de pantalla de asignación, utilizando una sintaxis `array_to_string('_',organizations)`:

* Matriz `organizations`
* `person.name.firstName` cadena
* `person.name.lastName` cadena
* `personalEmail.address` cadena

![Ejemplo de asignación que incluye la función array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo los elementos de la matriz se concatenan en una sola cadena utilizando el carácter `_`.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Función `filterArray` para exportar matrices filtradas

Utilice la función `filterArray` para filtrar los elementos de una matriz exportada. Puede combinar esta función con la función `array_to_string` descrita anteriormente.

Continuando con el objeto de matriz `organizations` desde arriba, puede escribir una función como `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, devolviendo las organizaciones con un valor para `founded` en el año 2021 o más reciente.

![Ejemplo de la función filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo los dos elementos de la matriz que cumplen el criterio se concatenan en una sola cadena utilizando el carácter `_`.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Función `transformArray` para exportar matrices transformadas

Utilice la función `transformArray` para transformar los elementos de una matriz exportada. Puede combinar esta función con la función `array_to_string` descrita anteriormente.

Continuando con el objeto de matriz `organizations` desde arriba, puede escribir una función como `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`, devolviendo los nombres de las organizaciones convertidas a mayúsculas.

![Ejemplo de la función transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo los tres elementos de la matriz se transforman y concatenan en una sola cadena utilizando el carácter `_`.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### Función `iif` para exportar matrices {#iif-function-export-arrays}

Utilice la función `iif` para exportar elementos de una matriz en ciertas condiciones. Por ejemplo, si continúa con el objeto de matriz `organizations` desde arriba, puede escribir una función condicional simple como `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Ejemplo de asignación que incluye la función iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. En este caso, el primer elemento de la matriz es Marketing, por lo que la persona es miembro del departamento de marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### Función `add_to_array` para exportar matrices {#add-to-array-function-export-arrays}

Utilice la función `add_to_array` para agregar elementos a una matriz exportada. Puede combinar esta función con la función `array_to_string` descrita anteriormente.

Continuando con el objeto de matriz `organizations` desde arriba, puede escribir una función como `source: array_to_string('_', add_to_array(organizations,"2023"))`, que devuelve las organizaciones de las que es miembro una persona en el año 2023.

![Ejemplo de asignación que incluye la función add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo los tres elementos de la matriz se concatenan en una sola cadena utilizando el carácter `_` y 2023 también se anexa al final de la cadena.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### Función `flattenArray` para exportar matrices aplanadas

Utilice la función `flattenArray` para acoplar una matriz multidimensional exportada. Puede combinar esta función con la función `array_to_string` descrita anteriormente.

Continuando con el objeto de matriz `organizations` desde arriba, puede escribir una función como `array_to_string('_', flattenArray(organizations))`. Tenga en cuenta que la función `array_to_string` aplana la matriz de entrada de forma predeterminada en una cadena.

El resultado es el mismo que para la función `array_to_string` descrita anteriormente.

### Función `coalesce` para exportar matrices {#coalesce-function-export-arrays}

Utilice la función `coalesce` para acceder al primer elemento no nulo de una matriz y exportarlo a una cadena.

Por ejemplo, puede combinar los siguientes campos XDM a continuación, como se muestra en la captura de pantalla de asignación, utilizando una sintaxis `coalesce(subscriptions.hasPromotion)` para devolver el primer valor `true` de `false` en la matriz:

* Matriz `"subscriptions.hasPromotion": [null, true, null, false, true]`
* `person.name.firstName` cadena
* `person.name.lastName` cadena
* `personalEmail.address` cadena

![Ejemplo de asignación que incluye la función de combinación.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo se exporta en el archivo el primer valor `true` no nulo de la matriz.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### Función `size_of` para exportar matrices {#sizeof-function-export-arrays}

Utilice la función `size_of` para indicar cuántos elementos existen en una matriz. Por ejemplo, si tiene un objeto de matriz `purchaseTime` con varias marcas de tiempo, puede usar la función `size_of` para indicar cuántas compras independientes realizó una persona.

Por ejemplo, puede combinar los siguientes campos XDM a continuación, como se muestra en la captura de pantalla de asignación.

* Matriz `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` que indica cinco tiempos de compra independientes por parte del cliente
* `personalEmail.address` cadena

![Ejemplo de asignación que incluye la función size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo la segunda columna indica el número de elementos de la matriz, correspondiente al número de compras independientes realizadas por el cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Acceso a matrices basadas en índices {#index-based-array-access}

Puede acceder al índice de una matriz para exportar un solo elemento de la matriz. Por ejemplo, similar al ejemplo anterior para la función `size_of`, si desea tener acceso y exportar solo la primera vez que un cliente ha comprado un determinado producto, puede utilizar `purchaseTime[0]` para exportar el primer elemento de la marca de tiempo, `purchaseTime[1]` para exportar el segundo elemento de la marca de tiempo, `purchaseTime[2]` para exportar el tercer elemento de la marca de tiempo, etc.

![Ejemplo de asignación que muestra cómo se puede tener acceso a un elemento de una matriz.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

En este caso, el archivo de salida tiene el siguiente aspecto, al exportar la primera vez que el cliente ha realizado una compra:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### Funciones `first` y `last` para exportar matrices {#first-and-last-functions-export-arrays}

Utilice las funciones `first` y `last` para exportar el primer o último elemento de una matriz. Por ejemplo, si continúa con el objeto de matriz `purchaseTime` con varias marcas de tiempo de los ejemplos anteriores, puede utilizarlas en funciones para exportar la primera o la última hora de compra realizada por una persona.

![Ejemplo de asignación que incluye las funciones primera y última.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

En este caso, el archivo de salida tiene el siguiente aspecto, al exportar la primera y la última vez que el cliente ha realizado una compra:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->