---
solution: Experience Platform
title: Modelo de datos de la industria de telecomunicaciones ERD
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para la industria de telecomunicaciones, compatible con el Modelo de datos de experiencia (XDM) para su uso en Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# [!UICONTROL Telecomunicaciones] modelo de datos del sector ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para la industria de las telecomunicaciones. El ERD se presenta intencionalmente de manera desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD tal como se describe es una recomendación sobre cómo debe modelar los datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe construir los esquemas recomendados y sus relaciones. Consulte las guías sobre la administración de [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la IU de para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en un subyacente [Clase del modelo de datos de experiencia (XDM)](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **negrita** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que se pueden utilizar para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcada como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o individuo que realizó la transacción.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el identificador único (`_id`) proporcionado por la clase XDM ExperienceEvent. Consulte el documento de referencia sobre [ExperienceEvent de XDM](../../classes/experienceevent.md) para obtener más información sobre qué se espera de este valor.

## [!UICONTROL Telecomunicaciones] casos de uso

En la siguiente tabla se describen las clases recomendadas y los grupos de campos de esquema para varios casos de uso comunes del sector de las telecomunicaciones.

| Caso de uso | Clases y grupos de campos recomendados |
| --- | --- |
| Comprenda a los clientes que son buenos candidatos para las oportunidades de ampliación de ventas o de venta cruzada en función de sus tenencias actuales y de su comportamiento de navegación. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de ampliación de venta]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Detalles de actualización]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Suscripción de telecomunicaciones]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Datos demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Datos personales de contacto]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Reasigne a los abandonadores del carro de compras con anuncios relevantes y correos electrónicos personalizados automatizados. Suprimir anuncios cuando se convierten. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de comercio]](../../field-groups/event/upsell-details.md) (Para capturar abandonos del carro de compras)</li></ul></li><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Suscripción de telecomunicaciones]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Datos demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Datos personales de contacto]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Cuando se marque la probabilidad de pérdida de un cliente (según la interacción de un empleado o un algoritmo automatizado de aprendizaje automático), envíe los detalles del cliente a canales digitales y no digitales. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de marketing de campaña]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Detalles del canal]](../../field-groups/event/channel-details.md)</li><li>Un grupo de campos personalizados que contiene contenido personalizado</li></ul></li><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Datos demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Datos personales de contacto]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
