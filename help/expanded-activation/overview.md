---
title: Activación ampliada de Audience Manager
description: Aprenda a activar audiencias de Audience Manager en destinos sociales y publicitarios mediante la activación expandida de Audience Manager.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Activación ampliada de Audience Manager

La activación expandida de Audience Manager, creada en Adobe Experience Platform, ayuda a los usuarios de [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) existentes a activar sus audiencias en las plataformas de destino [social](../destinations/catalog/social/overview.md) y [publicidad](../destinations/catalog/advertising/overview.md) de Real-Time CDP, como [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md) y más.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] solo está disponible para los usuarios de [!DNL Audience Manager] existentes.

## Terminología {#terminology}

La activación expandida de Audience Manager utiliza conceptos y componentes de Adobe Experience Platform. Para comprender mejor el flujo de trabajo de activación expandida y los componentes que va a utilizar, asegúrese de tener una comprensión básica de los siguientes conceptos:

* [Audiencias](../segmentation/ui/overview.md): las audiencias son conjuntos de personas que comparten comportamientos o características similares. Adobe Experience Platform puede generar esta colección de personas mediante las definiciones de segmentos o la composición de audiencias (audiencia generada por Platform), o a partir de fuentes externas como cargas personalizadas (audiencia generada externamente). En la activación expandida, los segmentos (audiencias) del Audience Manager se importan como [cargas personalizadas](../segmentation/ui/audience-portal.md#import-audience).
* [Conectores de Source](../sources/home.md): los conectores de Source (también conocidos como fuentes) ayudan a los usuarios de Experience Platform a ingerir fácilmente datos de múltiples fuentes, lo que permite estructurar, etiquetar y mejorar los datos mediante los servicios de Experience Platform. Los datos se pueden ingerir desde una variedad de fuentes, como almacenamiento basado en la nube, software de terceros y sistemas CRM.
* [Conectores de destino](../destinations/home.md): Los destinos describen cualquier extremo, como una aplicación de Adobe, una plataforma de publicidad, un servicio de almacenamiento en la nube o un servicio de marketing, en el que se activa y se entrega una audiencia. [!DNL Expanded Activation] admite la activación de audiencias en los conectores de destino [advertising](../destinations/catalog/advertising/overview.md) y [social](../destinations/catalog/social/overview.md).

## Requisitos previos {#prerequisites}

Antes de activar audiencias mediante la activación expandida, asegúrese de cumplir los requisitos previos que se describen a continuación.

### Requisitos de usuario y función {#permission-requirements}

Para poder usar [!DNL Expanded Activation], debe crear una cuenta de usuario desde el Admin Console y asignarla al rol [!DNL Expanded Activation]. Consulte la página [administración](administration.md) para obtener instrucciones detalladas sobre cómo hacerlo.

### Requisitos de audiencia {#audience-requirements}

Para activar audiencias a través de [!DNL Expanded Activation], asegúrese de que las audiencias del Audience Manager estén basadas en **direcciones de correo electrónico con hash**. Existen dos maneras de garantizar esto, en función del uso que haga su Audience Manager:

* Si usa la funcionalidad [Destinos basados en personas de Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), ya está introduciendo direcciones de correo electrónico con hash en Audience Manager. No hay ningún paso adicional que necesite realizar en este caso. Puede saltar a [activar audiencias mediante la activación expandida](activate-audiences.md).
* Si _no_ usa la funcionalidad [Destinos basados en personas de Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), debe crear un nuevo origen de datos en Audience Manager y utilizarlo para almacenar direcciones de correo electrónico con hash. Consulte la documentación sobre [configuración de una fuente de datos para flujos de trabajo de correo electrónico con hash](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) para saber cómo hacerlo. Después de haber ingerido direcciones de correo electrónico con hash en la fuente de datos del Audience Manager, lea la documentación sobre [activación de audiencias mediante la activación expandida](activate-audiences.md).

## Pasos siguientes {#next-steps}

Ahora que comprende mejor los casos de uso y las ventajas de usar [!DNL Expanded Activation], comience a [configurar su cuenta](administration.md) y, a continuación, [active sus audiencias](activate-audiences.md).
