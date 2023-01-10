---
solution: Experience Platform
title: Información general sobre los modelos de datos del sector
description: Obtenga información sobre los modelos de datos estandarizados para varias verticales del sector que se pueden construir con componentes estándar del Modelo de datos de experiencia (XDM).
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# Resumen de los modelos de datos del sector

El Modelo de datos de experiencia (XDM) le permite crear esquemas altamente personalizables para capturar datos clave de experiencia del cliente relacionados con su negocio. Para ayudar a agilizar el proceso de modelado de los datos para ajustarlos a XDM, Adobe Experience Platform proporciona un versátil conjunto de componentes XDM estándar, que capturan conceptos que se utilizan comúnmente en varias industrias.

>[!NOTE]
>
>Los nuevos componentes XDM estándar se lanzan continuamente para adaptarse mejor a las necesidades del consumidor. Para obtener una lista de los componentes más actualizados, puede [explorar los recursos existentes en la interfaz de usuario](../../ui/explore.md) o consulte [repositorio oficial XDM](https://github.com/adobe/xdm/tree/master/components) en GitHub.

Según el sector en el que opere su empresa, algunos componentes XDM serán más relevantes para sus necesidades que otros. Además, las relaciones que establezca entre sus esquemas XDM variarán según su sector.

A fin de ayudar a orientar su estrategia de modelado de datos en función de su sector particular, esta guía proporciona una referencia de diagramas de relaciones con las entidades (ERD) para varias verticales del sector compatibles.

## Requisitos previos

Para leer los ERD a los que se hace referencia en esta guía, debe tener una comprensión práctica de cómo los componentes XDM interactúan con los esquemas de formularios y cómo funcionan los esquemas XDM en el Experience Platform en su conjunto. Asegúrese de haber leído la siguiente documentación general antes de continuar:

* [Información general del sistema XDM](../../home.md): Descubra cómo funciona XDM en el ecosistema de la plataforma.
* [Aspectos básicos de la composición del esquema](../../schema/composition.md): Descubra cómo los componentes XDM (como grupos de campos de esquema, clases y tipos de datos) contribuyen a la estructura de un esquema, así como la función de los campos de identidad.

También se recomienda que revise el [guía de prácticas recomendadas para modelado de datos](../../schema/best-practices.md) para obtener directrices generales sobre cómo asignar los datos a XDM.

## Modelo de datos del sector ERD {#erds}

Los ERD se proporcionan para las siguientes verticales industriales:

* [[!UICONTROL Comercial]](./retail.md)
* [[!UICONTROL Servicios financieros]](./financial.md)
* [[!UICONTROL Atención]](./healthcare.md)
* [[!UICONTROL Telecomunicaciones]](./telecom.md)
* [[!UICONTROL Viajes y hospitalidad]](./travel-hospitality.md)

## Pasos siguientes

Este documento ofrecía una visión general de los modelos de datos industriales ERD y de cómo interpretarlos. Para ver un ERD, seleccione uno de la lista anterior.
