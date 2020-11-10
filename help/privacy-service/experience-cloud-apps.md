---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aplicaciones de Privacy Service y Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 4cd7b9d3ca542c2fba83d066197b92775c053729
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 22%

---


# [!DNL Privacy Service] y [!DNL Experience Cloud] aplicaciones

Adobe Experience Platform [!DNL Privacy Service] está diseñado para admitir solicitudes de privacidad para varias aplicaciones de Adobe Experience Cloud. Cada aplicación admite diferentes valores de producto e ID para identificar los sujetos de datos.

Este documento sirve como referencia para la documentación de [!DNL Experience Cloud] la aplicación que describe cómo configurar esa aplicación para operaciones relacionadas con la privacidad. Esto incluye cómo formatear y etiquetar los datos. Se cubren dos categorías de solicitudes:

* [Aplicaciones integradas con Privacy Service](#integrated): Aplicaciones que pueden enviar solicitudes de acceso, eliminación o exclusión a [!DNL Privacy Service].
* [Aplicaciones](#self-serve)de autoservicio: Aplicaciones que deben administrar sus solicitudes de privacidad internamente y no pueden comunicarse [!DNL Privacy Service] directamente.

Revise la documentación de sus [!DNL Experience Cloud] aplicaciones para aprender a dar formato a sus solicitudes de privacidad y los valores que se admiten para dichas solicitudes.

## Aplicaciones integradas con [!DNL Privacy Service] {#integrated}

A continuación se muestra una lista de [!DNL Experience Cloud] aplicaciones que están integradas con [!DNL Privacy Service], incluidas las [!DNL Privacy Service] capacidades con las que son compatibles y los vínculos a la documentación para obtener más información.

| de asistencia al cliente | Acceso/eliminación | Exclusión de la venta | Documentación y consideraciones |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Acceder/eliminar documentación del RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Acceder/eliminar documentación de CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentación de exclusión para CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] gestiona las solicitudes de exclusión mediante variables de sistema de informes de [privacidad](https://docs.adobe.com/content/help/es-ES/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/es-ES/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentación de exclusión](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Acceder o eliminar documentación](https://helpx.adobe.com/es/campaign/kb/campaign-privacy.html)</li><li>[Documentación de exclusión](../segmentation/honoring-opt-outs.md)</li></ul> |
| Atributos del cliente de Adobe (CRS) | ✓ | N/D | <ul><li>[Acceder/eliminar documentación del RGPD](https://docs.adobe.com/content/help/es-ES/core-services/interface/customer-attributes/gdpr.html)</li><li>[Acceder/eliminar documentación de CCPA](https://docs.adobe.com/content/help/es-ES/core-services/interface/customer-attributes/ccpa.html)</li><li>Los atributos del cliente no tienen la capacidad de transferir datos, por lo que las solicitudes de exclusión no se aplican.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Acceder/eliminar documentación para el lago de datos](../catalog/privacy.md)</li><li>[Acceso y eliminación de la documentación para el Perfil del cliente en tiempo real](../profile/privacy.md)</li><li>[!DNL Experience Platform] honra las solicitudes de [exclusión para los segmentos](../segmentation/honoring-opt-outs.md)de audiencia.</li></ul> |
| Autenticación de Adobe Primetime | ✓ | N/D | <ul><li>[Acceder o eliminar documentación](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] no tiene la capacidad de transferir datos, por lo tanto las solicitudes de exclusión no se aplican.</li></ul> |
| Adobe Target | ✓ | N/D | <ul><li>[Acceder o eliminar documentación](https://docs.adobe.com/content/help/es-ES/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] no tiene la capacidad de transferir datos, por lo tanto las solicitudes de exclusión no se aplican.</li></ul> |


## Aplicaciones de autoservicio {#self-serve}

A continuación se muestra una lista de [!DNL Experience Cloud] aplicaciones que no están integradas [!DNL Privacy Service] y deben gestionar internamente sus problemas de privacidad. Se proporcionan vínculos a la documentación de cada aplicación, junto con descripciones del contenido de la documentación.

| de asistencia al cliente | Descripción de la documentación |
| ------- | ----------- |
| [Adobe Campaign Classic](https://helpx.adobe.com/es/campaign/kb/campaign-privacy.html) | Información general sobre las funcionalidades del RGPD para Adobe Campaign Classic. |
| [Administrador dinámico de etiquetas de Adobe](https://docs.adobe.com/content/help/es-ES/dtm/using/tools/opt-in.html) | Pasos para evitar que las etiquetas de Adobe se activen hasta que se obtenga el consentimiento. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Información general sobre cómo un administrador de privacidad del cliente o AEM administrador puede gestionar solicitudes de RGPD. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Pasos para hacer acceso al RGPD y eliminar solicitudes mediante Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Cómo los desarrolladores pueden usar las extensiones y el creador de reglas para definir las soluciones de inclusión y de exclusión. |
