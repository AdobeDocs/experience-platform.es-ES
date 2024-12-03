---
solution: Experience Platform
title: Modelo de datos del sector minorista
description: Vea un modelo de datos estandarizado para el sector minorista, compatible con el modelo de datos de experiencia (XDM) para su uso en Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# [!UICONTROL Comercial] modelo de datos del sector

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector minorista. El ERD se presenta intencionalmente de manera desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD tal como se describe es una recomendación sobre cómo debe modelar los datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe construir los esquemas recomendados y sus relaciones. Consulte las guías sobre la administración de [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en una clase [Experience Data Model (XDM) subyacente](../composition.md#class).
* Los campos con sangría debajo de un campo principal representan un campo secundario, o subcampo, que pertenece al grupo de campos del elemento principal.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que se pueden utilizar para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcada como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o individuo que realizó la transacción.

![Ejemplo de ERD para un modelo de datos de un sector comercial](../../images/industries/retail.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el atributo de identificador único (`_id`) proporcionado por la clase XDM ExperienceEvent. Consulte el documento de referencia sobre [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.

## Casos de uso de [!UICONTROL Retail]

En la siguiente tabla se describen las clases recomendadas y los grupos de campos de esquema para varios casos de uso minorista comunes.

| Ejemplo de uso | Clases y grupos de campos recomendados |
| --- | --- |
| Combine fuentes de datos en línea y sin conexión y resuelva la identidad entre dispositivos y en línea/sin conexión para proporcionar informes de atribución holísticos entre canales y dispositivos. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de Commerce](../../field-groups/event/commerce-details.md)</li><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Producto](../../classes/product.md)**:<ul><li>[Catálogo de productos](../../field-groups/product/product-catalog.md)</li><li>[Categoría del producto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Proporcione experiencias dirigidas y personalizadas para varios segmentos a fin de aumentar los ingresos y ayudar a aumentar la plataforma en la orquestación omnicanal. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de marketing de campaña](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalles de canal](../../field-groups/event/channel-details.md)</li><li>[Detalles de Commerce](../../field-groups/event/commerce-details.md)</li><li>[Detalles del entorno](../../field-groups/event/environment-details.md)</li><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Datos personales de contacto](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalles de contacto de trabajo](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analice la atribución multitáctil para mejorar la eficacia del marketing. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de marketing de campaña](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalles de canal](../../field-groups/event/channel-details.md)</li><li>[Detalles de Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Mejore la relevancia del correo electrónico mediante una segmentación mejorada para hombres y mujeres. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Producto](../../classes/product.md)**:<ul><li>[Catálogo de productos](../../field-groups/product/product-catalog.md)</li><li>[Categoría del producto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Ingeste datos de lealtad (socio) para aumentar la información relevante del producto en los canales web, de correo electrónico y de marketing digital. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Detalles demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalles de fidelización](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Producto](../../classes/product.md)**:<ul><li>[Catálogo de productos](../../field-groups/product/product-catalog.md)</li><li>[Categoría del producto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Reasigne a los abandonadores del carro de compras mediante correos electrónicos automatizados y personalizados. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Detalles de Commerce](../../field-groups/event/commerce-details.md)</li><li>[Detalles web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Producto](../../classes/product.md)**:<ul><li>[Catálogo de productos](../../field-groups/product/product-catalog.md)</li><li>[Categoría del producto](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
