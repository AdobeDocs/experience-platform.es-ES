---
title: (Beta) Utilice campos calculados para exportar matrices en archivos de esquema plano
type: Tutorial
description: Aprenda a utilizar campos calculados para exportar matrices en archivos de esquema plano desde Real-Time CDP a destinos de almacenamiento en la nube.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 1%

---

# (Beta) Utilice campos calculados para exportar matrices en archivos de esquema plano {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Compatibilidad con matrices de exportación (Beta)"
>abstract="Utilice el **Añadir campo calculado** para exportar matrices simples de valores int, string o boolean desde Experience Platform al destino de almacenamiento en la nube deseado. Se aplican algunas limitaciones. Consulte la documentación para ver ejemplos exhaustivos y funciones compatibles."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Ejemplos"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Limitaciones conocidas"

>[!AVAILABILITY]
>
>* La funcionalidad para exportar matrices a través de campos calculados está actualmente en Beta. La documentación y las funcionalidades están sujetas a cambios.

Obtenga información sobre cómo exportar matrices a través de campos calculados desde Real-Time CDP en archivos de esquema plano a [destinos de almacenamiento en la nube](/help/destinations/catalog/cloud-storage/overview.md). Lea este documento para comprender los casos de uso habilitados por esta funcionalidad.

Obtenga información detallada sobre los campos calculados, qué son y por qué importan. Lea las páginas vinculadas a continuación para obtener una introducción a los campos calculados en la preparación de datos y más información sobre todas las funciones disponibles:

