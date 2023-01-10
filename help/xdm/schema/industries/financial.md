---
solution: Experience Platform
title: Modelo de datos del sector de servicios financieros ERD
description: Vea un diagrama de relaciones de entidades (ERD) que describe un modelo de datos estandarizado para el sector bancario, de servicios financieros y de seguros (BFSI). Este modelo de datos es compatible con Experience Data Model (XDM) para su uso en Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# [!UICONTROL Servicios financieros] modelo de datos de la industria ERD

El siguiente diagrama de relaciones de entidades (ERD) representa un modelo de datos estandarizado para el sector bancario, de servicios financieros y de seguros (BFSI). El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD como se describe es una recomendación sobre cómo debe modelar sus datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe crear los esquemas recomendados y sus relaciones usted mismo. Consulte las guías sobre la administración [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en un [Clase del Modelo de datos de experiencia (XDM)](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

![](../../images/industries/financial.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el identificador único (`_id`) proporcionado por la clase XDM ExperienceEvent . Consulte el documento de referencia sobre [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.

## [!UICONTROL Servicios financieros] casos de uso

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso financiero comunes.

| Caso de uso | Clases recomendadas y grupos de campos |
| --- | --- |
| Impulse la personalización a escala para segmentos preferidos mediante perspectivas de informes omnicanal y automatice los recorridos para aumentar la inscripción en un programa de recompensas preferido. | <ul><li>**[[!UICONTROL Producto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoría del producto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Acciones de tarjeta]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Detalles de solicitud de cotización]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Detalles del depósito]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Detalles del canal]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Transferencias de saldo]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalles de contacto personal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalles de fidelidad]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimice la personalización entre canales en los canales en línea y sin conexión. | <ul><li>**[[!UICONTROL Producto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoría del producto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles del canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalles de contacto personal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalles de fidelidad]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Impulse nuevas oportunidades de ingresos mediante el uso de perspectivas obtenidas del análisis de comportamiento entre canales, identificando patrones de uso del producto que podrían conducir a nuevas ofertas de productos. | <ul><li>**[[!UICONTROL Directiva]](../../classes/policy.md)**</li><li>**[[!UICONTROL Producto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoría del producto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Acciones de tarjeta]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Compatibilidad con la búsqueda en el sitio]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Detalles del depósito]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Detalles del canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalles de contacto personal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalles de fidelidad]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
