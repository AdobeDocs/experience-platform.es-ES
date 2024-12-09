---
title: Tipo de datos del período
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de período (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# Tipo de datos [!UICONTROL Period]

[!UICONTROL Period] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona un período de tiempo definido por una fecha/hora de inicio y finalización. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de período](../../images/data-types/healthcare/period.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Fin] | `end` | Fecha/Hora | La fecha y hora de finalización. |
| [!UICONTROL Start] | `start` | Fecha/Hora | La fecha y hora de inicio. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
