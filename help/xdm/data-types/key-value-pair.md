---
title: Tipo de datos del par de valores clave
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de pares de valores clave (XDM).
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 5%

---

# [!UICONTROL Par de valores clave] tipo de datos

[!UICONTROL Par de valores clave] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura los detalles de un par de clave-valor genérico. Este tipo de datos se utiliza en la variable [[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent] grupo de campos](../field-groups/event/analytics-full-extension.md) para describir los elementos de matriz de una variable de lista.

![Estructura del par de valores clave](../images/data-types/key-value-pair.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `key` | Cadena | Una clave (nombre) para una variable o valor genérico. |
| `value` | Cadena | El valor de la variable . |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte [el repositorio XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
