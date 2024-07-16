---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;campos;esquemas;esquemas;telecomunicaciones;suscripción;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de suscripción de telecomunicaciones
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de suscripción de telecomunicaciones (XDM).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 20%

---

# [!UICONTROL Suscripción de telecomunicaciones] tipo de datos

[!UICONTROL Suscripción de telecomunicaciones] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles para tipos de suscripción de telecomunicaciones específicos, como Internet, móvil, medios o teléfono fijo.

>[!NOTE]
>
>Este documento describe el tipo de datos. Para el grupo de campos del mismo nombre, consulte la [[!UICONTROL Guía de referencia del grupo de campos Suscripción a telecomunicaciones]](../field-groups/profile/telecom-subscription.md).
>
>Si está describiendo un tipo de suscripción que no está relacionado con el sector de las telecomunicaciones, use el tipo de datos genérico [[!UICONTROL Subscription]](./subscription.md) en su lugar.

![Estructura de suscripción de telecomunicaciones](../images/data-types/telecom-subscription/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `devices` | Matriz de objetos | Describe una lista de dispositivos y/o accesorios asociados con el plan. Consulte la sección [debajo de](#devices) para obtener detalles sobre la estructura esperada de cada elemento de matriz. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Describe el propietario de la suscripción. |
| `ID` | Cadena | Un identificador único de la instancia de suscripción. |
| `billingPeriod` | Cadena | La duración entre los períodos de facturación. |
| `billingStartDate` | Fecha | La fecha en la que comienza el período de facturación. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `chargeMethod` | Cadena | La forma en que se configura la facturación para cobrar al cliente. |
| `contractID` | Cadena | El ID único del contrato de esta suscripción. |
| `country` | Cadena | El país en el que se basan los términos del contrato y del acuerdo de suscripción. |
| `endDate` | Fecha | La fecha en la que finaliza el plazo de suscripción actual. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentDueDate` | Fecha | La fecha de vencimiento del pago de la suscripción. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Cadena | El método de pago para pagos recurrentes. |
| `paymentStatus` | Cadena | El estado de pago de la cuenta. |
| `planName` | Cadena | El nombre legible en lenguaje natural de la suscripción. |
| `reason` | Cadena | La intención general que tiene el miembro en cuanto al uso de la suscripción. |
| `renew` | Cadena | La forma acordada en que la suscripción puede continuar después de la fecha de finalización. |
| `startDate` | Fecha | La fecha de inicio de la suscripción. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Cadena | El estado actual de la suscripción. |
| `subscriptionCategory` | Cadena | La principal categorización de nivel superior de este tipo de suscripción. |
| `subscriptionSKU` | Cadena | El SKU (código de referencia) de la suscripción. |
| `subscriptionSubCategory` | Cadena | La subcategorización específica de la suscripción. |
| `term` | Entero | El valor numérico del término de suscripción. |
| `termUnitOfTime` | Cadena | La unidad de tiempo del periodo. |
| `topUp` | Cadena | Describe los términos acordados sobre cómo se vuelven a comprar los aspectos consumibles de una suscripción durante un período de facturación. |
| `type` | Cadena | El ámbito del derecho en relación con la cantidad de personas incluidas en la suscripción. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` es una matriz de objetos, cada uno de los cuales describe un dispositivo o accesorio asociado a la suscripción.

![Estructura de la matriz de dispositivos](../images/data-types/telecom-subscription/devices.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `deviceFees` | Objeto | Un objeto que registra cualquier tarifa de dispositivo para elementos como enrutadores, módems y receptores. Espera las siguientes propiedades:<ul><li>`amount`: El importe monetario representado por `currencyCode`.</li><li>`conversionDate`: la fecha en la que se realizó la conversión de moneda.</li><li>`currencyCode`: el [código de divisa en formato ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) para `amount`.</li></ul> |
| `ID` | Cadena | Un ID único para el dispositivo. |
| `OS` | Cadena | El sistema operativo del dispositivo. |
| `deviceInsurance` | Cadena | Indica si un cliente ha contratado un seguro para este dispositivo. |
| `manufacturer` | Cadena | El fabricante del dispositivo. |
| `name` | Cadena | Nombre del dispositivo. |
| `paymentOptions` | Cadena | Indica si el dispositivo se pagará en cuotas o al precio total al contado. |
| `serialNumber` | Cadena | El número de serie del dispositivo. |
| `status` | Cadena | El estado del dispositivo. |
| `storageCapacity` | Cadena | La capacidad de almacenamiento del dispositivo. |
| `type` | Cadena | El tipo de dispositivo. |

{style="table-layout:auto"}
