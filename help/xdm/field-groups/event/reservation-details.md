---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;reserva;detalles de reserva;
title: Grupo de campos de esquema Detalles de reserva
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de reserva .
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 5%

---


# [!UICONTROL Grupo de campos ] Detalle de la reserva

[!UICONTROL Reserva ] Detalle es un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) cliente para capturar información sobre una reserva, incluyendo longitud, modificación, estado reembolsable y número de habitaciones.

El grupo de campos proporciona un único campo de tipo de objeto, `reservations`. Las propiedades contenidas en este objeto se explican a continuación.

![Estructura de los detalles de la reserva](../../images/field-groups/reservation-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `nonRefundableAmount` | [Moneda](../../data-types/currency.md) | El importe del precio de reserva marcado como no reembolsable. |
| `transaction` | [Transacción](../../data-types/transaction.md) | Describe la transacción de moneda para la reserva. |
| `id` | Cadena | Identificador único de la reserva. |
| `cancellation` | Número entero | Este valor se captura cuando se cancela una reserva. |
| `confirmationNumber` | Cadena | El número o identificador de confirmación de la reserva. |
| `created` | Número entero | Este valor se captura cuando se creó la reserva. |
| `currencyCode` | Cadena | El código de moneda ISO 4217 utilizado para realizar la compra. |
| `endDate` | DateTime | Fecha final de la reserva, devolución o salida. |
| `length` | Número entero | Número total de días para la reserva. |
| `modification` | Número entero | Este valor se captura cuando se modifica una reserva. |
| `modificationDate` | DateTime | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Número entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Número entero | Número de niños asociados a la reserva. |
| `purpose` | Cadena | El propósito de la reserva, generalmente de negocios o personal. |
| `startDate` | DateTime | La fecha de inicio de la recogida, salida o registro de la reserva. |
| `triptype` | Cadena | Indica si la reserva es para un viaje de ida, de ida y vuelta o de varias ciudades. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Grupos de campos de reserva específicos del sector

Existen otros grupos de campos estándar que amplían el esquema [!UICONTROL Detalles de reserva] para casos de uso específicos del sector. Consulte la siguiente documentación para obtener más información:

* [[!UICONTROL Reserva de comedor]](./dining-reservation.md)
* [[!UICONTROL Reserva de vuelo]](./flight-reservation.md)
* [[!UICONTROL Reserva de alojamiento]](./lodging-reservation.md)