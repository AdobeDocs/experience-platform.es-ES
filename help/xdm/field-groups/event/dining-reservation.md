---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;reservación;comedor;
title: Grupo de campos de esquema de reserva de restaurante
description: Obtenga información acerca del grupo de campos Esquema de reserva de restaurante.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 13%

---

# [!UICONTROL Reserva de restaurante] grupo de campos de esquema

[!UICONTROL Reserva de restaurante] es un grupo de campo de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) que se usa para capturar información sobre una reserva de restaurante.

El grupo de campos es una extensión del grupo de campos [!UICONTROL Detalles de la reserva] y contiene todos los campos iguales en un único campo de tipo de objeto, `reservations`. Además de estos campos genéricos, [!UICONTROL Reserva para comer] también incluye la matriz `diningReservations`. Esta matriz de objetos se utiliza para describir una o más reservas con propiedades específicas de restaurantes.

>[!NOTE]
>
>Este documento cubre los detalles de la matriz `diningReservations`. Para obtener información sobre los demás campos proporcionados en el objeto `reservations`, consulte la [[!UICONTROL Referencia del grupo de campos Detalles de la reserva]](./reservation-details.md).

![Estructura de reserva de restaurante](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` es una matriz de objetos que representa una lista de reservas de restaurantes. Si un evento de reserva implica reservas en varios restaurantes diferentes a distintas horas del día, por ejemplo, estas reservas pueden enumerarse como objetos individuales en `diningReservations` para un único evento.

A continuación se proporciona la estructura de cada objeto proporcionado en `diningReservations`.

![estructura de reserva para restaurantes](../../images/field-groups/dining-reservation/diningReservations.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ID` | Cadena | El número o identificador de la reserva. |
| `cancellation` | Entero | Este valor se registra cuando se cancela una reserva. |
| `confirmationNumber` | Cadena | El número o identificador de confirmación de la reserva. |
| `created` | Entero | Este valor se registra cuando se crea una reserva. |
| `cuisine` | Entero | El tipo de cocina del restaurante. |
| `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para realizar la compra. |
| `deliveryPartners` | Cadena | Socios de entrega disponibles en el restaurante. |
| `diningOptions` | Cadena | Opciones para comer y de envío que ofrece el restaurante. |
| `groupReservation` | Booleano | Indica si la reserva es para un grupo. |
| `length` | Entero | Número total de días de la reserva. |
| `loyaltyID` | Cadena | El ID del programa de fidelización del huésped que figura en la reserva. |
| `modification` | Entero | Este valor se registra cuando se modifica una reserva. |
| `modificationDate` | Fecha/Hora | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Entero | El número de niños asociados con la reserva. |
| `numberOfRooms` | Entero | El número de habitaciones asociadas con la reserva. |
| `partySize` | Entero | El número de personas en el comedor. |
| `priceCategory` | Cadena | La categoría de precio de la reserva que se está realizando. |
| `purpose` | Cadena | El propósito de la reserva, por lo general, ya sea comercial o personal. |
| `reservationTime` | Fecha/Hora | La hora de reserva de la mesa. |
| `restaurantID` | Cadena | Identificador de la ubicación del restaurante o la mesa. |
| `reservationStatus` | Cadena | El estado de la reserva. |
| `specialOccasion` | Booleano | Indica si la reserva es para una ocasión especial. |
| `status` | Entero | El estado de reserva de la mesa. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
