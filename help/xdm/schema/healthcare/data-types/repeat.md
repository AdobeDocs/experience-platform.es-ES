---
title: Repetir tipo de datos
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia repetida (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# [!UICONTROL Repetir] tipo de datos

[!UICONTROL Repetir] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona un conjunto de reglas que describen cuándo se programa un evento. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Repetir estructura de tipo de datos](../../../images/healthcare/data-types/reference.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Período enlazado] | `boundsPeriod` | [[!UICONTROL Período]](../data-types/period.md) | Las horas de inicio y finalización. |
| [!UICONTROL Intervalo enlazado] | `boundsRange` | [[!UICONTROL Intervalo]](../data-types/range.md) | El límite de rango. |
| [!UICONTROL Duración enlazada] | `boundsDuration` | [[!UICONTROL Duración]](../data-types/duration.md) | El límite de duración. |
| [!UICONTROL Recuento] | `count` | Entero | Número de veces que se va a repetir, con un valor mínimo de `0`. |
| [!UICONTROL Recuento Máximo] | `countMax` | Entero | Número máximo de veces que se va a repetir, con un valor mínimo de `0`. |
| [!UICONTROL Día De La Semana] | `dayOfWeek` | Matriz de cadenas | Matriz de cadenas que detalla los días disponibles. Los valores de esta propiedad deben ser iguales a uno o varios de los siguientes valores de enumeración conocidos. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Duración] | `duration` | Duplicada | La cantidad de tiempo. |
| [!UICONTROL Duración máxima] | `durationMax` | Duplicada | El período de tiempo máximo. |
| [!UICONTROL Unidad de duración] | `durationUnit` | Cadena | La unidad de duración. Los valores de esta propiedad deben ser iguales a uno o varios de los siguientes valores de enumeración conocidos. <li> `s` (segundos) </li> <li> `min` (minutos) </li> <li> `h` (por hora) </li> <li> `d` (diario) </li>  <li> `wk` (semanal) </li> <li> `mo` (mensual) </li> <li> `a` (anual)</li> |
| [!UICONTROL Frecuencia] | `frequency` | Duplicada | Número de repeticiones que deben producirse dentro de un período, con un valor mínimo de `0`. |
| [!UICONTROL Frecuencia máxima] | `frequencyMax` | Duplicada | Número máximo de repeticiones que deben producirse con un período, con un valor mínimo de `0`. |
| [!UICONTROL Desplazamiento] | `offset` | Entero | Los minutos hasta el evento (antes o después). |
| [!UICONTROL Período] | `period` | Duplicada | La duración durante la cual se aplica la frecuencia. |
| [!UICONTROL Período Máximo] | `periodMax` | Duplicada | El límite superior del periodo. |
| [!UICONTROL Unidad de período] | `periodUnit` | Cadena | La unidad de tiempo. Los valores de esta propiedad deben ser iguales a uno o varios de los siguientes valores de enumeración conocidos. <li> `s` (segundos) </li> <li> `min` (minutos) </li> <li> `h` (por hora) </li> <li> `d` (diario) </li>  <li> `wk` (semanal) </li> <li> `mo` (mensual) </li> <li> `a` (anual)</li> |
| [!UICONTROL Hora Del Día] | `timeOfDay` | Matriz de cadenas | Hora del día a la que se producirá la acción. |
| [!UICONTROL When] | `when` | Matriz de cadenas | El código del período de tiempo de la acción. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
