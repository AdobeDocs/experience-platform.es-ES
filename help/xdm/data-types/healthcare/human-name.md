---
title: Tipo de datos de nombre humano
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de nombres humanos (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# [!UICONTROL Nombre humano] tipo de datos

[!UICONTROL Nombre humano] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona información sobre el nombre de una persona u otra entidad viva. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos con nombre humano](../../images/data-types/healthcare/human-name.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../healthcare/period.md) | Período de tiempo en el que el nombre está o estaba en uso. |
| [!UICONTROL Familia] | `family` | Cadena | La familia o el apellido. |
| [!UICONTROL Dado] | `given` | Matriz de cadenas | El nombre dado, incluido cualquier segundo nombre. |
| [!UICONTROL Prefijo] | `prefix` | Matriz de cadenas | Cualquier parte del nombre antes del nombre propio o de pila. |
| [!UICONTROL Sufijo] | `suffix` | Matriz de cadenas | Cualquier parte del nombre después de la familia o el apellido. |
| [!UICONTROL Texto] | `text` | Cadena | La representación de texto sin formato del nombre completo. |
| [!UICONTROL Usar] | `use` | Cadena | El uso del nombre. Los valores de esta propiedad deben ser iguales a uno o varios de los siguientes valores de enumeración conocidos. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
