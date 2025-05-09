---
solution: Experience Platform
title: Modelo de datos de la industria de viajes y hospitalidad
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para la industria de viajes y hospitalidad, compatible con el Modelo de datos de experiencia (XDM) para su uso en Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!UICONTROL Viajes y hospitalidad] modelo de datos de la industria ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para la industria de viajes y hospitalidad. El ERD se presenta intencionalmente de manera desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD tal como se describe es una recomendación sobre cómo debe modelar los datos para este caso de uso del sector. Para utilizar este modelo de datos en Experience Platform, debe construir los esquemas recomendados y sus relaciones. Consulte las guías sobre la administración de [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en una clase [Experience Data Model (XDM) subyacente](../composition.md#class).
* Los campos con sangría debajo de un campo principal representan un campo secundario, o subcampo, que pertenece al grupo de campos del elemento principal.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que se pueden utilizar para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcada como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o individuo que realizó la transacción.

![Ejemplo de ERD para un modelo de datos de hospitalidad de viajes](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el atributo de identificador único (`_id`) proporcionado por la clase XDM ExperienceEvent. Consulte el documento de referencia sobre [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.

## Casos de uso de [!UICONTROL Viajes y hospitalidad]

En la siguiente tabla se describen las clases recomendadas y los grupos de campos de esquema para varios casos de uso comunes del sector de viajes y hospitalidad.

| Ejemplo de uso | Clases y grupos de campos recomendados |
| --- | --- |
| Venta cruzada de restaurantes y otras atracciones residentes para los huéspedes del mercado y los huéspedes con próximas reservas de hotel. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de alojamiento](../../field-groups/event/lodging-reservation.md)</li><li>[Reserva de restaurante](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Datos personales de contacto](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Ofrezca a los huéspedes del hotel una amplia gama de servicios de calidad y entretenimiento en este hotel en Londres. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de restaurante](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Datos personales de contacto](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li><li>[Detalles de fidelización](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Ofreciendo a los huéspedes del hotel una amplia gama de servicios de calidad, el The Grand Hotel se compromete a garantizarle la estancia más confortable. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de alojamiento](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Datos personales de contacto](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li><li>[Detalles de fidelización](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Ofrezca a los huéspedes del hotel y a los huéspedes del hotel próximas reservas de vuelos y otras atracciones locales. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de vuelo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Datos personales de contacto](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li><li>[Detalles de fidelización](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
