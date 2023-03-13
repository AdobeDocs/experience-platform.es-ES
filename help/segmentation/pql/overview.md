---
keywords: Experience Platform;inicio;temas populares;PQL;pql;lenguaje de consulta de perfil
solution: Experience Platform
title: Información general sobre el lenguaje de consulta de perfil (PQL)
description: Esta guía proporciona información general sobre el PQL, e incluye directrices de formato y expresiones PQL de ejemplo.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 3%

---

# [!DNL Profile Query Language] Información general de (PQL)

[!DNL Profile Query Language] (PQL) es un [!DNL Experience Data Model] Lenguaje de consulta compatible con (XDM) diseñado para admitir la definición y ejecución de consultas de segmentación para [!DNL Real-Time Customer Profile] datos.

Esta guía proporciona información general sobre el PQL, e incluye directrices de formato y expresiones PQL de ejemplo.

## Formato de consulta PQL

Las consultas PQL tienen la siguiente firma:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

El parámetro de entrada puede ser un primitivo simple, como un booleano o una cadena, o un tipo más complejo, como un objeto, una matriz o un mapa.

Existen tres formas diferentes de hacer referencia a los parámetros de entrada dentro del cuerpo de una expresión PQL:

### Referencia implícita al primer parámetro

En el ejemplo siguiente, como el primer parámetro siempre está en contexto, una referencia de propiedad (`homeAddress`) se puede hacer directamente a ella.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Referencia explícita al primer parámetro

En el ejemplo siguiente, `$1` hace referencia al primer parámetro. Como resultado, `$2` haría referencia al segundo parámetro, etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Uso de variables con nombre, usando la notación lambda

En el ejemplo siguiente, `Profile` es un nombre de variable que puede elegir el autor de la consulta.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Literales PQL

PQL proporciona compatibilidad con los siguientes tipos literales:

| Literal | Definición | Ejemplo |
| ------- | ---------- | ------- |
| Cadena | Un tipo de datos compuesto por caracteres entre comillas dobles. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Un tipo de datos que puede ser verdadero o falso. | `true`, `false` |
| Número entero | Un tipo de datos que representa un número entero. Puede ser positivo, negativo o cero. | `-201`, `0`, `412` |
| Doble | Un tipo de datos que represente cualquier número real. Puede ser positivo, negativo o cero. | `-51.24`, `3.14`, `0.6942058` |
| Fecha | Un tipo de datos que se puede utilizar para crear fechas basadas en el año, el mes y el día como parámetros enteros. Tiene el formato `date(year, month, day)` | `date(2020, 3, 14)` |
| Matriz | Un tipo de datos que se comprende como un grupo de otros valores literales. Utiliza corchetes para agrupar y comas para delimitar entre distintos valores. <br> **Nota:** No puede acceder directamente a las propiedades de los elementos de una matriz. Por lo tanto, si necesita acceder a una propiedad dentro de una matriz, el método admitido es `select X from array where X.item = ...`. <br> PQL reserva la palabra `xEvent` para hacer referencia a una matriz de eventos de experiencia vinculados a un perfil. | `[1, 4, 7]`, `["US", "CA"]` |
| Referencias de tiempo relativo | Palabras reservadas que se pueden utilizar para formar referencias de intervalo de tiempo y marca de tiempo. <ul><li>ahora, hoy, ayer, mañana</li><li>esto, lo último, lo siguiente</li><li>antes, después y desde</li><li>milisegundo(s), segundo(s), minuto(s), hora(s), día(s), semana(s), mes(es), año(s), década(s), siglo/siglos, milenio/milenio</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Funciones PQL

La siguiente tabla describe las diferentes categorías de funciones PQL admitidas, incluidos los vínculos a documentación adicional para obtener más información.

| Categoría | Definición |
| -------- | ---------- |
| Booleano | Se utiliza para implementar álgebra booleana dentro de PQL. Encontrará más información sobre estas funciones en la [documento de funciones booleanas](./boolean-functions.md). |
| Comparación | Se utiliza para comparar entre diferentes elementos PQL. Encontrará más información sobre estas funciones en la [documento de funciones de comparación](./comparison-functions.md). |
| Matriz, lista y conjunto | Se utiliza para interactuar con matrices, listas y conjuntos. Encontrará más información sobre estas funciones en la [documento de funciones de matriz, lista y conjunto](./array-functions.md). |
| Mapa | Se utiliza para interactuar con mapas. Encontrará más información sobre estas funciones en la [documento de funciones de mapa](./map-functions.md). |
| Cadena | Se utiliza para interactuar con cadenas. Encontrará más información sobre estas funciones en la [documento de funciones de cadena](./string-functions.md). |
| Objeto | Se utiliza para interactuar con objetos. Encontrará más información sobre estas funciones en la [documento de funciones de objeto](./object-functions.md). |
| Aritmética | Se utiliza para realizar operaciones aritméticas básicas en elementos PQL. Encontrará más información sobre estas funciones en la [documento de funciones aritméticas](./arithmetic-functions.md) |
| Agregación | Se utiliza para combinar los resultados de una matriz en un resultado singular. Puede encontrar más información sobre las funciones de agregación en la [documento de funciones de agregación](./aggregation-functions.md). |
| Fecha y hora | Se utiliza junto con los objetos fecha, hora y fecha y hora. Encontrará más información sobre estas funciones en la [documento de funciones de fecha y hora](./datetime-functions.md). |
| Filtro | Se utiliza para filtrar datos dentro de matrices. Encontrará más información sobre estas funciones en la [documento de funciones de filtro](./filter-functions.md). |
| Cuantificadores lógicos | Se utiliza para afirmar condiciones dentro de una matriz. Encontrará más información en la [documento de cuantificadores lógicos](./logical-quantifiers.md). |
| Varios | Las funciones que no se ajustan a ninguna de las categorías anteriores se encuentran en la [documento de funciones varias](./misc-functions.md). |

## Pasos siguientes

Ahora que ha aprendido a utilizar [!DNL Profile Query Language], puede utilizar PQL al crear y modificar segmentos. Para obtener más información sobre la segmentación, lea la [resumen de segmentación](../home.md).
