---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;esquemas;telecomunicaciones;suscripción;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de suscripción a telecomunicaciones
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de suscripción a telecomunicaciones (XDM).
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 10%

---

# [!UICONTROL Tipo de datos de ] suscripción de telecomunicaciones

[!UICONTROL La ] suscripción de telecomunicaciones es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles de tipos de suscripción de telecomunicaciones específicos, como Internet, dispositivos móviles, medios o líneas fijas.

>[!NOTE]
>
>Este documento describe el tipo de datos. Para el grupo de campos del mismo nombre, consulte la guía de referencia del grupo de campos [[!UICONTROL Telecom Subscription].](../field-groups/profile/telecom-subscription.md)
>
>Si está describiendo un tipo de suscripción que no está relacionado con el sector de las telecomunicaciones, utilice el tipo de datos genérico [[!UICONTROL Subscription]](./subscription.md) en su lugar.

![Estructura de suscripción de telecomunicaciones](../images/data-types/telecom-subscription/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `devices` | Matriz de objetos | Describe una lista de dispositivos y/o accesorios asociados con el plan. Consulte la sección [a continuación](#devices) para obtener más información sobre la estructura esperada de cada elemento de matriz. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Describe el propietario de la suscripción. |
| `ID` | Cadena | Identificador único de la instancia de suscripción. |
| `billingPeriod` | Cadena | La duración entre facturación. |
| `billingStartDate` | Fecha  | La fecha en la que comienza el periodo de facturación. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `chargeMethod` | Cadena | La forma en que se configura la facturación para cobrar al cliente. |
| `contractID` | Cadena | ID exclusivo del contrato que rige esta suscripción. |
| `country` | Cadena | El país en el que se basan las condiciones contractuales y de acuerdo de suscripción. |
| `endDate` | Fecha  | La fecha en la que finaliza el término de suscripción actual. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentDueDate` | Fecha  | La fecha en la que se debe el pago de la suscripción. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Cadena | El método de pago para pagos recurrentes. |
| `paymentStatus` | Cadena | La situación de pago de la cuenta. |
| `planName` | Cadena | El nombre legible para la suscripción. |
| `reason` | Cadena | La intención general que tiene el miembro para el uso de la suscripción. |
| `renew` | Cadena | La forma acordada de que la suscripción pueda continuar después de la fecha de finalización. |
| `startDate` | Fecha  | La fecha en la que comienza la suscripción. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Cadena | El estado actual de la suscripción. |
| `subscriptionCategory` | Cadena | La categorización principal de nivel superior de este tipo de suscripción. |
| `subscriptionSKU` | Cadena | La unidad de mantenimiento de existencias (SKU) para la suscripción. |
| `subscriptionSubCategory` | Cadena | La subcategoría específica de la suscripción. |
| `term` | Número entero | El valor numérico del término de suscripción. |
| `termUnitOfTime` | Cadena | Unidad de tiempo para el período de término. |
| `topUp` | Cadena | Describe los términos acordados para saber cómo se recompran los aspectos consumibles de una suscripción durante un período de facturación. |
| `type` | Cadena | El alcance del derecho en relación con el número de personas cubiertas por la suscripción. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` es una matriz de objetos, cada uno de los cuales describe un dispositivo o accesorio asociado a la suscripción.

![Estructura de la matriz de dispositivos](../images/data-types/telecom-subscription/devices.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `deviceFees` | Objeto | Un objeto que captura cualquier tarifa de dispositivo para elementos como enrutadores, módems y receptores. Espera las siguientes propiedades:<ul><li>`amount`: El importe monetario representado por el  `currencyCode`.</li><li>`conversionDate`: La fecha en la que se realizó la conversión de moneda.</li><li>`currencyCode`: El código de moneda  [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) para  `amount`.</li></ul> |
| `ID` | Cadena | Un ID exclusivo para el dispositivo. |
| `OS` | Cadena | El sistema operativo del dispositivo. |
| `deviceInsurance` | Cadena | Indica si un cliente ha elegido un seguro para este dispositivo. |
| `manufacturer` | Cadena | El fabricante del dispositivo. |
| `name` | Cadena | Un nombre para el dispositivo. |
| `paymentOptions` | Cadena | Indica si el dispositivo se pagará en cuotas o a precios de venta al por menor completos. |
| `serialNumber` | Cadena | El número de serie del dispositivo. |
| `status` | Cadena | El estado del dispositivo. |
| `storageCapacity` | Cadena | La capacidad de almacenamiento del dispositivo. |
| `type` | Cadena | El tipo de dispositivo. |

{style=&quot;table-layout:auto&quot;}