---
title: Activación expandida de Audience Manager
description: Aprenda a activar audiencias de Audience Manager en destinos sociales y publicitarios mediante la activación expandida de Audience Manager.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Activación expandida de Audience Manager

La activación expandida de Audience Manager, creada en Adobe Experience Platform, ayuda a los sistemas existentes [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) los usuarios activan sus audiencias en [social](../destinations/catalog/social/overview.md) y [publicidad](../destinations/catalog/advertising/overview.md) plataformas de destino de Real-Time CDP, como [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md), y más.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] solo está disponible para los [!DNL Audience Manager] usuarios.

## Terminología {#terminology}

La activación expandida de Audience Manager utiliza conceptos y componentes de Adobe Experience Platform. Para comprender mejor el flujo de trabajo de activación expandida y los componentes que va a utilizar, asegúrese de tener una comprensión básica de los siguientes conceptos:

* [Audiencias](../segmentation/ui/overview.md): las audiencias son conjuntos de personas que comparten comportamientos o características similares. Adobe Experience Platform puede generar esta colección de personas mediante las definiciones de segmentos o la composición de audiencias (audiencia generada por Platform), o a partir de fuentes externas como cargas personalizadas (audiencia generada externamente). En la Activación expandida, los segmentos (audiencias) del Audience Manager se importan como [cargas personalizadas](../segmentation/ui/overview.md#import-audience).
* [Conectores de origen](../sources/home.md): los conectores de origen (también conocidos como fuentes) ayudan a los usuarios de Experience Platform a ingerir fácilmente datos de varias fuentes, lo que permite estructurar, etiquetar y mejorar los datos mediante servicios de Experience Platform. Los datos se pueden ingerir desde una variedad de fuentes, como almacenamiento basado en la nube, software de terceros y sistemas CRM.
* [Conectores de destino](../destinations/home.md): los destinos describen cualquier punto final, como una aplicación de Adobe, una plataforma de publicidad, un servicio de almacenamiento en la nube o un servicio de marketing, en el que se activa y se entrega una audiencia. [!DNL Expanded Activation] admite la activación de audiencias en [publicidad](../destinations/catalog/advertising/overview.md) y [social](../destinations/catalog/social/overview.md) conectores de destino.

## Requisitos previos {#prerequisites}

Antes de activar audiencias mediante la activación expandida, asegúrese de cumplir los requisitos previos que se describen a continuación.

### Requisitos de usuario y función {#permission-requirements}

Antes de usar [!DNL Expanded Activation], debe crear una cuenta de usuario desde el Admin Console y asignarla al [!DNL Expanded Activation] función. Consulte la [administración](administration.md) para obtener instrucciones detalladas sobre cómo hacerlo.

### Requisitos de audiencia {#audience-requirements}

Para activar audiencias mediante [!DNL Expanded Activation], asegúrese de que las audiencias de Audience Manager se basen en **direcciones de correo electrónico con hash**. Existen dos maneras de garantizar esto, en función del uso que haga su Audience Manager:

* Si utiliza el complemento [Audience Manager People-Based Destinations](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) funcionalidad, entonces ya está introduciendo direcciones de correo electrónico con hash en Audience Manager. No hay ningún paso adicional que necesite realizar en este caso. Puede saltar a [activación de audiencias mediante la activación expandida](activate-audiences.md).
* Si es usted _no_ uso del [Audience Manager People-Based Destinations](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) funcionalidad, debe crear una nueva fuente de datos en Audience Manager y utilizarla para almacenar direcciones de correo electrónico con hash. Consulte la documentación sobre [configuración de una fuente de datos para flujos de trabajo de correo electrónico con hash](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) para aprender a hacer esto. Después de haber introducido direcciones de correo electrónico con hash en la fuente de datos de Audience Manager, lea la documentación sobre [activación de audiencias mediante la activación expandida](activate-audiences.md).

## Pasos siguientes {#next-steps}

Ahora que comprende mejor los casos de uso y las ventajas de utilizar [!DNL Expanded Activation], inicio [configuración de la cuenta](administration.md) y luego [activar las audiencias](activate-audiences.md).

