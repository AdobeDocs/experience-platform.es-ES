---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía ui;mapper;asignación;fecha;funciones de fecha;fechas; fechas;
solution: Experience Platform
title: Funciones de fecha de preparación de datos
topic: overview
description: Este documento presenta las funciones de fecha utilizadas con la preparación de datos.
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 16%

---


# Funciones de fecha de preparación de datos

La preparación de datos admite funciones de fecha, tanto como cadenas como como objetos de fecha y hora.

## Conversiones de funciones de fecha

Cuando los campos de cadena de datos entrantes se asignan a campos de fecha en esquemas que utilizan el modelo de datos de experiencia (XDM), el formato de fecha debe mencionarse explícitamente. Si no se menciona explícitamente, la preparación de datos intentará convertir los datos de entrada haciendo coincidir con los siguientes formatos. Una vez encontrado un formato coincidente, dejará de evaluar cualquier formato subsiguiente.

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
> La preparación de datos intentará convertir las cadenas a fechas lo mejor posible. Sin embargo, estas conversiones pueden dar lugar a resultados no deseados. Por ejemplo, el valor de cadena &quot;12112020&quot; coincide con el patrón &quot;Dindyyyy&quot;, pero es posible que el usuario haya pensado que la fecha se lea con el patrón &quot;ddMMyyyy&quot;. Como resultado, los usuarios deben mencionar explícitamente el formato de fecha para las cadenas.

## Cadenas de formato de fecha y hora

La siguiente tabla muestra las letras de patrón definidas para las cadenas de formato. Tenga en cuenta que las letras distinguen entre mayúsculas y minúsculas.

| Símbolo | Significado | Presentación | Ejemplo |
| ------ | ------- | ------------ | ------- |
| G | La era | Texto | AD; Anno Domini; A |
| Y | Año, basado en la semana ISO | Número | 1996; 96 |
| y | El año | Número | 2004; 04 |
| M/L | Mes del año | Número/Texto | 7; 07; Jul; Julio; J |
| w | Semana del año | Número | 27 |
| W | Semana del mes | Número | 3 |
| D | Día del año | Número | 189 |
| d | Día del mes | Número | 10 |
| F | Día de la semana en un mes | Número | 2 |
| E | Nombre del día de la semana | Texto | Martes; Tue |
| u | Día de la semana, como número. 1 representa el lunes, ..., 7 representa el domingo | Número | 1 |
| a | Marcador AM/PM | Texto | PM |
| H | Hora del día (0-23) | Número | 0 |
| k | Hora del día (1-24) | Número | 24 |
| K | Hora en AM/PM (0-11) | Número | 0 |
| h | Hora en AM/PM (1-12) | Número | 12 |
| m | Minuto en la hora | Número | 38 |
| s | Segundo en el minuto | Número | 44 |
| S | Millisegundo | Número | 245 |
| z | Zona horaria | Huso horario general | Hora estándar del Pacífico; PST; GMT-08:00 |
| Z | Zona horaria | Zona horaria RFC 822 | -0800 |
| X | Zona horaria | Zona horaria ISO 8601 | -08; -0800; -08:00 |
| V | ID de zona horaria | Texto | América/Los Ángeles |
| O | Desplazamiento de zona horaria | Texto | GMT+8 |
| Q/q | Trimestre del año | Número/Texto | 3; 03; T3; Tercer trimestre |

**Ejemplo**

La expresión `date(orderDate, "yyyy-MM-dd")` convertirá un valor `orderDate` de &quot;31 de diciembre de 2020&quot; en un valor datetime de &quot;2020-12-31&quot;.