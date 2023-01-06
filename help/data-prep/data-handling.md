---
keywords: Experience Platform;inicio;temas populares;asignación de csv;asignación de archivo csv;asignación de archivo csv a xdm;asignación de csv a xdm;guía de ui;asignador;asignación;preparación de datos;preparación de datos;preparación de datos;
solution: Experience Platform
title: Gestión de formatos de datos con la preparación de datos
description: Este documento ofrece información general sobre cómo se gestionan los distintos tipos de datos en la preparación de datos.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# Gestión de formatos de datos con la preparación de datos

La preparación de datos puede gestionar de forma fiable diferentes formatos de datos introducidos en Adobe Experience Platform. Este documento describe cómo se tratan los diferentes formatos de datos con la preparación de datos.

## Booleano {#booleans}

Si el tipo de origen es una cadena y el tipo de destino es booleano, la preparación de datos puede analizar automáticamente el valor y convertir el valor de origen en booleano.

Los valores `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`y `TRUE` se analizan automáticamente para `true`.

Los valores `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`y `FALSE` se analizan automáticamente para `false`.

## Fechas {#dates}

La preparación de datos admite funciones de fecha, tanto como cadenas como objetos datetime.

### Formato de la función de fecha

La función date convierte cadenas y objetos datetime para que se conviertan en un objeto ZonianDateTime con formato ISO 8601.

**Formato**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATE}` | Requerido. La cadena que representa la fecha. |
| `{FORMAT}` | Opcional. La cadena que representa el formato de la fecha de origen. Encontrará más información sobre el formato de cadena en la [sección de cadena de formato de fecha y hora](#format). |
| `{DEFAULT_DATE}` | Opcional. La fecha predeterminada que se devolverá si la fecha proporcionada es nula. |

Por ejemplo, la expresión `date(orderDate, "yyyy-MM-dd")` convertirá un `orderDate` valor de &quot;31 de diciembre de 2020&quot; en un valor de fecha y hora de &quot;2020-12-31&quot;.

### Conversiones de funciones de fecha

Cuando los campos de cadena de datos entrantes se asignan a campos de fecha en esquemas que utilizan Experience Data Model (XDM), el formato de fecha debe mencionarse explícitamente. Si no se menciona explícitamente, la preparación de datos intentará convertir los datos de entrada al hacerlos coincidir con los siguientes formatos. Una vez encontrado un formato coincidente, dejará de evaluar cualquier formato subsiguiente.

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
> La preparación de datos intentará convertir cadenas en fechas lo mejor posible. Sin embargo, estas conversiones pueden dar lugar a resultados no deseados. Por ejemplo, el valor de la cadena &quot;12112020&quot; coincide con el patrón &quot;MMddyyyy&quot;, pero es posible que el usuario haya pensado que la fecha se leyera con el patrón &quot;ddMMyyyy&quot;. Como resultado, los usuarios deben mencionar explícitamente el formato de fecha para las cadenas.

### Cadenas de formato de fecha y hora {#format}

En la tabla siguiente se muestran las letras de patrón definidas para las cadenas de formato. Tenga en cuenta que las letras distinguen entre mayúsculas y minúsculas.

| Símbolo | Significado | Presentación | Ejemplo |
| ------ | ------- | ------------ | ------- |
| G | La era | Texto | AD; Anno Domini; A |
| Y | Año, basado en la semana ISO | Número | 1996; 96 |
| y | El año | Número | 2004; 04 |
| M/L | Mes del año | Número/Texto | 7; 07; Jul; julio; J |
| w | Semana del año | Número | 27 |
| W | Semana del mes | Número | 3 |
| D | Día del año | Número | 189 |
| d | Día del mes | Número | 10 |
| F | Día de la semana de un mes | Número | 2 |
| E | Nombre del día de la semana | Texto | Martes; Tue |
| u | Día de la semana, como número. 1 representa lunes, ..., 7 representa domingo | Número | 1 |
| a | Marcador AM/PM | Texto | PM |
| H | Hora del día (0-23) | Número | 0 |
| k | Hora del día (1-24) | Número | 24 |
| K | Hora de la AM/PM (0-11) | Número | 0 |
| h | Hora a la am/pm (1-12) | Número | 12 |
| m | Minuto en la hora | Número | 38 |
| s | Segundo en el minuto | Número | 44 |
| S | Millisegundo | Número | 245 |
| z | Zona horaria | Zona horaria general | Hora estándar del Pacífico; PST; GMT-08:00 |
| Z | Zona horaria | Zona horaria RFC 822 | -0800 |
| X | Zona horaria | Zona horaria ISO 8601 | -08; -0800; -08:00 |
| V | ID de zona horaria | Texto | América/Los Ángeles |
| O | Desplazamiento de zona horaria | Texto | GMT+8 |
| Q/q | Trimestre del año | Número/Texto | 3; 03; T3; Trimestre 3 |

## Mapas {#maps}

Actualmente, los mapas no son compatibles con [!DNL Data Prep].
