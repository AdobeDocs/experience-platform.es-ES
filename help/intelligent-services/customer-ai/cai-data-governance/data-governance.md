---
keywords: Experience Platform;control de datos;ayuda al cliente;temas populares
solution: Experience Platform
feature: Customer AI
title: Control de datos en Customer AI
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados para cumplir con sus prácticas comerciales, obligaciones legales y procesos de desarrollo.
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: 0fcdb358882fba7f7923e5d6fc1a947699276e18
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 9%

---

# AI del cliente y control de datos

Cualquier configuración relacionada con el control de datos en Customer AI se hereda de Adobe Experience Platform.

## Control de datos {#governance}

La integración entre Customer AI y Adobe Experience Platform Data Governance le permite controlar y comprender sus datos en todo su recorrido a través de Platform. Esto implica mantener la calidad de los datos, el linaje de datos, la catalogación de datos y mucho más.

Las etiquetas y políticas de uso de datos que se crearon en conjuntos de datos consumidos por Platform se pueden ver en el flujo de trabajo de configuración de Customer AI . Estas etiquetas detienen o advierten a los usuarios que utilizan campos etiquetados.

Esta integración le permite administrar el cumplimiento de normas de forma más eficiente. Los administradores de datos de su organización pueden establecer políticas para restringir el uso. Como resultado, puede utilizar datos que cumplan las políticas definidas por los administradores de datos. Lea la documentación de [Etiquetas y políticas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html?lang=es) para obtener más información.

## Política de consentimiento {#consent-policy}

Customer AI respeta sus preferencias de consentimiento. Una vez que haya [configurar y activar la directiva de consentimiento](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=es#consent-policy), Customer AI respetará los datos de consentimiento recopilados por usted. Solo se utilizan datos consentidos para puntuar el modelo en ejecuciones posteriores del modelo. Las nuevas puntuaciones reemplazarán a las anteriores y se podrán utilizar en la segmentación. Actualmente, esta función solo está disponible para clientes de HealthCare Shield y clientes de Privacy and Security Shield.

Puede obtener más información sobre esta función aquí:

[Introducción a Customer AI](../../customer-ai/getting-started.md)
[Adobe Experience Platform y aplicaciones](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Diagramas de arquitectura de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
