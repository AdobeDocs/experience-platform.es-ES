---
title: Tipo de datos de relación
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de relación (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL Tipo de datos de proporción]

[!UICONTROL Ratio] es un tipo de datos XDM (Experience Data Model) estándar que proporciona una proporción de dos valores [[!UICONTROL Quantity]](../data-types/quantity.md) a través de un numerador y un denominador. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de proporción](../../../images/healthcare/data-types/ratio.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Denominador] | `denominator` | [[!UICONTROL Cantidad simple]](../data-types/simple-quantity.md) | El valor del denominador. |
| [!UICONTROL Numerador] | `numerator` | [[!UICONTROL Cantidad]](../data-types/quantity.md) | El valor del numerador. |

>[!NOTE]
>
> `denominator` y `numerator` tienen diferentes tipos de datos debido a la especificación creada según la versión 5 de FHIR de HL7.

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
