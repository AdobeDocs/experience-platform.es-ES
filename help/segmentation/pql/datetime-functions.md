---
solution: Experience Platform
title: Funciones de fecha y hora PQL
description: Las funciones de fecha y hora se utilizan para realizar operaciones de fecha y hora en valores dentro del lenguaje de consulta de perfil (PQL).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 4%

---

# Funciones de fecha y hora

Las funciones de fecha y hora se utilizan para realizar operaciones de fecha y hora en los valores dentro de [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Mes actual

El `currentMonth` La función devuelve el mes actual en forma de entero.

**Formato**

```sql
currentMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el mes de nacimiento de la persona es el mes actual.

```sql
person.birthMonth = currentMonth()
```

## Obtener mes

El `getMonth` función devuelve el mes como un entero, en función de una marca de tiempo determinada.

**Formato**

```sql
{TIMESTAMP}.getMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el mes de nacimiento de la persona es junio.

```sql
person.birthdate.getMonth() = 6
```

## Año actual

El `currentYear` La función devuelve el año actual como un entero.

**Formato**

```sql
currentYear()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el producto se vendió en el año actual.

```sql
product.saleYear = currentYear()
```

## Obtener año

El `getYear` función devuelve el año, como un entero, en función de una marca de tiempo determinada.

**Formato**

```sql
{TIMESTAMP}.getYear()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el año de nacimiento de la persona cae en 1991, 1992, 1993, 1994 o 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Día actual del mes

El `currentDayOfMonth` La función devuelve el día actual del mes en forma de entero.

**Formato**

```sql
currentDayOfMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el día de nacimiento de la persona coincide con el día actual del mes.

```sql
person.birthDay = currentDayOfMonth()
```

## Obtener día del mes

El `getDayOfMonth` función devuelve el día, como un entero, en función de una marca de tiempo determinada.

**Formato**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Ejemplo**

La siguiente consulta PQL comprueba si el artículo se vendió en los primeros 15 días del mes.

```sql
product.sale.getDayOfMonth() <= 15
```

## Ocurre

El `occurs` compara la función de marca de tiempo dada con un período de tiempo fijo.

**Formato**

El `occurs` se puede escribir utilizando cualquiera de los siguientes formatos:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argumento | Descripción |
| --------- | ----------- |
| `{COMPARISON}` | Un operador de comparación. Puede ser cualquiera de los siguientes operadores: `>`, `>=`, `<`, `<=`, `=`, `!=`. Encontrará más información sobre las funciones de comparación en la [documento de funciones de comparación](./comparison-functions.md). |
| `{INTEGER}` | Un entero no negativo. |
| `{TIME_UNIT}` | Una unidad de tiempo. Puede ser cualquiera de las siguientes palabras: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Una preposición que describe cuándo comparar la fecha. Puede ser cualquiera de las siguientes palabras: `before`, `after`, `from`. |
| `{TIME}` | Puede ser un literal de marca de tiempo (`today`, `now`, `yesterday`, `tomorrow`), una unidad de tiempo relativa (una de `this`, `last`, o `next` seguido de una unidad de tiempo) o un atributo de marca de tiempo. |

>[!NOTE]
>
>Uso de la palabra `on` es opcional. Está ahí para mejorar la legibilidad de algunas combinaciones, como `timestamp occurs on date(2019,12,31)`.

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

`today` es una palabra reservada que representa la marca de tiempo del inicio del día de la ejecución de PQL.

**Ejemplo**

La siguiente consulta PQL comprueba si el cumpleaños de una persona fue hace tres días.

```sql
person.birthday occurs = 3 days before today
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de fecha y hora, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
