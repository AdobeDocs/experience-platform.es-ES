---
title: Privacidad en el Perfil de datos del cliente en tiempo real
seo-title: Privacidad en el Perfil de datos del cliente en tiempo real
description: El Perfil de datos de clientes en tiempo real le permite optimizar el proceso para mantener las operaciones de datos conformes con las normativas de privacidad.
seo-description: El Perfil de datos de clientes en tiempo real le permite optimizar el proceso para mantener las operaciones de datos conformes con las normativas de privacidad.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Privacidad en tiempo real CDP

[!DNL Real-time Customer Data Platform] (CDP en tiempo real) ayuda a los especialistas en mercadotecnia a reunir datos de varios sistemas empresariales, permitiéndoles identificar, comprender y captar mejor a sus clientes. Adobe mantiene la privacidad de los datos del consumidor como un principio de diseño fundamental y proporciona varios controles para ayudar a los especialistas en marketing a administrar la privacidad de los datos de sus clientes.

La mayoría de las funcionalidades de CDP en tiempo real están impulsadas por el Adobe Experience Platform. Este documento proporciona información sobre las distintas tecnologías de mejora de la privacidad admitidas por CDP en tiempo real, con vínculos a la documentación para obtener más información [!DNL Experience Platform] .

## [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] le permite agilizar el proceso para mantener sus operaciones de datos en conformidad con las normas de privacidad, como el [!DNL General Data Protection Regulation] (RGPD) y el [!DNL California Consumer Privacy Act] (CPA). Dado que CDP en tiempo real aprovecha [!DNL Experience Platform] las capacidades de recopilación y almacenamiento de datos, las solicitudes de acceso y eliminación para RGPD y CPA deben administrarse dentro de [!DNL Platform]. Consulte el documento de información general [del](../../privacy-service/home.md) Privacy Service para obtener una introducción más detallada del servicio.

Existen dos métodos para enviar solicitudes individuales de datos del RGPD y la CPA para acceder y eliminar datos de clientes:

* Utilice [!DNL Privacy Service UI](https://gdprui.cloud.adobe.io/) para crear y supervisar solicitudes de acceso y eliminación dentro de un espacio de trabajo visual. Consulte el tutorial [de la interfaz de usuario del](../../privacy-service/ui/overview.md) Privacy Service para obtener instrucciones paso a paso.
* Utilice el [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) para administrar las solicitudes de acceso y eliminación con llamadas de API RESTful. Consulte el tutorial [de API de](../../privacy-service/api/getting-started.md) Privacy Service para obtener instrucciones paso a paso.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Pasos siguientes

Este documento proporcionó una breve introducción a las capacidades de privacidad de CDP en tiempo real. Para obtener información más detallada sobre las prácticas recomendadas y los pasos para enviar solicitudes de acceso o eliminación, consulte la documentación [del](../../privacy-service/home.md)Privacy Service.