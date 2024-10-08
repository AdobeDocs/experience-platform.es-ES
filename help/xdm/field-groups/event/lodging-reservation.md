---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;reservación;hospedaje;
title: Grupo de campos de esquema de reserva de alojamiento
description: Obtenga información acerca del grupo de campos Esquema de reserva de alojamiento.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 7%

---

# [!UICONTROL Reserva de alojamiento] grupo de campos de esquema

[!UICONTROL Reserva de alojamiento] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) que se usa para recopilar información sobre una reserva de alojamiento.

El grupo de campos es una extensión del grupo de campos [!UICONTROL Detalles de la reserva] y contiene todos los campos iguales en un único campo de tipo de objeto, `reservations`. Además de estos campos genéricos, [!UICONTROL Reserva de alojamiento] también incluye la matriz `lodgingReservations`. Esta matriz de objetos se utiliza para describir una o más reservas con propiedades únicas para el alojamiento.

>[!NOTE]
>
>Este documento cubre los detalles de la matriz `lodgingReservations`. Para obtener información sobre los demás campos proporcionados en el objeto `reservations`, consulte la [[!UICONTROL Referencia del grupo de campos Detalles de la reserva]](./reservation-details.md).

![Estructura de reserva de alojamiento](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` es una matriz de objetos que representa una lista de reservas de alojamiento. Si un evento de reserva implica reservas en varios hoteles diferentes a lo largo de la ruta de un viaje, por ejemplo, estas reservas pueden enumerarse como objetos individuales en `lodgingReservations` para un solo evento.

A continuación se proporciona la estructura de cada objeto proporcionado en `lodgingReservations`.

![estructura de reservas de alojamiento](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Moneda]](../../data-types/currency.md) | El precio medio diario de la habitación del hotel. |
| `lodgingCheckIn` | Objeto | Un objeto que describe los detalles del registro de alojamiento. Incluye los siguientes valores:<ul><li>`digitalKey`: (entero) indica cuándo un invitado selecciona el uso de una clave digital al registrarse.</li><li>`earlyCheckInRequested`: (entero) indica cuándo un invitado solicita registrarse antes de las horas de llegada normales.</li><li>`lateCheckInRequested`: (entero) indica cuándo un invitado solicita registrarse más tarde de las horas de llegada normales.</li><li>`noRoomCheckIn`: (entero) este valor se captura cuando un invitado termina de registrarse cuando no hay habitaciones disponibles en ese momento.</li><li>`oneRoomCheckIn`: (entero) este valor se captura cuando un invitado termina de registrarse cuando solo hay una habitación disponible en ese momento.</li><li>`roomKeys`: (Número entero) El número de llaves de habitación estándar proporcionadas al registrarse a la llegada.</li><li>`userSelectedRoom`: (booleano) indica si el huésped seleccionó su habitación en el momento de llegada.</li></ul> |
| `rackrate` | [[!UICONTROL Moneda]](../../data-types/currency.md) | El coste de una reserva para el mismo día sin reserva previa. |
| `ID` | Cadena | El número o identificador de la reserva. |
| `agentID` | Cadena | El ID de agente asociado con la reserva de hotel. |
| `basePrice` | Cadena | El precio base antes de aplicar descuentos. |
| `bookingID` | Cadena | El ID de reserva asociado con la reserva de hotel. |
| `cancellation` | Entero | Este valor se registra cuando se cancela una reserva. |
| `checkInDate` | Fecha/Hora | La fecha de registro de la reserva de habitación. |
| `checkOutDate` | Fecha/Hora | La fecha de salida de la reserva de habitación. |
| `confirmationNumber` | Cadena | El número o identificador de confirmación de la reserva. |
| `couponCode` | Cadena | Un código de cupón asociado con la reserva de hotel. |
| `created` | Entero | Este valor se registra cuando se crea una reserva. |
| `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para realizar la compra. |
| `discountPercent` | Duplicada | El porcentaje de descuento asociado con la reserva. |
| `freeCancelation` | Booleano | Indica si la habitación tiene una política de cancelación gratuita. |
| `guestID` | Cadena | El ID de huésped asociado con la reserva de hotel. |
| `length` | Entero | Número total de días de la reserva. |
| `loyaltyID` | Cadena | El ID del programa de fidelización del huésped que figura en la reserva. |
| `modification` | Entero | Este valor se registra cuando se modifica una reserva. |
| `modificationDate` | Fecha/Hora | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Entero | El número de niños asociados con la reserva. |
| `numberOfRooms` | Entero | El número de habitaciones asociadas con la reserva. |
| `propertyID` | Cadena | Identificador del hotel o resort de la reserva. |
| `propertyName` | Cadena | El nombre del hotel o resort de la reserva. |
| `purpose` | Cadena | El propósito de la reserva, por lo general, ya sea comercial o personal. |
| `ratePlan` | Cadena | La tarifa a la que se vendió la habitación. |
| `refundable` | Booleano | Indica si la habitación es reembolsable. |
| `reservationStatus` | Cadena | El estado de la reserva. |
| `roomAccessibilityType` | Cadena | El tipo de accesibilidad de la habitación, como movilidad, audición u otro. |
| `roomCapacity` | Entero | El número de personas de la habitación del hotel. |
| `roomType` | Cadena | El tipo de habitación que se está reservando. |
| `smoking` | Booleano | Indica si la habitación permite fumar. |
| `tripType` | Cadena | Indica si la reserva es para un viaje de ida, de ida y vuelta o de varias ciudades. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
