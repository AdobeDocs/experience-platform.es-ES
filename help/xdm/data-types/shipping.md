---
title: Tipo de datos de envío
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia de envío (XDM).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 18%

---

# [!UICONTROL Envío] tipo de datos

[!UICONTROL Envío] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona detalles relacionados con el envío de uno o más productos. Incluye detalles sobre la logística y detalles específicos sobre la entrega de los artículos pedidos.


![Un diagrama del tipo de datos [!UICONTROL Envío].](../images/data-types/shipping.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Método de envío] | `shippingMethod` | cadena | El método de envío elegido por el cliente. |
| [!UICONTROL Importe de envío] | `shippingAmount` | número | El importe que el cliente tuvo que pagar por el envío. |
| [!UICONTROL Código de divisa] | `currencyCode` | cadena | El código alfabético de la divisa en formato ISO 4217 usado para poner el precio al producto. |
| [!UICONTROL Destino de envío] | `shippingDestination` | cadena | El destino de envío especificado por el usuario (por ejemplo, casa, tienda, etc.). |
| [!UICONTROL Fecha de envío] | `shipDate` | cadena | La fecha en la que se envían uno o más artículos de un pedido. |
| [!UICONTROL Dirección de envío] | `address` | [[!UICONTROL dirección]](./address.md) | La dirección de envío. |
| [!UICONTROL Número de seguimiento] | `trackingNumber` | número | El número de seguimiento proporcionado por el transportista. |
| [!UICONTROL URL de seguimiento] | `trackingURL` | cadena | Dirección URL para realizar un seguimiento del estado de envío de un artículo de pedido. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
