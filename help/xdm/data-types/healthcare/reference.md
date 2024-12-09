---
title: Tipo de datos de referencia
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de referencia (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---

# [!UICONTROL Referencia] tipo de datos

[!UICONTROL Referencia] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona una referencia de un recurso a otro. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de referencia](../../images/data-types/healthcare/reference.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Identificador] | `identifier` | [[!UICONTROL Identificador]](../healthcare/identifier.md) | La referencia lógica cuando no se conoce la referencia literal. |
| [!UICONTROL Pantalla] | `display` | Cadena | La alternativa textual para la referencia. |
| [!UICONTROL Referencia] | `reference` | Cadena | La referencia literal, relativa, interna o absoluta URL. |
| [!UICONTROL Tipo] | `type` | Cadena | El tipo al que hace referencia, representado como URI. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
