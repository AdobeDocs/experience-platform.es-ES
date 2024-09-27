---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;asignador;asignación;preparación de datos;preparación de datos;
solution: Experience Platform
title: Administrar formatos de datos con preparación de datos
description: Este documento ofrece información general sobre cómo se administran los distintos tipos de datos en la preparación de datos.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: a49140853124f4f7beee87a739c8e670838947f4
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 11%

---

# Administrar formatos de datos con preparación de datos

La preparación de datos puede gestionar de forma fiable diferentes formatos de datos introducidos en Adobe Experience Platform. Este documento describe cómo se tratan los distintos formatos de datos con la preparación de datos.

## Booleanos {#booleans}

Si el tipo de origen es una cadena y el tipo de destino es un booleano, la preparación de datos puede analizar automáticamente el valor y convertirlo en un booleano.

Los valores `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true` y `TRUE` se analizarán automáticamente para que sean `true`.

Los valores `n`, `N`, `no`, `NO`, `off`, `OFF`, `false` y `FALSE` se analizarán automáticamente para que sean `false`.

## Fechas {#dates}

La preparación de datos admite funciones de fecha, tanto como cadenas como objetos datetime.

### Formato de función de fecha

La función de fecha convierte cadenas y objetos datetime en un objeto ZonedDateTime con formato ISO 8601.

**Formato**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATE}` | Requerido. Cadena que representa la fecha. |
| `{FORMAT}` | Opcional. Cadena que representa el formato de la fecha de origen. Encontrará más información sobre el formato de cadena en la [sección de cadenas de formato de fecha y hora](#format). |
| `{DEFAULT_DATE}` | Opcional. La fecha predeterminada que se devolverá si la fecha proporcionada es nula. |

Por ejemplo, la expresión `date(orderDate, "yyyy-MM-dd")` convertirá un valor `orderDate` de &quot;31 de diciembre de 2020&quot; en un valor de fecha y hora de &quot;2020-12-31&quot;.

### Conversiones de función de fecha

Cuando los campos de cadena de los datos entrantes se asignan a campos de fecha en esquemas que utilizan Experience Data Model (XDM), el formato de fecha debe mencionarse explícitamente. Si no se menciona explícitamente, la preparación de datos intentará convertir los datos de entrada haciéndolos coincidir con los siguientes formatos. Una vez encontrado un formato coincidente, dejará de evaluar los formatos posteriores.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> La preparación de datos intentará convertir las cadenas en fechas lo mejor posible. Sin embargo, estas conversiones pueden dar lugar a resultados no deseados. Por ejemplo, el valor de cadena &quot;12112020&quot; coincide con el patrón &quot;ddMMyyyy&quot;, pero el usuario puede haber pensado que la fecha se leyera con el patrón &quot;ddMMyyyy&quot;. Como resultado, los usuarios deben mencionar explícitamente el formato de fecha para las cadenas.

### Cadenas de formato de fecha y hora {#format}

>[!TIP]
>
>Actualmente, la función de fecha de la ingesta por lotes elimina los milisegundos si los valores de fecha están en este formato: `2024-05-05 20:39:00.005` PST. Para conservar los milisegundos, use este formato: `2024-05-05 20:39:00.005-0800`

En la tabla siguiente se muestra qué letras de patrón se definen para las cadenas de formato. Tenga en cuenta que las letras distinguen entre mayúsculas y minúsculas.

| Símbolo | Significado | Presentación | Ejemplo |
| ------ | ------- | ------------ | ------- |
| G | La era | Texto | AD; Anno Domini; A |
| Y | Año, según la semana ISO | Número | 1996; 96 |
| y | El año | Número | 2004; 04 |
| M/L | Mes del año | Número/Texto | 7; 07; Jul; Julio; J |
| w | Semana del año | Número | 27 |
| W | Semana del mes | Número | 3 |
| D | Día del año | Número | 189 |
| d | Día del mes | Número | 10 |
| F | Día de la semana de un mes | Número | 2 |
| E | Nombre del día de la semana | Texto | Martes; Mar |
| u | Día de la semana, como número. 1 representa lunes, ..., 7 representa domingo | Número | 1 |
| a | Marcador AM/PM | Texto | PM |
| H | Hora del día (0-23) | Número | 0 |
| k | Hora del día (1-24) | Número | 24 |
| K | Hora a.m./p.m. (0-11) | Número | 0 |
| h | Hora en AM/PM (1-12) | Número | 12 |
| m | Minuto de la hora | Número | 38 |
| s | Segundo en el minuto | Número | 44 |
| S | Milisegundo | Número | 245 |
| z | Zona horaria | Zona horaria general | Hora estándar del Pacífico; PST; GMT-08:00 |
| Z | Zona horaria | Zona horaria RFC 822 | -0800 |
| X | Zona horaria | Zona horaria ISO 8601 | -08; -0800; -08:00 |
| V | ID de zona horaria | Texto | América/Los_Ángeles |
| O | Desplazamiento de zona horaria | Texto | GMT+8 |
| P/Q | Trimestre del año | Número/Texto | 3; 03; T3; 3er trimestre |

## Mapas {#maps}

Actualmente no se admiten mapas en [!DNL Data Prep].
