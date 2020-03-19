---
title: Privacidad en el perfil de datos del cliente en tiempo real
seo-title: Privacidad en el perfil de datos del cliente en tiempo real
description: El perfil de datos del cliente en tiempo real le permite optimizar el proceso para mantener las operaciones de datos conformes con las normativas de privacidad.
seo-description: El perfil de datos del cliente en tiempo real le permite optimizar el proceso para mantener las operaciones de datos conformes con las normativas de privacidad.
translation-type: tm+mt
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Privacidad en tiempo real CDP

La plataforma de datos del cliente en tiempo real (CDP en tiempo real) ayuda a los especialistas en marketing a reunir los datos de varios sistemas empresariales, permitiéndoles identificar, comprender y captar mejor a sus clientes. Adobe mantiene la privacidad de los datos del consumidor como un principio de diseño fundamental y proporciona varios controles para ayudar a los especialistas en marketing a administrar la privacidad de los datos de sus clientes.

La mayoría de las funciones de CDP en tiempo real son ofrecidas por Adobe Experience Platform. Este documento proporciona información sobre las distintas tecnologías de mejora de la privacidad admitidas por CDP en tiempo real, con vínculos a la documentación de la plataforma de experiencia para obtener más información.

## Privacy Service

Adobe Experience Platform Privacy Service le permite agilizar el proceso de mantener las operaciones de datos conformes con las normativas de privacidad, como el Reglamento General de Protección de Datos (RGPD) y la Ley de Protección de los Consumidores de California (CCPA). Dado que CDP en tiempo real aprovecha las capacidades de la Plataforma de experiencia para la recopilación y almacenamiento de datos, las solicitudes de acceso y eliminación para el RGPD y CCPA deben administrarse dentro de la Plataforma. Consulte el documento de información general [de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) Privacy Service para obtener una introducción más detallada del servicio.

Existen dos métodos para enviar solicitudes individuales de datos del RGPD y la CPA para acceder y eliminar datos de clientes:

* Utilice la interfaz de usuario [de](https://gdprui.cloud.adobe.io/) Privacy Service para crear y supervisar solicitudes de acceso y eliminación en un espacio de trabajo visual. Consulte el tutorial [de la interfaz de usuario de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) Privacy Service para obtener instrucciones paso a paso.
* Utilice la API [de](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) Privacy Service para administrar las solicitudes de acceso y eliminación con las llamadas de RESTful API. Consulte el tutorial [de API de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md) Privacy Service para obtener instrucciones paso a paso.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Pasos siguientes

Este documento proporciona una breve introducción a las capacidades de privacidad de CDP en tiempo real. Para obtener información más detallada sobre las prácticas recomendadas y los pasos para enviar solicitudes de acceso o eliminación, consulte la documentación [de](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html)Privacy Service.