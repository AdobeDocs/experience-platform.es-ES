---
keywords: destinos;plataforma de experiencia de adobe;plataforma;destinos información general;activar datos;activar;
title: Información general sobre los destinos
seo-title: Información general sobre los destinos
description: Obtenga información sobre cómo activar datos de Adobe Experience Platform en destinos para campañas de marketing entre canales, correos electrónicos, publicidad de destino y mucho más.
seo-description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos de Adobe Experience Platform. Puede utilizar Destinos en Adobe Experience Platform para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.
translation-type: tm+mt
source-git-commit: 2efdefc69c937c70f6a463113a73ca71d8998e14
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---


# Información general del [!DNL Destinations]{#overview}

![Pancarta de información general sobre destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.

## Destinos y fuentes {#destinations-and-sources}

Una de las funcionalidades principales de Platform es la ingesta de sus datos de origen y su activación para las necesidades de su negocio. Utilice [orígenes](../sources/home.md) para ingerir datos en la plataforma y destinos para exportar datos desde la plataforma.

## Pasos de destinos {#steps}

* Elija entre un [catálogo de autoservicio](./catalog/overview.md) de todos los destinos disponibles en Platform.
* Use destinos para [activar](./ui/activate-destinations.md) y enviar perfiles o segmentos a plataformas de automatización de mercadotecnia, plataformas de publicidad digital, etc.
* Programe las exportaciones de datos a sus destinos preferidos en horas normales.

## Controles {#controls}

Los controles del [espacio de trabajo Destinations](./ui/destinations-workspace.md) le permiten:

* Examinar el catálogo de plataformas de destino en el que puede activar los datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Cree una cuenta en una ubicación de almacenamiento o vincule Plataforma a la cuenta en la plataforma de destino;
* Seleccione qué segmentos deben activarse en los destinos;
* Seleccione los campos [Modelo de datos de experiencia (XDM)](../xdm/home.md) que desea exportar al activar segmentos en destinos de marketing por correo electrónico.

## Tipos y categorías de destino {#types-and-categories}

Para obtener información detallada, consulte la [información general sobre tipos de destino y categorías](./destination-types.md).

## Destinos y controles de acceso {#access-controls}

La funcionalidad de destinos de Platform funciona con los permisos de Adobe Experience Platform control de acceso. Según el nivel de permiso del usuario, puede realizar vistas, administrar y activar destinos. Para obtener información sobre los permisos individuales, consulte [Control de acceso en Adobe Experience Platform](../access-control/home.md) y desplácese hacia abajo hasta la parte inferior de la página.

Para obtener más información sobre controles de acceso, consulte la [guía del usuario de Control de acceso](../access-control/ui/overview.md).

## [!DNL Data Governance] restricciones para activar datos en destinos  {#data-governance}

La gobernanza de los datos se aplica a los destinos de plataforma mediante:

* *Casos* de uso de marketing que puede seleccionar en el flujo de trabajo de creación de destinos;
* *Las* directivas de uso de datos que restringen la activación de datos que contienen determinadas etiquetas de uso en destinos con determinados casos de uso de mercadotecnia.

Consulte [!DNL Data Governance] en la documentación de la Plataforma para obtener más información sobre [casos de uso de mercadotecnia](../data-governance/policies/overview.md) y [resolución de violaciones de políticas de datos](../data-governance/enforcement/auto-enforcement.md).

Para obtener más información sobre la selección de casos de uso de mercadotecnia en el flujo de trabajo de creación de destino, consulte las páginas siguientes para los distintos tipos de destino en Plataforma:

* [Destinos publicitarios - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Destinos publicitarios - Publicidades de Google](./catalog/advertising/google-ads-destination.md)
* [Destinos publicitarios - Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [Destinos de almacenamiento de nube](./catalog/cloud-storage/workflow.md)
* [Destinos de mercadotecnia de correo electrónico](./catalog/email-marketing/overview.md)
* [Destinos de redes sociales](./catalog/social/workflow.md)

Para obtener más información sobre las infracciones de directivas de datos en el flujo de trabajo de activación de segmentos, consulte el paso Revisión de [Activar perfiles y segmentos a un destino](./ui/activate-destinations.md#review).