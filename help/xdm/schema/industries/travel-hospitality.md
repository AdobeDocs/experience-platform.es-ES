---
solution: Experience Platform
title: Modelo de datos ERD de la industria de viajes y hospitalidad
topic-legacy: overview
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para el sector de viajes y hostelería, compatible con Experience Data Model (XDM) para su uso en Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# [!UICONTROL Modelo de datos de la industria de viajes y ] hospitalidad ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector de viajes y hostelería. El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD como se describe es una recomendación sobre cómo debe modelar sus datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe crear los esquemas recomendados y sus relaciones usted mismo. Consulte las guías sobre la administración de [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en una clase [Experience Data Model (XDM) subyacente](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>La entidad Evento de experiencia incluye un campo &quot;_ID&quot;, que representa el atributo de identificador único (`_id`) proporcionado por la clase ExperienceEvent XDM. Consulte el documento de referencia en [XDM ExperienceEvent](../../classes/experienceevent.md) para obtener más información sobre lo que se espera para este valor.