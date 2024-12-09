---
title: Tipo de datos de identificador
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de identificador (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL Identificador] tipo de datos

[!UICONTROL Identificador] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona un identificador pensado para el cálculo. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de identificador](../../images/data-types/healthcare/identifier.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../healthcare/period.md) | Período de tiempo en el que el ID es o era válido para su uso. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | La descripción del identificador. |
| [!UICONTROL Asignador] | `assigner` | Cadena | La organización que emitió el ID. |
| [!UICONTROL Sistema] | `system` | Cadena | El área de nombres del valor del identificador, representado como URI. |
| [!UICONTROL Usar] | `use` | Cadena | El uso del identificador. Los valores de esta propiedad deben ser iguales a uno o varios de los siguientes valores de enumeración conocidos. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Valor] | `value` | Cadena | El valor único del ID. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
