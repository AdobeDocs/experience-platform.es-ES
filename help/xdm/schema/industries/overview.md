---
solution: Experience Platform
title: Información general sobre los modelos de datos del sector
topic: sobre validación
description: Obtenga información sobre los modelos de datos estandarizados para varias verticales del sector que se pueden construir con componentes estándar del Modelo de datos de experiencia (XDM).
translation-type: tm+mt
source-git-commit: 6a7aebb64a533158f7ab17af0cd28243aeda0eca
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Resumen de los modelos de datos del sector

El Modelo de datos de experiencia (XDM) le permite crear esquemas altamente personalizables para capturar datos clave de experiencia del cliente relacionados con su negocio. Para ayudar a agilizar el proceso de modelado de los datos para ajustarlos a XDM, Adobe Experience Platform proporciona un versátil conjunto de componentes XDM estándar, que capturan conceptos que se utilizan comúnmente en varias industrias.

>[!NOTE]
>
>Los nuevos componentes XDM estándar se lanzan continuamente para adaptarse mejor a las necesidades del consumidor. Para obtener una lista de los componentes más actualizados, puede [explorar los recursos existentes en la interfaz de usuario](../../ui/explore.md) o consultar el [repositorio XDM oficial](https://github.com/adobe/xdm/tree/master/components) en GitHub.

Según el sector en el que opere su empresa, algunos componentes XDM serán más relevantes para sus necesidades que otros. Además, las relaciones que establezca entre sus esquemas XDM variarán según su sector.

A fin de ayudar a orientar su estrategia de modelado de datos en función de su sector particular, esta guía proporciona una referencia de diagramas de relaciones con las entidades (ERD) para varias verticales del sector compatibles.

## Requisitos previos

Para leer los ERD a los que se hace referencia en esta guía, debe tener una comprensión práctica de cómo los componentes XDM interactúan con los esquemas de formularios y cómo funcionan los esquemas XDM en el Experience Platform en su conjunto. Asegúrese de haber leído la siguiente documentación general antes de continuar:

* [Información general](../../home.md) del sistema XDM: Descubra cómo funciona XDM en el ecosistema de la plataforma.
* [Aspectos básicos de la composición](../../schema/composition.md) del esquema: Descubra cómo los componentes XDM (como mezclas, clases y tipos de datos) contribuyen a la estructura de un esquema, así como la función de los campos de identidad.

También se recomienda revisar la [guía de prácticas recomendadas de modelado de datos](../../schema/best-practices.md) para obtener directrices generales sobre cómo asignar los datos a XDM.

## Modelo de datos del sector ERD {#erds}

Los modelos verticales del sector representados por los ERD que figuran a continuación se crean intencionadamente de manera desnormalizada y teniendo en cuenta cómo se almacenan los datos en la Plataforma.

Para un ERD determinado, cada entidad mostrada en se basa en una clase XDM subyacente. Para una entidad determinada, cada fila marcada con **bold** representa una mezcla o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita. Los campos más importantes de una entidad determinada se resaltan en rojo.

>[!NOTE]
>
>Algunas entidades pueden incluir un campo &quot;_ID&quot;. Representa el identificador único (`_id`) que Platform asigna automáticamente a las entidades de evento o perfil cuando se incorporan. Sin embargo, puede elegir utilizar sus propios valores de ID únicos para este campo si lo desea.

Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.

Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

Los ERD se proporcionan para las siguientes verticales industriales:

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)
* [[!UICONTROL Telecommunications]](./telecom.md)

## Pasos siguientes

Este documento ofrecía una visión general de los modelos de datos industriales ERD y de cómo interpretarlos. Para ver un ERD, seleccione uno de la lista anterior.