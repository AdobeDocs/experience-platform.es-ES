---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;suscripción;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de suscripción
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de Suscripción (XDM).
translation-type: tm+mt
source-git-commit: 8ccf0a53f231c9f59cd87735126b180c6b678e51
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 9%

---


# [!UICONTROL Tipo ] de datos de suscripción

[!UICONTROL La ] suscripción es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los derechos de licencia para software, servicios o bienes que se utilizan en función del tiempo o el uso.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [[!UICONTROL Dispositivo]](./device.md) | Describe detalles sobre el dispositivo vinculado a la suscripción. |
| `environment` | [[!UICONTROL Entorno]](./environment.md) | Contiene información sobre la situación que rodea a la observación del evento, en concreto información transitoria como las versiones de red o software. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Describe una persona individual. Esto también puede representar a una persona que actúa en diferentes funciones, como cliente, contacto o propietario. |
| `SKU` | Cadena | La unidad de almacenamiento (SKU), un identificador único para un producto. |
| `billingPeriod` | Cadena | Duración entre facturación. |
| `billingStartDate` | Fecha | Fecha en la que debe pagarse la primera factura. El formato de fecha (sin tiempo) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `category` | Cadena | La clasificación principal de nivel superior de este tipo de suscripción. |
| `chargeMethod` | Cadena | La forma en que se configura la facturación para cargar al cliente. |
| `contractID` | Cadena | ID única del contrato que rige esta suscripción. |
| `country` | Cadena | El país en el que están enraizados los términos contractuales y de acuerdo de suscripción. |
| `endDate` | Fecha | Fecha en la que finaliza el término de suscripción actual. El formato de fecha (sin tiempo) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Cadena | El método de pago para pagos recurrentes. |
| `paymentStatus` | Cadena | La situación de pago de la cuenta. |
| `planName` | Cadena | El nombre legible en lenguaje natural de la suscripción. |
| `reason` | Cadena | La intención general que tiene el miembro para el uso de la suscripción. |
| `renew` | Cadena | La forma acordada en que la suscripción podrá continuar después de la fecha de finalización. |
| `revision` | Cadena | Identificación entre suscripciones del mismo nombre y jerarquía de categorías. |
| `startDate` | Fecha | Fecha en la que comienza la suscripción. El formato de fecha (sin tiempo) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Cadena | Estado actual de la suscripción. |
| `subCategory` | Cadena | Subcategoría específica de la suscripción. |
| `term` | Número entero | Valor numérico del término de suscripción. |
| `termUnitOfTime` | Cadena | Unidad de tiempo para el período de término. |
| `topUp` | Cadena | Describe los términos acordados para saber cómo se recompran los aspectos consumibles de una suscripción durante un período de facturación. |
| `type` | Cadena | El alcance de la asignación de derechos en relación con el número de personas cubiertas por la suscripción. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)