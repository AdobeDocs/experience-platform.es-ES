---
title: Tipo de datos de envío
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia de envío (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---

# [!UICONTROL Envío] tipo de datos

[!UICONTROL Envío] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona detalles relacionados con el envío de uno o más productos. Incluye detalles sobre la logística y detalles específicos sobre la entrega de los artículos pedidos.


![Un diagrama de la [!UICONTROL Envío] tipo de datos.](../images/data-types/shipping.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Método de envío] | `shippingMethod` | string | El método de envío elegido por el cliente. |
| [!UICONTROL Importe de envío] | `shippingAmount` | number | El importe que el cliente tuvo que pagar por el envío. |
| [!UICONTROL Código de divisa] | `currencyCode` | string | El código alfabético de la divisa en formato ISO 4217 usado para poner el precio al producto. |
| [!UICONTROL Destino de envío] | `shippingDestination` | string | El destino de envío especificado por el usuario (por ejemplo, casa, tienda, etc.). |
| [!UICONTROL Fecha de envío] | `shipDate` | string | La fecha en la que se envían uno o más artículos de un pedido. |
| [!UICONTROL Dirección de envío] | `address` | [[!UICONTROL dirección]](./address.md) | La dirección de envío. |
| [!UICONTROL Número de seguimiento] | `trackingNumber` | number | El número de seguimiento proporcionado por el transportista. |
| [!UICONTROL URL de seguimiento] | `trackingURL` | string | Dirección URL para realizar un seguimiento del estado de envío de un artículo de pedido. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
