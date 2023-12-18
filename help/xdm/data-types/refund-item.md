---
title: Tipo de datos de artículo de reembolso
description: Obtenga información sobre el tipo de datos Modelo de datos de experiencia (XDM) de artículo de reembolso.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL Elemento de reembolso] tipo de datos

[!UICONTROL Elemento de reembolso] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe captura información relacionada con un reembolso asociado con un pedido.

![Diagrama del tipo de datos de artículo de reembolso.](../images/data-types/refund-item.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID de transacción] | `transactionID` | string | El identificador único de la transacción de este artículo de devolución. |
| [!UICONTROL Importe de reembolso] | `refundAmount` | number | El valor del reembolso. |
| [!UICONTROL Motivo del reembolso] | `refundReason` | string | El motivo por el que se emitió un reembolso. |
| [!UICONTROL Tipo de pago de reembolso] | `refundPaymentType` | string | El método de pago de este pedido. Se permiten valores personalizados. |
| [!UICONTROL Código de divisa] | `currencyCode` | string | El código de divisa en formato ISO 4217 usado para este artículo de reembolso. Por ejemplo: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
