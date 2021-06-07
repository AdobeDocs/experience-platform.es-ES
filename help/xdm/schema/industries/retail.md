---
solution: Experience Platform
title: Modelo de datos del sector minorista ERD
topic-legacy: overview
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para el sector minorista, compatible con el modelo de datos de experiencias (XDM) para su uso en Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 629f47b934c59fe875a54cb13962033122097538
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

#  Modelo de datos del sector minorista ERD

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