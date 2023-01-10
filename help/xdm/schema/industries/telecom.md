---
solution: Experience Platform
title: Modelo de datos ERD del sector de las telecomunicaciones
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para el sector de las telecomunicaciones, compatible con el modelo de datos de experiencias (XDM) para su uso en Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---

# [!UICONTROL Telecomunicaciones] modelo de datos de la industria ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector de las telecomunicaciones. El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD como se describe es una recomendación sobre cómo debe modelar sus datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe crear los esquemas recomendados y sus relaciones usted mismo. Consulte las guías sobre la administración [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en un [Clase del Modelo de datos de experiencia (XDM)](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el identificador único (`_id`) proporcionado por la clase XDM ExperienceEvent . Consulte el documento de referencia sobre [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.

## [!UICONTROL Telecomunicaciones] casos de uso

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso comunes en el sector de las telecomunicaciones.

| Caso de uso | Clases recomendadas y grupos de campos |
| --- | --- |
| Comprender a los clientes que son buenos candidatos para oportunidades de ventas cruzadas o de incremento de ventas en función de sus carteras actuales y su comportamiento de navegación. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de ventas adicionales]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Detalles de la actualización]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Suscripción a Telecom]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Detalles demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalles de contacto personal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Reasigne como objetivo a los abandonadores del carro de compras mediante anuncios relevantes y correos electrónicos personalizados automatizados. Suprima los anuncios cuando se conviertan. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles del comercio]](../../field-groups/event/upsell-details.md) (Para capturar abandonos del carro de compras)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Suscripción a Telecom]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Detalles demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalles de contacto personal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Cuando se marca que un cliente tiene probabilidad de producirse (según la interacción de un empleado o un algoritmo automatizado de aprendizaje automático), envíe los detalles del cliente a canales digitales y no digitales. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de marketing de campaña]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Detalles del canal]](../../field-groups/event/channel-details.md)</li><li>Un grupo de campos personalizado con contenido personalizado</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalles de contacto personal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
