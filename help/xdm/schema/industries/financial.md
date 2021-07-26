---
solution: Experience Platform
title: Modelo de datos del sector de servicios financieros ERD
topic-legacy: overview
description: Vea un diagrama de relaciones de entidades (ERD) que describe un modelo de datos estandarizado para el sector bancario, de servicios financieros y de seguros (BFSI). Este modelo de datos es compatible con Experience Data Model (XDM) para su uso en Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# [!UICONTROL Modelo de datos del sector de los ] servicios financieros ERD

El siguiente diagrama de relaciones de entidades (ERD) representa un modelo de datos estandarizado para el sector bancario, de servicios financieros y de seguros (BFSI). El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD como se describe es una recomendación sobre cómo debe modelar sus datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe crear los esquemas recomendados y sus relaciones usted mismo. Consulte las guías sobre la administración de [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en una clase [Experience Data Model (XDM) subyacente](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

![](../../images/industries/financial.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el atributo de identificador único (`_id`) proporcionado por la clase ExperienceEvent XDM. Consulte el documento de referencia en [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.