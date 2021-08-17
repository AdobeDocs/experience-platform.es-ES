---
keywords: destinos;adobe experience platform;platform;información general sobre destinos;activar datos;activar;
title: Información general sobre los destinos
seo-title: Información general sobre los destinos
description: Obtenga información sobre cómo activar datos de Adobe Experience Platform en destinos para campañas de marketing en canales múltiples, correos electrónicos, publicidad segmentada y mucho más.
seo-description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos desde Adobe Experience Platform. Puede usar Destinos en Adobe Experience Platform para activar los datos conocidos y desconocidos para campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: b7392596c7ed96032dc8ad6bb8e423640f562394
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Información general del [!DNL Destinations] {#overview}

![Banner de información general sobre destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

## Destinos y fuentes {#destinations-and-sources}

Una de las funcionalidades principales de Platform es la ingesta de sus datos de origen y su activación para sus necesidades comerciales. Utilice [sources](../sources/home.md) para introducir datos en Platform y destinos para exportar datos desde Platform.

## Pasos de destinos {#steps}

* Elija entre un [catálogo de autoservicio](./catalog/overview.md) de todos los destinos disponibles en Platform.
* Utilice destinos para y envíe perfiles o segmentos a plataformas de automatización de marketing, plataformas de publicidad digital y mucho más.
* Programe exportaciones de datos a sus destinos preferidos en ocasiones regulares.

## Controles {#controls}

Los controles del [Espacio de trabajo Destinations](./ui/destinations-workspace.md) le permiten:

* Examine el catálogo de plataformas de destino donde puede activar los datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Cree una cuenta en una ubicación de almacenamiento o vincule Platform a la cuenta en la plataforma de destino;
* Seleccione qué segmentos deben activarse en los destinos;
* Seleccione los campos [Experience Data Model (XDM)](../xdm/home.md) que desea exportar al activar segmentos en destinos de marketing por correo electrónico.

## Tipos y categorías de destino {#types-and-categories}

Para obtener información detallada, consulte [información general sobre tipos de destino y categorías](./destination-types.md).

## Destinos y controles de acceso {#access-controls}

La funcionalidad de destinos de Platform funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede ver, administrar y activar destinos. Para obtener información sobre los permisos individuales, consulte [Control de acceso en Adobe Experience Platform](../access-control/home.md) y desplácese hacia abajo hasta la parte inferior de la página.

Para obtener más información sobre los controles de acceso, consulte la [Guía del usuario del control de acceso](../access-control/ui/overview.md).

## [!DNL Data Governance] restricciones sobre la activación de datos en destinos {#data-governance}

El control de datos se aplica a los destinos de Platform mediante:

* *Acciones de marketing* que puede seleccionar en el flujo de trabajo crear destinos .
* *Políticas de uso de* datos que restringen la activación de datos que contienen determinadas etiquetas de uso en destinos con determinadas acciones de marketing.

Consulte [!DNL Data Governance] en la documentación de Platform para obtener más información sobre [acciones de marketing](../data-governance/policies/overview.md) y [resolución de violaciones de políticas de datos](../data-governance/enforcement/auto-enforcement.md).

Para obtener más información sobre la selección de acciones de marketing en el flujo de trabajo crear destino , consulte las siguientes páginas para los distintos tipos de destino en Platform:

* [Destinos publicitarios: Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinos publicitarios - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinos publicitarios - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinos de almacenamiento en la nube](./catalog/cloud-storage/overview.md)
* [Destinos de marketing por correo electrónico](./catalog/email-marketing/overview.md)
* [Destinos sociales](./catalog/social/overview.md)

Para obtener más información sobre las violaciones de políticas de datos en el flujo de trabajo de activación de segmentos, consulte el paso Revisar en las siguientes guías:

* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](./ui/activate-segment-streaming-destinations.md#review)
* [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](./ui/activate-streaming-profile-destinations.md#review)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](./ui/activate-batch-profile-destinations.md#review)
