---
title: Tipo de datos de dinero
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia monetaria (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# Tipo de datos [!UICONTROL Dinero]

[!UICONTROL Dinero] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona una gran utilidad económica en cualquier moneda reconocida. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos monetarios](../../../images/healthcare/data-types/money.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Moneda] | `currency` | Cadena | El código de divisa en formato ISO 4217. |
| [!UICONTROL Valor] | `value` | Duplicada | El valor numérico. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
