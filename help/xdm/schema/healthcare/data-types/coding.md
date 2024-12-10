---
title: Tipo de datos de codificación
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de codificación (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---

# [!UICONTROL Codificación] tipo de datos

[!UICONTROL Codificación] es un tipo de datos XDM (Experience Data Model) estándar que describe una referencia a un código definido por un sistema terminológico. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de codificación](../../../images/healthcare/data-types/coding.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | Cadena | El símbolo en la sintaxis definida por el sistema. |
| [!UICONTROL Pantalla] | `display` | Cadena | La representación definida por el sistema. |
| [!UICONTROL Sistema] | `system` | Cadena | El área de nombres del valor del identificador, representado como URI. |
| [!UICONTROL  Lo Ha Seleccionado El Usuario] | `userSelected` | Booleano | Un indicador de si el usuario eligió esta codificación. El valor predeterminado es false. |
| [!UICONTROL Versión] | `version` | Cadena | La versión del sistema. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
