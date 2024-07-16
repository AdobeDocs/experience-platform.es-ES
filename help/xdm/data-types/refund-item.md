---
title: Tipo de datos de artículo de reembolso
description: Obtenga información sobre el tipo de datos Modelo de datos de experiencia (XDM) de artículo de reembolso.
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL Tipo de datos del elemento de reembolso]

[!UICONTROL Artículo de reembolso] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe la información de captura relacionada con un reembolso asociado con un pedido.

![Diagrama del tipo de datos de elemento de reembolso.](../images/data-types/refund-item.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID de transacción] | `transactionID` | cadena | El identificador único de la transacción de este artículo de devolución. |
| [!UICONTROL Importe de reembolso] | `refundAmount` | número | El valor del reembolso. |
| [!UICONTROL Motivo del reembolso] | `refundReason` | cadena | El motivo por el que se emitió un reembolso. |
| [!UICONTROL Tipo de pago de reembolso] | `refundPaymentType` | cadena | El método de pago de este pedido. Se permiten valores personalizados. |
| [!UICONTROL Código de divisa] | `currencyCode` | cadena | El código de divisa en formato ISO 4217 usado para este artículo de reembolso. Por ejemplo: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