* [Guía e información general de IU](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funciones de preparación de datos](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>No todas las funciones enumeradas anteriormente son compatibles *al exportar campos a destinos de almacenamiento en la nube* uso de la funcionalidad de campos calculados. Consulte la [sección funciones compatibles](#supported-functions) más abajo para obtener más información.

## Matrices y otros tipos de objetos en Platform {#arrays-strings-other-objects}

En Experience Platform, puede utilizar [Esquemas XDM](/help/xdm/home.md) para administrar diferentes tipos de campo. Anteriormente, podía exportar campos de tipo de par clave-valor simples, como cadenas, fuera de Experience Platform a los destinos deseados. Un ejemplo de un campo de este tipo que era compatible con la exportación anteriormente es `personalEmail.address`:`johndoe@acme.org`.

Otros tipos de campo de Experience Platform incluyen campos de matriz. Más información sobre [administración de campos de matriz en la IU de Experience Platform](/help/xdm/ui/fields/array.md). Además de los tipos de campo admitidos anteriormente, ahora puede exportar objetos de matriz como: `organizations:[marketing, sales, engineering]`. Consulte más información a continuación [ejemplos extensos](#examples) Obtenga información sobre cómo utilizar varias funciones para acceder a elementos de matrices, unir elementos de matrices en una cadena, etc.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones conocidas para la versión beta de esta funcionalidad:

* En este momento no se admite la exportación a archivos JSON o Parquet con esquemas jerárquicos. Solo puede exportar matrices a archivos de esquema plano CSV, JSON y Parquet.
* En este momento, *solo puede exportar matrices simples (o matrices de valores primitivos) a destinos de almacenamiento en la nube*. Esto significa que se pueden exportar objetos de matriz que incluyen valores de cadena, int o booleanos. No se pueden exportar asignaciones o matrices de asignaciones u objetos La ventana modal de campos calculados sólo muestra las matrices que se pueden exportar.

## Requisitos previos {#prerequisites}

[Connect](/help/destinations/ui/connect-destination.md) a un destino de almacenamiento en la nube deseado, avance en el [pasos de activación para destinos de cloud storage](/help/destinations/ui/activate-batch-profile-destinations.md) y llegar al [asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) paso.

## Cómo exportar campos calculados {#how-to-export-calculated-fields}

En el paso Asignación del flujo de trabajo de activación para los destinos de almacenamiento en la nube, seleccione **[!UICONTROL (Beta) Agregar campo calculado]**.

![Agregue el campo calculado resaltado en el paso de asignación del flujo de trabajo de activación por lotes.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Se abrirá una ventana modal en la que se pueden seleccionar atributos que se pueden utilizar para exportar atributos fuera de Experience Platform.

>[!IMPORTANT]
>
>Solo algunos de los campos del esquema XDM están disponibles en la variable **[!UICONTROL Campo]** vista. Puede ver valores de cadena y matrices de valores de cadena, int y booleanos. Por ejemplo, la variable `segmentMembership` matriz no se muestra, ya que incluye otros valores de matriz.

![Ventana modal de la funcionalidad de campo calculado sin función seleccionada todavía.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Por ejemplo, utilice la variable `join` función en el `loyaltyID` como se muestra a continuación para exportar una matriz de ID de fidelidad como una cadena concatenada con un guion bajo en un archivo CSV. Ver [más información sobre este y otros ejemplos más adelante](#join-function-export-arrays).

![Ventana modal de la funcionalidad de campo calculado con la función de combinación seleccionada.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Seleccionar **[!UICONTROL Guardar]** para mantener el campo calculado y volver al paso de asignación.

![Ventana modal de la funcionalidad de campo calculado con la función de combinación seleccionada y el control Guardar resaltado.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Vuelva a la etapa de asignación del flujo de trabajo y rellene el **[!UICONTROL Campo de destino]** con un valor del encabezado de columna que desee para este campo en los archivos exportados.

![Paso de asignación con el campo de destino resaltado.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleccionar campo de destino 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Cuando esté listo, seleccione **[!UICONTROL Siguiente]** para continuar con el siguiente paso del flujo de trabajo de activación.

![Paso de asignación con el campo de destino resaltado y un valor de destino rellenado.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funciones compatibles {#supported-functions}

Tenga en cuenta que solo se admiten las siguientes funciones en la versión beta de los campos calculados y la compatibilidad con matrices para destinos:

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Ejemplos de funciones utilizadas para exportar matrices {#examples}

Consulte los ejemplos y la información adicional en las secciones siguientes para ver algunas de las funciones enumeradas anteriormente. Para el resto de las funciones enumeradas, consulte la [Documentación de funciones generales en la sección Preparación de datos](/help/data-prep/functions.md).

### `join` función para exportar matrices {#join-function-export-arrays}

Utilice el `join` para concatenar los elementos de una matriz en una cadena, utilizando un separador deseado, como `_` o `|`.

Por ejemplo, puede combinar los siguientes campos XDM a continuación, como se muestra en la captura de pantalla de asignación, utilizando un `join('_',loyalty.loyaltyID)` sintaxis:

* `"organizations": ["Marketing","Sales,"Finance"]` matriz
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Ejemplo de asignación que incluye la función de unión.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo los tres elementos de la matriz se concatenan en una sola cadena utilizando `_` carácter.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` función para exportar matrices {#iif-function-export-arrays}

Utilice el `iif` para exportar elementos de una matriz en ciertas condiciones. Por ejemplo, continuar con `organizations` objeto de matriz desde arriba, puede escribir una función condicional simple como `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Ejemplo de asignación que incluye la función iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. En este caso, el primer elemento de la matriz es Marketing, por lo que la persona es miembro del departamento de marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` función para exportar matrices {#add-to-array-function-export-arrays}

Utilice el `add_to_array` para añadir elementos a una matriz exportada. Puede combinar esta función con el `join` función descrita anteriormente.

Continuación con el `organizations` objeto de matriz desde arriba, puede escribir una función como `source: join('_', add_to_array(organizations,"2023"))`, que devuelve las organizaciones de las que es miembro una persona en el año 2023.

![Ejemplo de asignación que incluye la función add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo los tres elementos de la matriz se concatenan en una sola cadena utilizando `_` y 2023 también se anexa al final de la cadena.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` función para exportar matrices {#coalesce-function-export-arrays}

Utilice el `coalesce` para acceder al primer elemento no nulo de una matriz y exportarlo a una cadena.

Por ejemplo, puede combinar los siguientes campos XDM a continuación, como se muestra en la captura de pantalla de asignación, utilizando un `coalesce(subscriptions.hasPromotion)` sintaxis para devolver la primera `true` de `false` en la matriz:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` matriz
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Ejemplo de asignación que incluye la función coalesce.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo el primer valor no nulo `true` el valor de la matriz se exporta en el archivo.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` función para exportar matrices {#sizeof-function-export-arrays}

Utilice el `size_of` para indicar cuántos elementos existen en una matriz. Por ejemplo, si tiene un `purchaseTime` objeto de matriz con varias marcas de tiempo, puede utilizar la variable `size_of` función para indicar cuántas compras independientes realizó una persona.

Por ejemplo, puede combinar los siguientes campos XDM a continuación, como se muestra en la captura de pantalla de asignación.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` matriz que indica cinco momentos de compra independientes del cliente
* `personalEmail.address` string

![Ejemplo de asignación que incluye la función size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

En este caso, el archivo de salida tiene el siguiente aspecto. Observe cómo la segunda columna indica el número de elementos de la matriz, correspondiente al número de compras independientes realizadas por el cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Acceso a matrices basadas en índices {#index-based-array-access}

Puede acceder al índice de una matriz para exportar un solo elemento de la matriz. Por ejemplo, similar al ejemplo anterior para `size_of` función, si desea acceder y exportar solo la primera vez que un cliente ha comprado un determinado producto, puede utilizar `purchaseTime[0]` para exportar el primer elemento de la marca de tiempo, `purchaseTime[1]` para exportar el segundo elemento de la marca de tiempo, `purchaseTime[2]` para exportar el tercer elemento de la marca de tiempo, etc.

![Ejemplo de asignación que muestra cómo se puede acceder a un elemento de una matriz.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

En este caso, el archivo de salida tiene el siguiente aspecto, al exportar la primera vez que el cliente ha realizado una compra:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` y `last` funciones para exportar matrices {#first-and-last-functions-export-arrays}

Utilice el `first` y `last` funciones para exportar el primer o el último elemento de una matriz. Por ejemplo, continuar con `purchaseTime` Objeto de matriz con varias marcas de tiempo de los ejemplos anteriores, puede utilizarlas para funciones para exportar la primera o la última hora de compra realizada por una persona.

![Ejemplo de asignación que incluye las funciones primera y última.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

En este caso, el archivo de salida tiene el siguiente aspecto, al exportar la primera y la última vez que el cliente ha realizado una compra:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### `md5` y `sha256` funciones hash {#hashing-functions}

Además de las funciones específicas para exportar matrices o elementos de una matriz, puede utilizar funciones hash para cifrar atributos. Por ejemplo, si tiene información de identificación personal en los atributos, puede hash en esos campos al exportarlos.

Puede usar valores de cadena hash directamente, por ejemplo `md5(personalEmail.address)`. Si lo desea, también puede hash elementos individuales de campos de matriz, de esta manera: `md5(purchaseTime[0])`