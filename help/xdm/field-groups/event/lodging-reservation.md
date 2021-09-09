---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;reserva;alojamiento;
title: Grupo de campos de esquema de reserva de alojamiento
description: Este documento proporciona una visión general del grupo de campos de esquema de reserva de alojamiento.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---


# [!UICONTROL Grupo de campos de esquema de ] reserva de alojamiento

[!UICONTROL Lodging ] Reservationes un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) cliente para capturar información relacionada con una reserva de alojamiento.

El grupo de campos es una extensión del grupo de campos [!UICONTROL Detalles de reserva] y contiene todos los mismos campos bajo un único campo de tipo de objeto, `reservations`. Además de estos campos genéricos, la [!UICONTROL reserva de alojamiento] también incluye la matriz `lodgingReservations`. Esta matriz de objetos se utiliza para describir una o más reservas con propiedades exclusivas del alojamiento.

>[!NOTE]
>
>Este documento cubre los detalles de la matriz `lodgingReservations`. Para obtener información sobre los demás campos proporcionados en el objeto `reservations`, consulte la referencia del grupo de campos [[!UICONTROL Detalles de reserva]](./reservation-details.md).

![Estructura de reservas de alojamiento](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` es una matriz de objetos que representa una lista de reservas de alojamiento. Si un evento de reserva implica reservas en varios hoteles diferentes a lo largo de la ruta de un viaje, por ejemplo, estas reservas se pueden listar como objetos individuales en `lodgingReservations` para un solo evento.

A continuación se proporciona la estructura de cada objeto proporcionada en `lodgingReservations`.

![estructura de las reservas](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Moneda]](../../data-types/currency.md) | Precio medio diario de la habitación del hotel. |
| `lodgingCheckIn` | Objeto | Un objeto que describe el alojamiento de los detalles del registro. Incluye los siguientes valores:<ul><li>`digitalKey`: (Número entero) Indica si un invitado selecciona el uso de una clave digital al registrarse.</li><li>`earlyCheckInRequested`: (Número entero) Indica si un invitado solicita la protección antes de las horas normales de registro.</li><li>`lateCheckInRequested`: (Número entero) Indica si un invitado solicita registrar en horas posteriores a las horas normales de registro.</li><li>`noRoomCheckIn`: (Total) Este valor se captura cuando un invitado termina de registrarse cuando no hay salas disponibles en ese momento.</li><li>`oneRoomCheckIn`: (Total) Este valor se captura cuando un invitado termina de registrarse cuando solo hay una habitación disponible en ese momento.</li><li>`roomKeys`: (Número entero) El número de llaves estándar de la habitación que se proporcionan durante el registro de entrada.</li><li>`userSelectedRoom`: (Booleano) Indica si el invitado seleccionó su habitación en el momento de la facturación.</li></ul> |
| `rackrate` | [[!UICONTROL Moneda]](../../data-types/currency.md) | El coste de una reserva en el mismo día sin reserva previa. |
| `ID` | Cadena | El número o identificador de reserva. |
| `agentID` | Cadena | El ID del agente asociado con la reserva de hotel. |
| `basePrice` | Cadena | El precio base antes de añadir cualquier descuento. |
| `bookingID` | Cadena | El ID de reserva asociado a la reserva de hotel. |
| `cancellation` | Número entero | Este valor se captura cuando se cancela una reserva. |
| `checkInDate` | DateTime | La fecha de registro de la reserva de la habitación. |
| `checkOutDate` | DateTime | La fecha de salida de la reserva de la habitación. |
| `confirmationNumber` | Cadena | El número o identificador de confirmación de la reserva. |
| `couponCode` | Cadena | Un código de cupón asociado a la reserva de hotel. |
| `created` | Número entero | Este valor se captura cuando se crea una reserva. |
| `currencyCode` | Cadena | El código de moneda ISO 4217 utilizado para realizar la compra. |
| `discountPercent` | Duplicada | El porcentaje de descuento asociado con la reserva. |
| `freeCancelation` | Booleano | Indica si la habitación tiene una política de cancelación gratuita. |
| `guestID` | Cadena | El ID de invitado asociado con la reserva de hotel. |
| `length` | Número entero | Número total de días para la reserva. |
| `loyaltyID` | Cadena | El ID del programa de fidelidad para el invitado indicado en la reserva. |
| `modification` | Número entero | Este valor se captura cuando se modifica una reserva. |
| `modificationDate` | DateTime | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Número entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Número entero | Número de niños asociados a la reserva. |
| `numberOfRooms` | Número entero | Número de habitaciones asociadas a la reserva. |
| `propertyID` | Cadena | Un identificador del hotel o resort para la reserva. |
| `propertyName` | Cadena | Nombre del hotel o complejo para la reserva. |
| `purpose` | Cadena | El propósito de la reserva, generalmente de negocios o personal. |
| `ratePlan` | Cadena | El precio de venta de la habitación. |
| `refundable` | Booleano | Indica si la habitación es reembolsable. |
| `reservationStatus` | Cadena | El estado de la reserva. |
| `roomAccessibilityType` | Cadena | El tipo de accesibilidad de la habitación, como movilidad, audición u otros. |
| `roomCapacity` | Número entero | El número de personas que alberga la habitación del hotel. |
| `roomType` | Cadena | El tipo de habitación reservada. |
| `smoking` | Booleano | Indica si la habitación permite fumar. |
| `tripType` | Cadena | Indica si la reserva es para un viaje de ida, de ida y vuelta o de varias ciudades. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
