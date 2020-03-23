---
title: Descripción general de destinos
seo-title: Descripción general de destinos
description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación sin problemas de datos desde la plataforma de datos del cliente en tiempo real. Puede utilizar los destinos en la plataforma de datos del cliente en tiempo real de Adobe para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas de correo electrónico, publicidad de objetivo y muchos otros casos de uso.
seo-description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación sin problemas de datos desde la plataforma de datos del cliente en tiempo real. Puede utilizar los destinos en la plataforma de datos del cliente en tiempo real de Adobe para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas de correo electrónico, publicidad de objetivo y muchos otros casos de uso.
translation-type: tm+mt
source-git-commit: b4b02913467c43d004574a1aa5cb2f793964ad1e

---


# Descripción general de destinos

**Los destinos** son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos desde la plataforma de datos del cliente en tiempo real. Puede utilizar **Destinos** para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas de correo electrónico, publicidad de objetivo y muchos otros casos de uso.

## Destinos y fuentes

Una de las funcionalidades principales de CDP en tiempo real es la ingesta de sus datos de origen y su activación para sus necesidades comerciales. Se utiliza **[!UICONTROL Sources]** para transferir datos a CDP en tiempo real y **[!UICONTROL Destinations]** para exportar datos desde CDP en tiempo real.

## Pasos de destino

* Utilícelo **[!UICONTROL Destinations]** para [activar](/help/rtcdp/destinations/activate-destinations.md) y enviar perfiles o segmentos a plataformas de automatización de marketing, plataformas de publicidad digital y mucho más.
* Elija entre un catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) autoservicio de todos los destinos disponibles en CDP en tiempo real.
* Programe las exportaciones de datos a sus destinos preferidos en horas normales.

## Controles

Los controles del espacio de trabajo [Destinos](/help/rtcdp/destinations/destinations-workspace.md) permiten:

* Examinar el catálogo de plataformas de destino en el que puede activar los datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Cree una cuenta en una ubicación de almacenamiento o vincule CDP en tiempo real con la cuenta en la plataforma de destino;
* Seleccione los segmentos que se deben activar en los destinos;
* Seleccione los campos [del Modelo de datos de](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/xdm_system/xdm_system_in_experience_platform.md) experiencia (XDM) que desea exportar al activar segmentos en destinos de marketing por correo electrónico.

## Tipos y categorías de destino: información general de vídeo

En CDP en tiempo real de Adobe, existen dos tipos de destinos: destinos de exportación de perfiles y destinos de exportación de segmentos. El siguiente vídeo describe los dos tipos de destinos.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Destinos de exportación de perfiles

Los destinos de exportación de perfiles generan un archivo que contiene perfiles o atributos. Estos destinos utilizan datos sin procesar, a menudo con la dirección de correo electrónico como clave principal.

### Destinos de exportación de segmentos

Los destinos de exportación de segmentos envían los perfiles y los segmentos para los que cumplen los requisitos. Estos destinos utilizan ID de segmento o ID de usuario.

### Categorías de destino

Los destinos del catálogo [](/help/rtcdp/destinations/destinations-catalog.md) Destinations se agrupan por categoría de destino (**Publicidad**, almacenamiento **en** nube o marketing **por** correo electrónico). Para obtener más información sobre cada uno de ellos, consulte el catálogo [Destinations](/help/rtcdp/destinations/destinations-catalog.md).

## Destinos y controles de acceso

La **[!UICONTROL Destinations]** funcionalidad de CDP en tiempo real funciona con los permisos de control de acceso de la plataforma Adobe Experience Platform. Según el nivel de permiso del usuario, puede ver, administrar y activar destinos. Para obtener información sobre los permisos individuales, consulte Control de [acceso en Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) y desplácese hacia abajo hasta la parte inferior de la página.

Para obtener más información sobre los controles de acceso, consulte la guía del usuario del control de [acceso](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md).