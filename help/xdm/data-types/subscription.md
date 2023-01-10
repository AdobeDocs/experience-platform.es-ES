---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;suscripción;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de suscripción
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de suscripción (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---

# [!UICONTROL Suscripción] tipo de datos

[!UICONTROL Suscripción] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los derechos de licencia a software, servicios o bienes que se utilizan en función del tiempo o el uso.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | Describe los detalles sobre el dispositivo vinculado a la suscripción. |
| `environment` | [[!UICONTROL Entorno]](./environment.md) | Contiene información sobre la situación circundante en la que se produjo la observación del evento, detallando específicamente información transitoria como las versiones de red o software. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Describe una persona individual. Esto también puede representar a una persona que actúa en varias funciones, como un cliente, un contacto o un propietario. |
| `SKU` | Cadena | La unidad de mantenimiento de existencias (SKU), identificador único de un producto. |
| `billingPeriod` | Cadena | La duración entre facturación. |
| `billingStartDate` | Fecha | La fecha en la que debe pagarse la primera factura. El formato de fecha (sin hora) debe seguir el [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) estándar. |
| `category` | Cadena | La categorización principal de nivel superior de este tipo de suscripción. |
| `chargeMethod` | Cadena | La forma en que se configura la facturación para cobrar al cliente. |
| `contractID` | Cadena | ID exclusivo del contrato que rige esta suscripción. |
| `country` | Cadena | El país en el que se basan las condiciones contractuales y de acuerdo de suscripción. |
| `endDate` | Fecha | La fecha en la que finaliza el término de suscripción actual. El formato de fecha (sin hora) debe seguir el [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) estándar. |
| `paymentMethod` | Cadena | El método de pago para pagos recurrentes. |
| `paymentStatus` | Cadena | La situación de pago de la cuenta. |
| `planName` | Cadena | El nombre legible para la suscripción. |
| `reason` | Cadena | La intención general que tiene el miembro para el uso de la suscripción. |
| `renew` | Cadena | La forma acordada de que la suscripción pueda continuar después de la fecha de finalización. |
| `revision` | Cadena | Identificación entre suscripciones del mismo nombre y jerarquía de categorías. |
| `startDate` | Fecha | La fecha en la que comienza la suscripción. El formato de fecha (sin hora) debe seguir el [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) estándar. |
| `status` | Cadena | El estado actual de la suscripción. |
| `subCategory` | Cadena | La subcategoría específica de la suscripción. |
| `term` | Número entero | El valor numérico del término de suscripción. |
| `termUnitOfTime` | Cadena | Unidad de tiempo para el período de término. |
| `topUp` | Cadena | Describe los términos acordados para saber cómo se recompran los aspectos consumibles de una suscripción durante un período de facturación. |
| `type` | Cadena | El alcance del derecho en relación con el número de personas cubiertas por la suscripción. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
