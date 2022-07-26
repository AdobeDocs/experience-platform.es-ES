---
title: Tipo de datos de detalles de implementación
description: Este documento proporciona información general sobre los detalles de implementación del tipo de datos del Modelo de datos de experiencia (XDM).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# [!UICONTROL Detalles de implementación] tipo de datos

[!UICONTROL Detalles de implementación] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe una implementación de tecnología, como una API o un SDK.

![Estructura del tipo de datos](../images/data-types/implementation-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `environment` | Cadena | El entorno de la implementación. |
| `name` | Cadena | Identificador del SDK o del extremo. Todos los SDK o extremos se identifican mediante un URI, incluidas las extensiones. |
| `version` | Cadena | Versión de la API o el SDK. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
