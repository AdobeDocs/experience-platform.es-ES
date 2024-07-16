---
keywords: Experience Platform;control de datos;inteligencia artificial aplicada al cliente;temas populares
solution: Experience Platform
feature: Customer AI
title: Administración de datos en Customer AI
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados para cumplir con las prácticas comerciales, las obligaciones legales y el proceso de desarrollo.
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# Inteligencia artificial aplicada al cliente y administración de datos en Customer AI

Cualquier configuración relacionada con la gobernanza de datos en la inteligencia artificial aplicada al cliente se hereda de Adobe Experience Platform.

## Control de datos {#governance}

La integración entre la inteligencia artificial aplicada al cliente y la gobernanza de datos de Adobe Experience Platform le permite controlar y comprender los datos a través de su recorrido mediante Platform. Esto implica mantener la calidad de los datos, el linaje, la catalogación y mucho más.

Las etiquetas y políticas de uso de datos creadas en conjuntos de datos consumidos por Platform se pueden ver en el flujo de trabajo de configuración de la inteligencia artificial aplicada al cliente. Estas etiquetas detienen o advierten a los usuarios que utilizan campos etiquetados.

Esta integración le permite administrar el cumplimiento de normas de forma más eficiente. Los administradores de datos de su organización pueden establecer políticas para restringir el uso. Como resultado, puede utilizar datos que cumplan con las directivas definidas por los administradores de datos. Lea la documentación de [Etiquetas y directivas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) para obtener más información.

## Política de consentimiento {#consent-policy}

La inteligencia artificial aplicada al cliente respeta sus preferencias de consentimiento. Una vez que haya [configurado y habilitado su directiva de consentimiento](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=es#consent-policy), la inteligencia artificial aplicada al cliente aceptará los datos de consentimiento recopilados de usted. Solo se utilizan datos consentidos para puntuar el modelo en ejecuciones posteriores del modelo. Las nuevas puntuaciones reemplazarán las puntuaciones antiguas y se pueden utilizar en la segmentación. Actualmente, esta función solo está disponible para los clientes de HealthCare Shield y para los clientes de Privacy and Security shield.

Puede obtener más información sobre esta función aquí:

[Introducción a la inteligencia artificial aplicada al cliente](../../customer-ai/getting-started.md)
[Adobe Experience Platform y aplicaciones](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Diagramas de arquitectura de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html?lang=es)
