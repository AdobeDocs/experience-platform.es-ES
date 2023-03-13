---
title: Tipo de datos de detalles de implementación
description: Este documento proporciona información general sobre los detalles de implementación del tipo de datos del Modelo de datos de experiencia (XDM).
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# [!UICONTROL Detalles de implementación] tipo de datos

[!UICONTROL Detalles de implementación] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe una implementación de tecnología, como una API o un SDK.

![Estructura de tipo de datos](../images/data-types/implementation-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `environment` | Cadena | El entorno de la implementación. |
| `name` | Cadena | El identificador del SDK o extremo. Todos los SDK o extremos se identifican mediante un URI, incluidas las extensiones. |
| `version` | Cadena | Versión de la API o del SDK. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
