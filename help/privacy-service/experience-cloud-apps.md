---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servicios de privacidad y aplicaciones de Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: f4a007b66806cb0d322226e1e1837cfce7ca4095
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 16%

---


# Servicios de privacidad y aplicaciones de Experience Cloud

El servicio de privacidad de Adobe Experience Platform está diseñado para admitir solicitudes de privacidad de varias aplicaciones de Adobe Experience Cloud. Cada aplicación admite diferentes valores de producto e ID para identificar los sujetos de datos.

Este documento sirve como referencia para la documentación de la aplicación de Experience Cloud que describe cómo configurar esa aplicación para operaciones relacionadas con la privacidad. Esto incluye cómo formatear y etiquetar los datos. Se cubren dos categorías de solicitudes:

* [Aplicaciones integradas con Privacy Service](#integrated): Aplicaciones que pueden enviar solicitudes de acceso, eliminación o exclusión a Privacy Service.
* [Aplicaciones](#self-serve)de autoservicio: Aplicaciones que deben administrar sus solicitudes de privacidad internamente y no pueden comunicarse directamente con Privacy Service.

Revise la documentación de sus aplicaciones de Experience Cloud para obtener información sobre cómo dar formato a sus solicitudes de privacidad y qué valores se admiten para dichas solicitudes.

## Aplicaciones integradas con Privacy Service {#integrated}

A continuación se muestra una lista de las aplicaciones de Experience Cloud que están integradas con Privacy Service, incluidas las funciones de Privacy Service con las que son compatibles y los vínculos a la documentación para obtener más información.

| Aplicación | Acceso/eliminación | Exclusión de la venta | Documentación y consideraciones |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Advertising Cloud aprovecha las capacidades de exclusión global existentes que ofrece Adobe Privacy Center. Consulte la guía para [realizar solicitudes](https://docs.adobe.com/content/help/es-ES/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) de privacidad de datos para obtener más información.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>Analytics gestiona las solicitudes de exclusión mediante variables de sistema de informes de [privacidad](https://docs.adobe.com/content/help/es-ES/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/es-ES/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentación de exclusión](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Documentación de exclusión](../segmentation/honoring-opt-outs.md)</li></ul> |
| Atributos del cliente de Adobe (CRS) | ✓ | N/D | <ul><li>[Acceder/eliminar documentación del RGPD](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/gdpr.html)</li><li>[Acceder/eliminar documentación de CCPA](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/ccpa.html)</li><li>Los atributos del cliente no tienen la capacidad de transferir datos, por lo que las solicitudes de exclusión no se aplican.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Acceder/eliminar documentación para el lago de datos](../catalog/privacy.md)</li><li>[Acceso y eliminación de la documentación para el Perfil del cliente en tiempo real](../profile/privacy.md)</li><li>La plataforma de experiencia respeta las solicitudes de [exclusión para los segmentos](../segmentation/honoring-opt-outs.md)de audiencia.</li></ul> |
| Autenticación de Adobe Primetime | ✓ | N/D | <ul><li>[Acceder o eliminar documentación](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime no tiene la capacidad de transferir datos, por lo tanto las solicitudes de exclusión no se aplican.</li></ul> |
| Adobe Target | ✓ | N/D | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/es-ES/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.translate.html)</li><li>Destinatario no tiene la capacidad de transferir datos, por lo tanto las solicitudes de exclusión no se aplican.</li></ul> |


## Aplicaciones de autoservicio {#self-serve}

A continuación se muestra una lista de aplicaciones de Experience Cloud que no están integradas con Privacy Service y deben gestionar internamente sus problemas de privacidad. Se proporcionan vínculos a la documentación de cada aplicación, junto con descripciones del contenido de la documentación.

| Aplicación | Descripción de la documentación |
| ------- | ----------- |
| [Adobe Campaign Classic](https://helpx.adobe.com/es/campaign/kb/campaign-privacy.html) | Información general sobre las funcionalidades de RGPD para Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/en/dtm/using/tools/opt-in.html) | Pasos para evitar que las etiquetas de Adobe se activen hasta que se obtenga el consentimiento. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Información general sobre cómo un administrador de privacidad del cliente o un administrador de AEM pueden gestionar solicitudes GDPR. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Pasos para hacer acceso al RGPD y eliminar solicitudes mediante Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Cómo los desarrolladores pueden usar las extensiones y el creador de reglas para definir las soluciones de inclusión y de exclusión. |
