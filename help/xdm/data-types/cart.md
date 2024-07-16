---
title: Tipo de datos del carrito
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia del carro de compras (XDM).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 14%

---

# Tipo de datos [!UICONTROL Carro]

El [!UICONTROL carro] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona propiedades relacionadas con un carro de compras. Utilice este tipo de datos para capturar el identificador único asignado por el vendedor (`Cart ID`) y el origen (`Cart Source`) donde se agregaron uno o más productos al carro de compras.

![Un diagrama del tipo de datos [!UICONTROL Carro].](../images/data-types/cart.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID de carrito] | `cartID` | cadena | Identificador único asignado por el vendedor al carrito de compras. |
| [!UICONTROL Carro de compras Source] | `cartSource` | cadena | Donde se agregaron uno o más productos al carro de compras. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
