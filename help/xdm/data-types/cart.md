---
title: Tipo de datos del carrito
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia del carro de compras (XDM).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 5%

---

# [!UICONTROL Carrito] tipo de datos

[!UICONTROL Carrito] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona propiedades relacionadas con un carro de compras. Utiliza este tipo de datos para capturar el identificador único asignado por el vendedor (`Cart ID`) y el origen (`Cart Source`) donde se agregaron uno o más productos al carro de compras.

![Un diagrama de la [!UICONTROL Carrito] tipo de datos.](../images/data-types/cart.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID de carrito] | `cartID` | string | Identificador único asignado por el vendedor al carro de compras. |
| [!UICONTROL Origen del carrito] | `cartSource` | string | Donde se agregaron uno o más productos al carro de compras. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
