---
keywords: Experience Platform;home;popular topics;PQL;pql;profile query language
solution: Experience Platform
title: Introducción al lenguaje de Consulta de perfil (PQL)
topic: developer guide
description: Esta guía proporciona una descripción general de PQL, que abarca las directrices de formato y proporciona expresiones PQL de ejemplo.
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 3%

---


# [!DNL Profile Query Language] Información general (PQL)

[!DNL Profile Query Language] (PQL) es un lenguaje de consulta compatible con [!DNL Experience Data Model] (XDM) diseñado para admitir la definición y ejecución de consultas de segmentación para [!DNL Real-time Customer Profile] datos.

Esta guía proporciona una descripción general de PQL, que abarca las directrices de formato y proporciona expresiones PQL de ejemplo.

## Formato de consulta PQL

Las consultas PQL tienen la siguiente firma:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

El parámetro de entrada puede ser un simple elemento primitivo, como un booleano o una cadena, o un tipo más complejo, como un objeto, una matriz o un mapa.

Existen tres maneras diferentes de hacer referencia a los parámetros de entrada dentro del cuerpo de una expresión PQL:

### Referencia implícita al primer parámetro

En el ejemplo siguiente, como el primer parámetro siempre está en contexto, se puede hacer una referencia de propiedad (`homeAddress`) directamente a él.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Referencia explícita al primer parámetro

En el ejemplo siguiente, `$1` hace referencia al primer parámetro. Como resultado, `$2` se referiría al segundo parámetro, etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Uso de variables con nombre, con notación lambda

En el ejemplo siguiente, `Profile` es un nombre de variable que puede elegir el autor de la consulta.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Literales PQL

PQL proporciona compatibilidad con los siguientes tipos de literales:

| Literal | Definición | Ejemplo |
| ------- | ---------- | ------- |
| Cadena | Tipo de datos compuesto por caracteres rodeados de comillas de doble. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Tipo de datos verdadero o falso. | `true`, `false` |
| Número entero | Un tipo de datos que representa un número entero. Puede ser positivo, negativo o cero. | `-201`, `0`, `412` |
| Duplicada | Un tipo de datos que representa cualquier número real. Puede ser positivo, negativo o cero. | `-51.24`, `3.14`, `0.6942058` |
| Fecha | Tipo de datos que se puede utilizar para crear fechas basadas en el año, mes y día como parámetros enteros. Tiene el formato `date(year, month, day)` | `date(2020, 3, 14)` |
| Matriz | Tipo de datos que se compone como un grupo de otros valores literales. Utiliza corchetes para agrupar y comas para delimitar entre diferentes valores. <br> **Nota:** No se puede acceder directamente a las propiedades de los elementos de una matriz. Por lo tanto, si necesita acceder a una propiedad dentro de una matriz, el método admitido es `select X from array where X.item = ...`. <br> PQL se reserva la palabra `xEvent` para hacer referencia a una matriz de eventos de experiencia vinculados a un perfil. | `[1, 4, 7]`, `["US", "CA"]` |
| Referencias de tiempo relativas | Palabras reservadas que pueden utilizarse para crear referencias de intervalo de tiempo y marca de tiempo. <ul><li>ahora, hoy, ayer, mañana</li><li>esto, último, siguiente</li><li>antes, después, de</li><li>milisegundos, segundos, minutos, horas, días, semanas, meses, años, décadas, siglos o milenios</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Funciones PQL

La siguiente tabla describe las diferentes categorías de las funciones PQL admitidas, incluyendo vínculos a documentación adicional para obtener más información.

| Categoría | Definición |
| -------- | ---------- |
| Booleano | Se utiliza para implementar álgebra booleana dentro de PQL. Encontrará más información sobre estas funciones en el documento [de funciones](./boolean-functions.md)booleanas. |
| Comparación | Se utiliza para comparar diferentes elementos PQL. Encontrará más información sobre estas funciones en el documento [de funciones de](./comparison-functions.md)comparación. |
| Matriz, lista y conjunto | Se utiliza para interactuar con matrices, listas y conjuntos. Encontrará más información sobre estas funciones en el documento [de funciones](./array-functions.md)array, lista y set. |
| Mapa | Se utiliza para interactuar con mapas. Puede encontrar más información sobre estas funciones en el documento [de funciones de](./map-functions.md)mapa. |
| Cadena | Se utiliza para interactuar con cadenas. Encontrará más información sobre estas funciones en el documento [de funciones de](./string-functions.md)cadena. |
| Objeto | Se utiliza para interactuar con objetos. Puede encontrar más información sobre estas funciones en el documento [de funciones de](./object-functions.md)objeto. |
| Aritmética | Se utiliza para realizar aritmética básica en elementos PQL. Encontrará más información sobre estas funciones en el documento de funciones [aritméticas](./arithmetic-functions.md) |
| Agregación | Se utiliza para combinar los resultados de una matriz en un resultado único. Puede encontrar más información sobre las funciones de agregación en el documento [de funciones de](./aggregation-functions.md)agregación. |
| Fecha y hora | Se utiliza junto con objetos date, time y datetime. Encontrará más información sobre estas funciones en el documento [de funciones de](./datetime-functions.md)fecha y hora. |
| Filtro | Se utiliza para filtrar datos dentro de matrices. Encontrará más información sobre estas funciones en el documento [de funciones de](./filter-functions.md)filtro. |
| Cuantificadores lógicos | Se utiliza para afirmar condiciones dentro de una matriz. Puede encontrar más información en el documento [de cuantificadores](./logical-quantifiers.md)lógicos. |
| Varios | Las funciones que no encajan en ninguna de las categorías anteriores se encuentran en el documento [de funciones](./misc-functions.md)diversas. |

## Pasos siguientes

Ahora que ha aprendido a usar [!DNL Profile Query Language], puede usar PQL al crear y modificar segmentos. Para obtener más información sobre la segmentación, lea la información general [sobre la](../home.md)segmentación.