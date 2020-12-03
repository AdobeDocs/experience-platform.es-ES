---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: Información general sobre los destinos
seo-title: Información general sobre los destinos
description: Active los datos de Platform en destinos para campañas de marketing entre canales, correos electrónicos, publicidad segmentada y mucho más.
seo-description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos desde la plataforma de datos del cliente en tiempo real. Puede utilizar Destinos en la plataforma de datos del cliente en tiempo real para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---


# [!DNL Destinations]sobre validación{#overview}

![Pancarta de información general sobre destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos desde la plataforma de datos del cliente en tiempo real. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.

## Destinos y fuentes {#destinations-and-sources}

Una de las funcionalidades principales de CDP en tiempo real es la ingesta de sus datos de origen y su activación para sus necesidades comerciales. Utilice fuentes para ingerir datos en CDP en tiempo real y destinos para exportar datos desde CDP en tiempo real.

## Pasos de destino {#steps}

* Elija entre un catálogo [de](./catalog/overview.md) autoservicio de todos los destinos disponibles en CDP en tiempo real.
* Utilice **[!UICONTROL Destinos]** para [activar](./ui/activate-destinations.md) y enviar perfiles o segmentos a plataformas de automatización de marketing, plataformas de publicidad digital, etc.
* Programe las exportaciones de datos a sus destinos preferidos en horas normales.

## Controles {#controls}

Los controles del espacio de trabajo [Destinos](./ui/destinations-workspace.md) permiten:

* Examinar el catálogo de plataformas de destino en el que puede activar los datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Cree una cuenta en una ubicación de almacenamiento o vincule CDP en tiempo real con la cuenta de la plataforma de destino;
* Seleccione qué segmentos deben activarse en los destinos;
* Seleccione los campos [del Modelo de datos de](../xdm/home.md) experiencia (XDM) que desea exportar al activar segmentos en destinos de marketing por correo electrónico.

## Destination types and categories {#types-and-categories}

Para obtener información detallada, consulte la descripción general [de tipos de](./destination-types.md)destino y categorías.

## Destinos y Controles de acceso {#access-controls}

La funcionalidad de destinos de CDP en tiempo real funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede realizar vistas, administrar y activar destinos. Para obtener información sobre los permisos individuales, consulte [Control de acceso en Adobe Experience Platform](../access-control/home.md) y desplácese hacia abajo hasta la parte inferior de la página.

Para obtener más información sobre controles de acceso, consulte la guía del usuario de [Control de acceso](../access-control/ui/overview.md).

## [!DNL Data Governance] restricciones para activar datos en destinos {#data-governance}

La administración de datos se impone para los destinos CDP en tiempo real mediante:

* *Casos* de uso de marketing que puede seleccionar en el flujo de trabajo de creación de destinos;
* *Directivas* de uso de datos que restringen la activación de datos que contienen ciertas etiquetas de uso en destinos con determinados casos de uso de mercadotecnia.

Consulte la [!DNL Data Governance] documentación de CDP en tiempo real para obtener más información sobre casos [de uso de](../rtcdp/privacy/data-governance-overview.md#destinations) mercadotecnia y [resolver violaciones](../rtcdp/privacy/data-governance-overview.md#enforcement)de políticas de datos.

Para obtener más información sobre la selección de casos de uso de mercadotecnia en el flujo de trabajo de creación de destino, consulte las páginas siguientes para los distintos tipos de destino en CDP en tiempo real:

* [Destinos publicitarios - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinos publicitarios - Publicidades de Google](./catalog/advertising/google-ads-destination.md)
* [Destinos publicitarios - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinos de almacenamiento de nube](./catalog/cloud-storage/workflow.md)
* [Destinos de mercadotecnia de correo electrónico](./catalog/email-marketing/overview.md)
* [Destinos de redes sociales](./catalog/social/workflow.md)

Para obtener más información sobre las infracciones de la directiva de datos en el flujo de trabajo de activación de segmentos, consulte el paso Revisar en [Activar perfiles y segmentos a un destino](./ui/activate-destinations.md#review).