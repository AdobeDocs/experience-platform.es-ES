---
title: Tipo de datos del intervalo
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de rango (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 66f8b574-04d9-435f-8743-4ff89c4c0079
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# [!UICONTROL Tipo de datos del rango]

[!UICONTROL Range] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona un conjunto de valores enlazados por valores bajos y altos. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de rango](../../../images/healthcare/data-types/range.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Alta] | `high` | [[!UICONTROL Cantidad simple]](../data-types/simple-quantity.md) | El límite más alto. |
| [!UICONTROL Baja] | `low` | [[!UICONTROL Cantidad simple]](../data-types/simple-quantity.md) | El límite más bajo. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
