---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;suscripción;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de suscripción
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de suscripción (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 28%

---

# [!UICONTROL Tipo de datos de suscripción]

[!UICONTROL Subscription] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los derechos con licencia para software, servicios o bienes que se utilizan en función del tiempo o el uso.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [[!UICONTROL Dispositivo]](./device.md) | Describe los detalles del dispositivo vinculado a la suscripción. |
| `environment` | [[!UICONTROL Entorno]](./environment.md) | Contiene información sobre el contexto en el que ocurrió la observación del evento, con información transitoria específica como la red o las versiones de software. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Describe a una persona individual. Esto también puede representar a una persona que tiene varias funciones, como cliente, contacto o propietario. |
| `SKU` | Cadena | El SKU (código de referencia), un identificador único de un producto. |
| `billingPeriod` | Cadena | La duración entre los períodos de facturación. |
| `billingStartDate` | Fecha | La fecha en la que vence la primera factura. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `category` | Cadena | La principal categorización de nivel superior de este tipo de suscripción. |
| `chargeMethod` | Cadena | La forma en que se configura la facturación para cobrar al cliente. |
| `contractID` | Cadena | El ID único del contrato de esta suscripción. |
| `country` | Cadena | El país en el que se basan los términos del contrato y del acuerdo de suscripción. |
| `endDate` | Fecha | La fecha en la que finaliza el plazo de suscripción actual. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Cadena | El método de pago para pagos recurrentes. |
| `paymentStatus` | Cadena | El estado de pago de la cuenta. |
| `planName` | Cadena | El nombre legible en lenguaje natural de la suscripción. |
| `reason` | Cadena | La intención general que tiene el miembro en cuanto al uso de la suscripción. |
| `renew` | Cadena | La forma acordada en que la suscripción puede continuar después de la fecha de finalización. |
| `revision` | Cadena | La identificación entre suscripciones del mismo nombre y jerarquía de categorías. |
| `startDate` | Fecha | La fecha de inicio de la suscripción. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Cadena | El estado actual de la suscripción. |
| `subCategory` | Cadena | La subcategorización específica de la suscripción. |
| `term` | Entero | El valor numérico del término de suscripción. |
| `termUnitOfTime` | Cadena | La unidad de tiempo del periodo. |
| `topUp` | Cadena | Describe los términos acordados sobre cómo se vuelven a comprar los aspectos consumibles de una suscripción durante un período de facturación. |
| `type` | Cadena | El ámbito del derecho en relación con la cantidad de personas incluidas en la suscripción. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
