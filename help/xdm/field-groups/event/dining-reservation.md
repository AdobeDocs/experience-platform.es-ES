---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;reserva;comedor;
title: Grupo de campos de esquema de reserva de comedor
description: Este documento proporciona una descripción general del grupo de campos Esquema de reserva de comedor.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---


# [!UICONTROL Grupo de campos de esquema de ] reserva de comedor

[!UICONTROL Dining ] Reservationes un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) visitante que captura información relacionada con una reserva de comedor.

El grupo de campos es una extensión del grupo de campos [!UICONTROL Detalles de reserva] y contiene todos los mismos campos bajo un único campo de tipo de objeto, `reservations`. Además de estos campos genéricos, [!UICONTROL Dining Reservation] también incluye la matriz `diningReservations`. Esta matriz de objetos se utiliza para describir una o más reservas con propiedades específicas del restaurante.

>[!NOTE]
>
>Este documento cubre los detalles de la matriz `diningReservations`. Para obtener información sobre los demás campos proporcionados en el objeto `reservations`, consulte la referencia del grupo de campos [[!UICONTROL Detalles de reserva]](./reservation-details.md).

![Estructura de la reserva](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` es una matriz de objetos que representa una lista de reservas de comedor. Si un evento de reserva implica reservas en varios restaurantes diferentes en diferentes momentos del día, por ejemplo, estas reservas se pueden listar como objetos individuales en `diningReservations` para un solo evento.

A continuación se proporciona la estructura de cada objeto proporcionada en `diningReservations`.

![comedorEstructura de reservas](../../images/field-groups/dining-reservation/diningReservations.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ID` | Cadena | El número o identificador de reserva. |
| `cancellation` | Número entero | Este valor se captura cuando se cancela una reserva. |
| `confirmationNumber` | Cadena | El número o identificador de confirmación de la reserva. |
| `created` | Número entero | Este valor se captura cuando se crea una reserva. |
| `cuisine` | Número entero | El tipo de cocina del restaurante |
| `currencyCode` | Cadena | El código de moneda ISO 4217 utilizado para realizar la compra. |
| `deliveryPartners` | Cadena | Socios de envío disponibles en el restaurante. |
| `diningOptions` | Cadena | El restaurante ofrece platos a la carta y a la carta. |
| `groupReservation` | Booleano | Indica si la reserva se está realizando para un grupo. |
| `length` | Número entero | Número total de días para la reserva. |
| `loyaltyID` | Cadena | El ID del programa de fidelidad para el invitado indicado en la reserva. |
| `modification` | Número entero | Este valor se captura cuando se modifica una reserva. |
| `modificationDate` | DateTime | Hora a la que se modificó la reserva por última vez. |
| `numberOfAdults` | Número entero | El número de adultos asociados con la reserva. |
| `numberOfChildren` | Número entero | Número de niños asociados a la reserva. |
| `numberOfRooms` | Número entero | Número de habitaciones asociadas a la reserva. |
| `partySize` | Número entero | El número de personas en la fiesta. |
| `priceCategory` | Cadena | La categoría de precios de la reserva que se está realizando. |
| `purpose` | Cadena | El propósito de la reserva, generalmente de negocios o personal. |
| `reservationTime` | DateTime | La hora para la que se reserva la reserva. |
| `restaurantID` | Cadena | Identificador del restaurante o de la zona de comedor. |
| `reservationStatus` | Cadena | El estado de la reserva. |
| `specialOccasion` | Booleano | Indica si la reserva se está realizando para una ocasión especial. |
| `status` | Número entero | El estado de la reserva para comidas. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
