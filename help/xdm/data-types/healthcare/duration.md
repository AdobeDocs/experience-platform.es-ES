---
title: Tipo de datos de duración
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de duración (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL Tipo de datos de duración]

[!UICONTROL Duration] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe una cantidad de tiempo. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de duración](../../images/data-types/healthcare/duration.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | Cadena | La forma codificada de la unidad de tiempo. |
| [!UICONTROL Sistema] | `system` | Cadena | Sistema que describe la unidad codificada, representada como URI. |
| [!UICONTROL Unidad] | `unit` | Cadena | La unidad de tiempo representada en milisegundos, segundos, minutos, horas, días, semanas, meses o años. Los valores de esta propiedad deben ser iguales a uno o varios de los siguientes valores de enumeración conocidos. <li> `ms` (milisegundos) </li> <li> `s` (segundos) </li> <li> `min` (minutos) </li> <li> `h` (horas) </li>  <li> `d` (días) </li> <li> `wk` (semanas) </li> <li> `mo` (meses) </li> <li> `a` (años) </li> |
| [!UICONTROL Valor] | `value` | Duplicada | El valor numérico de la unidad de tiempo. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
