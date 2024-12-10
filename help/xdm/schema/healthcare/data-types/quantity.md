---
title: Tipo de datos de cantidad
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de cantidad (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 11%

---

# [!UICONTROL Cantidad] tipo de datos

[!UICONTROL Cantidad] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona una cantidad medida o medible. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de cantidad](../../../images/healthcare/data-types/quantity.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | Cadena | La forma codificada de la unidad. |
| [!UICONTROL Comparador] | `comparator` | Cadena | El operador de comparación. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL Sistema] | `system` | Cadena | Sistema que define la forma de unidad codificada, representada como URI. |
| [!UICONTROL Unidad] | `unit` | Cadena | La representación de la unidad. |
| [!UICONTROL Valor] | `value` | Duplicada | El valor numérico. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
