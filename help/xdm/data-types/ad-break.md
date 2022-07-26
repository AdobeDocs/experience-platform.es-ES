---
title: Tipo de datos de desglose de anuncios
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de pausa publicitaria (XDM).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 6%

---

# [!UICONTROL Pausa publicitaria] tipo de datos

[!UICONTROL Pausa publicitaria] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe cómo se inserta un anuncio temporizado en un fragmento de medios temporizado.

![Estructura del tipo de datos](../images/data-types/ad-break.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_dc.title` | Cadena | Un nombre descriptivo para la pausa publicitaria. |
| `_id` | Cadena | Identificador único de la pausa publicitaria. |
| `offset` | Número entero | El desplazamiento, en segundos, de la pausa publicitaria desde el inicio del contenido principal. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
