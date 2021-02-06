---
keywords: Experience Platform;inicio;temas populares;PQL;pql;lenguaje de consulta de perfil
solution: Experience Platform
title: Descripción general del lenguaje de Consulta de perfil (PQL)
topic: developer guide
description: Esta guía proporciona una descripción general de PQL, que abarca las directrices de formato y proporciona expresiones PQL de ejemplo.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 3%

---


# [!DNL Profile Query Language] Información general (PQL)

[!DNL Profile Query Language] (PQL) es un lenguaje de consulta compatible con  [!DNL Experience Data Model] (XDM) diseñado para admitir la definición y ejecución de consultas de segmentación para  [!DNL Real-time Customer Profile] datos.

Esta guía proporciona una descripción general de PQL, que abarca las directrices de formato y proporciona expresiones PQL de ejemplo.

## Formato de consulta PQL

Las consultas PQL tienen la siguiente firma:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

El parámetro de entrada puede ser un simple elemento primitivo, como un booleano o una cadena, o un tipo más complejo, como un objeto, una matriz o un mapa.

Existen tres maneras diferentes de hacer referencia a los parámetros de entrada dentro del cuerpo de una expresión PQL:

### Referencia implícita al primer parámetro

En el ejemplo siguiente, como el primer parámetro siempre está en contexto, se puede hacer una referencia de propiedad (`homeAddress`) directamente en él.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Referencia explícita al primer parámetro

En el ejemplo siguiente, `$1` hace referencia al primer parámetro. Como resultado, `$2` haría referencia al segundo parámetro, etc.

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
| Número entero | Un tipo de datos que representa un número entero. Puede ser positivo, negativo o cero. | `-201`,  `0`,  `412` |
| Duplicada | Un tipo de datos que representa cualquier número real. Puede ser positivo, negativo o cero. | `-51.24`,  `3.14`,  `0.6942058` |
| Fecha | Tipo de datos que se puede utilizar para crear fechas basadas en el año, mes y día como parámetros enteros. Tiene el formato `date(year, month, day)` | `date(2020, 3, 14)` |
| Matriz | Tipo de datos que se compone como un grupo de otros valores literales. Utiliza corchetes para agrupar y comas para delimitar entre diferentes valores. <br> **Nota:** No se puede acceder directamente a las propiedades de los elementos de una matriz. Por lo tanto, si necesita acceder a una propiedad dentro de una matriz, el método admitido es `select X from array where X.item = ...`. <br> PQL se reserva la palabra  `xEvent` para hacer referencia a una matriz de eventos de experiencia vinculados a un perfil. | `[1, 4, 7]`,  `["US", "CA"]` |
| Referencias de tiempo relativas | Palabras reservadas que pueden utilizarse para crear referencias de intervalo de tiempo y marca de tiempo. <ul><li>ahora, hoy, ayer, mañana</li><li>esto, último, siguiente</li><li>antes, después, de</li><li>milisegundos, segundos, minutos, horas, días, semanas, meses, años, décadas, siglos o milenios</li></ul> | `X.timestamp occurs before today`,  `X.timestamp occurs last month`,  `X.timestamp occurs <= 3 days before now` |


## Funciones PQL

La siguiente tabla describe las diferentes categorías de las funciones PQL admitidas, incluyendo vínculos a documentación adicional para obtener más información.

| Categoría | Definición |
| -------- | ---------- |
| Booleano | Se utiliza para implementar álgebra booleana dentro de PQL. Encontrará más información sobre estas funciones en el [documento de funciones booleanas](./boolean-functions.md). |
| Comparación | Se utiliza para comparar diferentes elementos PQL. Encontrará más información sobre estas funciones en el documento [funciones de comparación](./comparison-functions.md). |
| Matriz, lista y conjunto | Se utiliza para interactuar con matrices, listas y conjuntos. Encontrará más información sobre estas funciones en el documento de funciones [array, lista y set](./array-functions.md). |
| Mapa | Se utiliza para interactuar con mapas. Encontrará más información sobre estas funciones en el [documento de funciones de mapa](./map-functions.md). |
| Cadena | Se utiliza para interactuar con cadenas. Encontrará más información sobre estas funciones en el documento [funciones de cadena](./string-functions.md). |
| Objeto | Se utiliza para interactuar con objetos. Encontrará más información sobre estas funciones en el documento [de funciones de objeto](./object-functions.md). |
| Aritmética | Se utiliza para realizar aritmética básica en elementos PQL. Encontrará más información sobre estas funciones en el [documento de funciones aritméticas](./arithmetic-functions.md) |
| Agregación | Se utiliza para combinar los resultados de una matriz en un resultado único. Encontrará más información sobre las funciones de agregación en el documento [funciones de agregación](./aggregation-functions.md). |
| Fecha y hora | Se utiliza junto con objetos date, time y datetime. Encontrará más información sobre estas funciones en el [documento de funciones de fecha y hora](./datetime-functions.md). |
| Filtro | Se utiliza para filtrar datos dentro de matrices. Encontrará más información sobre estas funciones en el documento [de funciones de filtro](./filter-functions.md). |
| Cuantificadores lógicos | Se utiliza para afirmar condiciones dentro de una matriz. Puede encontrar más información en el documento de cuantificadores lógicos [](./logical-quantifiers.md). |
| Varios | Las funciones que no encajan en ninguna de las categorías anteriores se encuentran en el [documento de funciones varias](./misc-functions.md). |

## Pasos siguientes

Ahora que ha aprendido a utilizar [!DNL Profile Query Language], puede utilizar PQL al crear y modificar segmentos. Para obtener más información sobre segmentación, lea la [información general de segmentación](../home.md).