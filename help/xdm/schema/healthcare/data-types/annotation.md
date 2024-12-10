---
title: Tipo de datos de anotación
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de anotación (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# [!UICONTROL Tipo de datos de anotación]

[!UICONTROL Anotación] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene un nodo de texto con atribución al autor. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de anotación](../../../images/healthcare/data-types/annotation.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Referencia de autor] | `authorReference` | [[!UICONTROL Referencia]](../data-types/reference.md) | Una referencia al autor. |
| [!UICONTROL Autor] | `authorString` | Cadena | Persona responsable de la anotación. |
| [!UICONTROL Texto] | `text` | Cadena | El contenido de la anotación. |
| [!UICONTROL Fecha] | `time` | Fecha/Hora | Cuando se realizó la anotación. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
