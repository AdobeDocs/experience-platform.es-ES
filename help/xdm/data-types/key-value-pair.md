---
title: Tipo de datos del par de valor clave
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de par de valores clave.
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 5%

---

# [!UICONTROL Par de valor clave] tipo de datos

[!UICONTROL Par de valor clave] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura los detalles de un par clave-valor genérico. Este tipo de datos se utiliza en [[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent] grupo de campos](../field-groups/event/analytics-full-extension.md) para describir los elementos de matriz de una variable de lista.

![Estructura del par de valores clave](../images/data-types/key-value-pair.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `key` | Cadena | Una clave (nombre) para una variable o valor genérico. |
| `value` | Cadena | El valor de la variable. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte [el repositorio XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
