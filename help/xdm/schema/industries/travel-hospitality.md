---
solution: Experience Platform
title: Modelo de datos ERD de la industria de viajes y hospitalidad
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para el sector de viajes y hostelería, compatible con Experience Data Model (XDM) para su uso en Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL Viajes y hospitalidad] modelo de datos de la industria ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector de viajes y hostelería. El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD como se describe es una recomendación sobre cómo debe modelar sus datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe crear los esquemas recomendados y sus relaciones usted mismo. Consulte las guías sobre la administración [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en un [Clase del Modelo de datos de experiencia (XDM)](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el identificador único (`_id`) proporcionado por la clase XDM ExperienceEvent . Consulte el documento de referencia sobre [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.

## [!UICONTROL Viajes y hospitalidad] casos de uso

En la siguiente tabla se describen las clases recomendadas y los grupos de campo de esquema para varios casos de uso comunes en la industria de viajes y hospitalidad.

| Caso de uso | Clases recomendadas y grupos de campos |
| --- | --- |
| Venta cruzada de restaurantes y otros lugares de interés para huéspedes del mercado y clientes con próximas reservas de hotel. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de alojamiento](../../field-groups/event/lodging-reservation.md)</li><li>[Reserva de comedor](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de contacto personal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Para los huéspedes del hotel y clientes con reservas de hotel, el hotel ofrece servicio de lavandería. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de comedor](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de contacto personal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li><li>[Detalles de fidelidad](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Hotel de alta venta y otros lugares de interés para huéspedes en el mercado y clientes con próximas reservas de hotel. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de alojamiento](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de contacto personal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li><li>[Detalles de fidelidad](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Para los clientes en el mercado y los clientes con reservas de hotel, venda vuelos y otros lugares de interés. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles de la reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de vuelo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de contacto personal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li><li>[Detalles de fidelidad](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
