---
title: Tipo de datos de cantidad simple
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de cantidad simple (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---

# [!UICONTROL Cantidad simple] tipo de datos

[!UICONTROL Cantidad simple] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona una cantidad medida o medible. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de cantidad simple](../../../images/healthcare/data-types/simple-quantity.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | Cadena | La forma codificada de la unidad. |
| [!UICONTROL Sistema] | `system` | Cadena | Sistema que define la forma de unidad codificada, representada como URI. |
| [!UICONTROL Unidad] | `unit` | Cadena | La representación de la unidad. |
| [!UICONTROL Valor] | `value` | Duplicada | El valor numérico. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
