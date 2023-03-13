---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;reservación;detalles de reservación;
title: Grupo de campos de esquema de detalles de reserva
description: Este documento proporciona información general del grupo de campos de esquema Detalles de la reserva.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---

# [!UICONTROL Detalles de reserva] grupo de campos de esquema

[!UICONTROL Detalles de reserva] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) se utiliza para recopilar información sobre una reserva, incluida la duración, la modificación, el estado reembolsable y el número de habitaciones.

El grupo de campos proporciona un único campo de tipo de objeto, `reservations`. Las propiedades contenidas en este objeto se explican a continuación.

![Estructura de detalles de reserva](../../images/field-groups/reservation-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `nonRefundableAmount` | [Moneda](../../data-types/currency.md) | El importe del precio de la reserva marcado como no reembolsable. |
| `transaction` | [Transacción](../../data-types/transaction.md) | Describe la transacción de moneda de la reserva. |
| `id` | Cadena | Un identificador único de la reserva. |
| `cancellation` | Número entero | Este valor se registra cuando se cancela una reserva. |
| `confirmationNumber` | Cadena | El número de confirmación o identificador de la reserva. |
| `created` | Número entero | Este valor se registra cuando se crea la reserva. |
| `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para realizar la compra. |
| `endDate` | DateTime | La fecha final de entrega, vuelta o salida de la reserva. |
| `length` | Número entero | Número total de días de la reserva. |
| `modification` | Número entero | Este valor se registra cuando se modifica una reserva. |
| `modificationDate` | DateTime | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Número entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Número entero | El número de niños asociados con la reserva. |
| `purpose` | Cadena | El propósito de la reserva, por lo general, ya sea comercial o personal. |
| `startDate` | DateTime | La fecha de inicio de recogida, salida o entrada de la reserva. |
| `triptype` | Cadena | Indica si la reserva es para un viaje de ida, de ida y vuelta o de varias ciudades. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Grupos de campos de reserva específicos del sector

Existen otros grupos de campos estándar que amplían el [!UICONTROL Detalles de reserva] para casos de uso específicos del sector. Consulte la siguiente documentación para obtener más detalles:

* [[!UICONTROL Reserva de restaurante]](./dining-reservation.md)
* [[!UICONTROL Reserva de vuelo]](./flight-reservation.md)
* [[!UICONTROL Reserva de alojamiento]](./lodging-reservation.md)
