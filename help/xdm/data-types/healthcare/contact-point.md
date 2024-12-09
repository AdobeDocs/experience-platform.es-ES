---
title: Tipo de datos del punto de contacto
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) del punto de contacto.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# [!UICONTROL Tipo de datos del punto de contacto]

[!UICONTROL Punto de contacto] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de contacto de una persona. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura del tipo de datos del punto de contacto](../../images/data-types/healthcare/contact-point.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../healthcare/period.md) | Período de tiempo en el que el punto de contacto estaba/está en uso. |
| [!UICONTROL Rango] | `rank` | Entero | La clasificación que indica el uso preferido del punto de contacto. El valor mínimo es `1` y el valor máximo es `2147483647`, donde `1` es la especificidad más alta. |
| [!UICONTROL Sistema] | `system` | Cadena | El sistema a través del cual se puede contactar con ellos. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Usar] | `use` | Cadena | El propósito del punto de contacto. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Valor] | `value` | Cadena | Los detalles del punto de contacto. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
