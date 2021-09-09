---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;reserva;vuelo;
title: Grupo de campos de esquema de reserva de vuelo
description: Este documento proporciona una descripción general del grupo de campos de esquema Reserva de vuelo .
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 4%

---


# [!UICONTROL Grupo de campos Flight ] Reservationschema

[!UICONTROL La ] reserva de vuelo es un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) visitante que captura información relacionada con una reserva de vuelo.

El grupo de campos es una extensión del grupo de campos [!UICONTROL Detalles de reserva] y contiene todos los mismos campos bajo un único campo de tipo de objeto, `reservations`. Además de estos campos genéricos, [!UICONTROL Reserva de vuelo] también incluye la matriz `flightReservations`. Esta matriz de objetos se utiliza para describir una o más reservas con propiedades exclusivas del transporte aéreo.

>[!NOTE]
>
>Este documento cubre los detalles de la matriz `flightReservations`. Para obtener información sobre los demás campos proporcionados en el objeto `reservations`, consulte la referencia del grupo de campos [[!UICONTROL Detalles de reserva]](./reservation-details.md).

![Estructura de la reserva de vuelo](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` es una matriz de objetos que representa una lista de reservas de vuelos. Si un evento de reserva implica reservas para múltiples vuelos de conexión en un viaje, por ejemplo, estas reservas pueden aparecer como objetos individuales en `flightReservations` para un solo evento.

A continuación se proporciona la estructura de cada objeto proporcionada en `flightReservations`.

![estructura de las reservas de vuelo](../../images/field-groups/flight-reservation/flightReservations.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `flightCheckIn` | Objeto | Captura detalles sobre el check-in de vuelo. El objeto incluye las siguientes propiedades:<ul><li>`arrivalAirportCode`: (Cadena) El código de aeropuerto de la ciudad de llegada.</li><li>`boardingGroup`: (Cadena) Indicador de orden de embarque específico de la compañía aérea.</li><li>`checkInMethod`: (Cadena) El método utilizado para registrar datos, como contador, en línea, quiosco o autoservicio.</li><li>`checkedBags`: (Número entero) El número de bolsas comprobadas para el vuelo.</li><li>`checkedPassengers`: (Número entero) El número de pasajeros facturados para el vuelo, si existen varios pasajeros para el mismo número de reserva.</li><li>`confirmationNumber`: (Cadena) El número o identificador de confirmación de la reserva.</li><li>`departureAirportCode`: (Cadena) El código de aeropuerto de la ciudad de salida.</li><li>`flightNumber`: (Cadena) El número de vuelo para el vuelo que se va a reservar.</li></ul> |
| `flightStatusSearch` | Objeto | Captura los detalles devueltos cuando se busca el estado del vuelo. El objeto incluye las siguientes propiedades:<ul><li>`arrivalAirportCode`: (Cadena) El código de aeropuerto de la ciudad de llegada.</li><li>`boardingGroup`: (Cadena) Indicador de orden de embarque específico de la compañía aérea.</li><li>`departureAirportCode`: (Cadena) El código de aeropuerto de la ciudad de salida.</li><li>`departureDate`: (DateTime) La fecha de salida del vuelo que se va a reservar.</li><li>`flightNumber`: (Cadena) El número de vuelo para el vuelo que se va a reservar.</li><li>`searchCount`: (Número entero) El número de veces que se ha buscado el estado del vuelo reservado.</li></ul> |
| `agentID` | Cadena | El agente o contable responsable de reservar la reserva, si procede. |
| `aircraftID` | Cadena | Identificador de la aeronave. |
| `aircraftType` | Cadena | El tipo de aeronave. |
| `arrivalAirportCode` | Cadena | El código de aeropuerto de la ciudad de llegada. |
| `arrivalDate` | DateTime | La fecha de llegada del vuelo que se va a reservar. |
| `cancellation` | Número entero | Este valor se captura cuando se cancela una reserva. |
| `confirmationNumber` | Cadena | El número o identificador de confirmación de la reserva. |
| `created` | Cadena | Este valor se captura cuando se crea una reserva. |
| `currencyCode` | Cadena | El código de moneda ISO 4217 utilizado para realizar la compra. |
| `departureAirportCode` | Cadena | El código del aeropuerto de la ciudad de salida. |
| `departureDate` | DateTime | La fecha de salida del vuelo que se va a reservar. |
| `fareClass` | Cadena | Clase de tarifa del vuelo que se reserva. |
| `flightNumber` | Cadena | Número de vuelo del vuelo que se va a reservar. |
| `length` | Número entero | Número total de días para la reserva. |
| `loyaltyID` | Cadena | El ID del programa de fidelidad o recompensas para el pasajero enumerado en la reserva. |
| `modification` | Número entero | Este valor se captura cuando se modifica una reserva. |
| `modificationDate` | DateTime | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Número entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Número entero | Número de niños asociados a la reserva. |
| `passengerID` | Cadena | Información del pasajero asociada a la reserva. |
| `purpose` | Cadena | El propósito de la reserva, generalmente de negocios o personal. |
| `salesChannel` | Cadena | Canal de ventas desde el cual se reservó la reserva. |
| `securityScreening` | Cadena | El tipo de control de seguridad al que está sujeto el pasajero. |
| `status` | Cadena | El estado de la reserva de vuelo. |
| `ticketNumber` | Cadena | El número o identificador de reserva. |
| `tripType` | Cadena | Indica si la reserva es para un viaje de ida, de ida y vuelta o de varias ciudades. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
