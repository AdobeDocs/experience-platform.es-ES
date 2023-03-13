---
title: Tipo de datos de impresiones
description: Este documento proporciona información general sobre el tipo de datos XDM Impresiones.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# [!UICONTROL Impresiones] tipo de datos

[!UICONTROL Impresiones] es un tipo de datos XDM estándar que describe una impresión de marketing, que es una métrica utilizada para cuantificar el número de vistas digitales o participaciones de un fragmento de contenido, como un anuncio, una publicación digital o una página web.

![](../images/data-types/impressions.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ID` | Cadena | Un ID único para la impresión. |
| `displays` | Número entero | El número de veces que el artículo de impresión se ha mostrado a un cliente. |
| `selected` | Número entero | El número de veces que se ha seleccionado o hecho clic en el elemento de impresión. |
| `type` | Cadena | El tipo de impresión. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
