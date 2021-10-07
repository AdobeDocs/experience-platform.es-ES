---
title: Tipo de datos de impresiones
description: Este documento proporciona información general sobre el tipo de datos XDM de Impresiones.
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

#  Tipo de datos de impresiones

 Las impresiones son un tipo de datos XDM estándar que describe una impresión de marketing, que es una métrica utilizada para cuantificar el número de vistas o participaciones digitales para un fragmento de contenido, como publicidad, publicación digital o página web.

![](../images/data-types/impressions.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ID` | Cadena | Un ID único para la impresión. |
| `displays` | Número entero | Número de veces que el elemento de impresión se ha mostrado a un cliente. |
| `selected` | Número entero | Número de veces que se ha seleccionado o hecho clic en el elemento de impresión. |
| `type` | Cadena | El tipo de impresión. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
