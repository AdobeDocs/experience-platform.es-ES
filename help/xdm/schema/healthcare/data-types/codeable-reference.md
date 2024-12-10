---
title: Tipo de datos de referencia codificable
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de referencia codificable (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL Tipo de datos de referencia codificable]

[!UICONTROL Referencia codificable] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe una referencia a un recurso o a un concepto. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de referencia codificable](../../../images/healthcare/data-types/codeable-reference.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Concepto] | `concept` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Una referencia a un concepto (por clase). |
| [!UICONTROL Referencia] | `reference` | [[!UICONTROL Referencia]](../data-types/reference.md) | Una referencia a un recurso. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
