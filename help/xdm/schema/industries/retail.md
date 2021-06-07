---
solution: Experience Platform
title: Modelo de datos del sector minorista
topic-legacy: overview
description: Vea un modelo de datos estandarizado para el sector minorista, compatible con Experience Data Model (XDM) para su uso en Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 9c5a4e064af0b46ff30b41afef71ca2fd3503a82
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

#  Modelo de datos del sector minorista

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector minorista. El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en una clase [Experience Data Model (XDM) subyacente](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

![](../../images/industries/retail.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el atributo de identificador único (`_id`) proporcionado por la clase ExperienceEvent XDM. Consulte el documento de referencia en [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.

##  Casos de uso minorista

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso minorista comunes.

| Caso de uso | Clases recomendadas y grupos de campos |
| --- | --- |
| Combine fuentes de datos en línea y sin conexión y resuelva la identidad entre dispositivos y sin conexión para proporcionar informes holísticos de atribución entre canales y dispositivos. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles del comercio](../../field-groups/event/commerce-details.md)</li><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**Producto**  (clase personalizada)\*:<ul><li>Producto (grupo de campos personalizados)\*</li></ul></li></ul> |
| Proporcione experiencias personalizadas y dirigidas para varios segmentos a fin de aumentar los ingresos y ayudar a aumentar la plataforma en la orquestación omnicanal. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles de marketing de campaña](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalles del canal](../../field-groups/event/channel-details.md)</li><li>[Detalles del comercio](../../field-groups/event/commerce-details.md)</li><li>[Detalles del entorno](../../field-groups/event/environment-details.md)</li><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de contacto personal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analice la atribución de múltiples contactos para mejorar la eficacia del marketing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles de marketing de campaña](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalles del canal](../../field-groups/event/channel-details.md)</li><li>[Detalles del comercio](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Mejore la relevancia del correo electrónico mediante una segmentación mejorada para hombres y mujeres. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles del comercio](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**Producto**  (clase personalizada)\*:<ul><li>Producto (grupo de campos personalizados)\*</li></ul></li></ul> |
| Ingeste datos de fidelidad (socio) para aumentar la información relevante del producto en los canales web, de correo electrónico y de marketing digital. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de fidelidad](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**Producto**  (clase personalizada)\*:<ul><li>Producto (grupo de campos personalizados)\*</li></ul></li></ul> |
| Reasigne como objetivo a los abandonadores del carro de compras mediante correos electrónicos automatizados y personalizados. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalles del comercio](../../field-groups/event/commerce-details.md)</li><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**Producto**  (clase personalizada)\*:<ul><li>Producto (grupo de campos personalizados)\*</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Aunque se ha planificado una clase de producto estándar para una versión futura, los esquemas de producto deben crearse actualmente utilizando una clase personalizada en su lugar. Por lo tanto, debe crear manualmente la estructura de la clase del esquema, así como la de los grupos de campos que agregue a ella. Consulte la sección [creación de una clase personalizada](../../ui/resources/classes.md#create) en la guía de la interfaz de usuario de XDM para obtener más información.*
