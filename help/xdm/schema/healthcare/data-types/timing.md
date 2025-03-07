---
title: Tipo de datos de temporización
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de tiempo (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Tipo de datos de temporización]

[!UICONTROL Intervalo] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe una programación de tiempo que proporciona información sobre un evento que puede ocurrir varias veces. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de tiempo](../../../images/healthcare/data-types/timing.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Evento] | `event` | Matriz de DateTime | Cuando se produce el evento. |
| [!UICONTROL Repetir] | `repeat` | [[!UICONTROL Repetir]](../data-types/repeat.md) | Información sobre cuándo se produce el evento. |
| [!UICONTROL Código] | `code` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código relacionado con el evento. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
