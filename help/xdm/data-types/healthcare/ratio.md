---
title: Tipo de datos de relación
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de relación (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL Tipo de datos de proporción]

[!UICONTROL Ratio] es un tipo de datos XDM (Experience Data Model) estándar que proporciona una proporción de dos valores [[!UICONTROL Quantity]](../healthcare/quantity.md) a través de un numerador y un denominador. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de proporción](../../images/data-types/healthcare/ratio.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Denominador] | `denominator` | [[!UICONTROL Cantidad simple]](../healthcare/simple-quantity.md) | El valor del denominador. |
| [!UICONTROL Numerador] | `numerator` | [[!UICONTROL Cantidad]](../healthcare/quantity.md) | El valor del numerador. |

>[!NOTE]
>
> `denominator` y `numerator` tienen diferentes tipos de datos debido a la especificación creada según la versión 5 de FHIR de HL7.

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
