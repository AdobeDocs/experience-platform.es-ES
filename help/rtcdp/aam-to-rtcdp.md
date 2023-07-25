---
title: Evolución de Audience Manager a Real-Time CDP
description: Comprenda las consideraciones antes de planificar la migración de Audience Manager a Real-Time CDP.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: ht
source-wordcount: '538'
ht-degree: 100%

---


# Evolución de Audience Manager a Real-Time CDP

A medida que su organización evoluciona para utilizar Adobe Real-Time CDP, explore estas consideraciones para preparar sus datos y tomar conciencia de las diferencias críticas entre las dos tecnologías. Este artículo está dirigido a un público profesional.

![Diagrama de evolución de Audience Manager a Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Considere la arquitectura de datos dentro de Audience Manager

Teniendo en cuenta la evolución de Audience Manager a Real-Time CDP, ahora es un momento crítico para analizar sus [segmentos de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=es) y determinar qué [señales](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=es), [rasgos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=es) y [reglas](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=es#segment-builder-section) son los que los componen.

Además, piense en las fuentes de datos que emplea actualmente en Audience Manager.

Adobe recomienda clasificar los segmentos de la siguiente manera:

* Segmentos que se pueden enviar a Experience Platform a través del [[!UICONTROL Conector de origen de Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), ya que no tienen dependencias de datos, no hay desafíos de destino o activación y sus reglas de segmentación se pueden crear a través del [generador de segmentos](/help/segmentation/ui/segment-builder.md) de Real-Time CDP más tarde.
* Los segmentos que tienen reglas que se pueden admitir, pero que pueden contener datos que no estarán disponibles en Real-Time CDP.
* Segmentos que no se pueden crear en Real-time CDP y a los que les falta funcionalidad.

>[!TIP]
>
>Adobe Real-Time CDP ofrece [tres tipos de evaluación de segmentos](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Lote], [!UICONTROL Streaming], y [!UICONTROL Edge]. Los clientes que utilizan segmentos en tiempo real en Audience Manager pueden verse restringidos por la limitación actual de 500 segmentos de streaming en Real-Time CDP. Más información acerca de las [protecciones de segmentación](/help/profile/guardrails.md).

## 2. ¿Qué segmentos son críticos para enviarse a través del [!UICONTROL conector de origen de Audience Manager]?

En función de sus criterios de evaluación, los segmentos sin dependencias de datos, sin desafíos de destino o activación y sus reglas de segmentación que se pueden crear a través de la recopilación de datos de Real-Time CDP como [SDK web de Adobe Experience Platform](/help/edge/web-sdk-faq.md) en una fecha posterior, se deben enviar a través del conector de origen de Audience Manager.

## 3. ¿Utilizará el destino [!UICONTROL Públicos de Experience Cloud] para devolver los datos a Audience Manager?

Los segmentos que tienen reglas compatibles con Real-Time CDP, pero con dependencias de activación para Audience Manager, pueden enviarse a Audience Manager mediante la tarjeta de destino [Públicos de Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## 4. ¿Qué destinos tiene en Audience Manager hoy en día para poder empezar a migrar a Real-Time CDP?

Adobe recomienda encarecidamente que los segmentos activados en Audience Manager para [destinos basados en personas](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es) se inserten en Real-Time CDP a través del [!UICONTROL Conector de origen de Audience Manager], para luego activarse a través de Real-Time CDP.

Todos los destinos basados en personas disponibles en Audience Manager, [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Coincidencia de clientes de Google]](/help/destinations/catalog/advertising/google-customer-match.md) y [LinkedIn](/help/destinations/catalog/social/linkedin.md), también están disponibles en Real-Time CDP.

Socios adicionales de estrategia de medios y datos de origen como [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) y [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) están disponibles.

Real-Time CDP admite actualmente más de 60 destinos de forma nativa en [catálogo](/help/destinations/catalog/overview.md), más de 20 de los cuales son destinos publicitarios o sociales que admiten la coincidencia de públicos de origen.

## Pasos siguientes

Después de leer esta página, ahora tiene que tener en cuenta un primer conjunto de consideraciones a medida que inicia su evolución de Audience Manager a Real-Time CDP.
