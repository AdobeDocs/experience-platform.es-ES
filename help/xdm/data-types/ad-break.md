---
title: Tipo de datos del desglose de anuncios
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de la pausa publicitaria.
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 6%

---

# [!UICONTROL Pausa para anuncios] tipo de datos

[!UICONTROL Pausa para anuncios] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe cómo se inserta un anuncio cronometrado en un medio cronometrado.

![Estructura de tipo de datos](../images/data-types/ad-break.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_dc.title` | Cadena | Un nombre descriptivo para la pausa publicitaria. |
| `_id` | Cadena | Un identificador único de la pausa publicitaria. |
| `offset` | Número entero | La diferencia en segundos de la pausa publicitaria desde el inicio del contenido principal. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
