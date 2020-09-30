---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;date and time functions;datetime functions;datetime;date;time;
solution: Experience Platform
title: Funciones de fecha y hora
topic: developer guide
description: Las funciones de fecha y hora se utilizan para realizar operaciones de fecha y hora en valores dentro del lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 4%

---


# Funciones de fecha y hora

Las funciones de fecha y hora se utilizan para realizar operaciones de fecha y hora en valores dentro de [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Mes actual

La `currentMonth` función devuelve el mes actual como un entero.

**Format**

```sql
currentMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el mes de nacimiento de la persona es el mes actual.

```sql
person.birthMonth = currentMonth()
```

## Obtener mes

La `getMonth` función devuelve el mes, como un entero, en función de una marca de tiempo determinada.

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el mes de nacimiento de la persona es en junio.

```sql
person.birthdate.getMonth() = 6
```

## Año actual

La `currentYear` función devuelve el año actual como un entero.

**Format**

```sql
currentYear()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el producto se vendió en el año en curso.

```sql
product.saleYear = currentYear()
```

## Obtener año

La `getYear` función devuelve el año, como un entero, en función de una marca de tiempo determinada.

**Format**

```sql
{TIMESTAMP}.getYear()
```

**Ejemplo**

La siguiente consulta de PQL comprueba si el año de nacimiento de la persona cae en 1991, 1992, 1993, 1994 o 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Día actual del mes

La `currentDayOfMonth` función devuelve el día actual del mes como un entero.

**Format**

```sql
currentDayOfMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el día de nacimiento de la persona coincide con el día del mes actual.

```sql
person.birthDay = currentDayOfMonth()
```

## Obtener día del mes

La `getDayOfMonth` función devuelve el día, como un entero, en función de una marca de tiempo determinada.

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el artículo se vendió en los primeros 15 días del mes.

```sql
product.sale.getDayOfMonth() <= 15
```

## Ocurre

La `occurs` función compara la función de marca de tiempo dada con un período de tiempo fijo.

**Format**

La `occurs` función se puede escribir con cualquiera de los siguientes formatos:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argumento | Descripción |
| --------- | ----------- |
| `{COMPARISON}` | Operador de comparación. Puede ser cualquiera de los siguientes operadores: `>`, `>=`, `<`, `<=`, `=`, `!=`. Encontrará más información sobre las funciones de comparación en el documento [de funciones de](./comparison-functions.md)comparación. |
| `{INTEGER}` | Un entero no negativo. |
| `{TIME_UNIT}` | Una unidad de tiempo. Puede ser cualquiera de las siguientes palabras: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries``millennium``millennia`,. |
| `{DIRECTION}` | Preposición que describe cuándo comparar la fecha. Puede ser cualquiera de las siguientes palabras: `before`, `after`, `from`. |
| `{TIME}` | Puede ser un literal de marca de hora (`today`, `now`, `yesterday`, `tomorrow`), una unidad de tiempo relativa (una de `this`, `last`o `next` seguida de una unidad de tiempo) o un atributo de marca de hora. |

>[!NOTE]
>
>El uso de la palabra `on` es opcional. Está ahí para mejorar la legibilidad de algunas combinaciones, como `timestamp occurs on date(2019,12,31)`.

**Ejemplo**

La siguiente consulta PQL comprueba si el artículo se vendió la semana pasada.

```sql
product.saleDate occurs last week
```

La siguiente consulta PQL comprueba si un artículo se vendió entre el 8 de enero de 2015 y el 1 de julio de 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Ahora

`now` es una palabra reservada que representa la marca de tiempo de la ejecución de PQL.

**Ejemplo**

La siguiente consulta PQL comprueba si un artículo se vendió exactamente tres horas antes.

```sql
product.saleDate occurs = 3 hours before now
```

## Hoy

`today` es una palabra reservada que representa la marca de hora del inicio del día de la ejecución de PQL.

**Ejemplo**

La siguiente consulta PQL comprueba si el cumpleaños de una persona era hace tres días.

```sql
person.birthday occurs = 3 days before today
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de fecha y hora, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
