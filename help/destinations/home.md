---
keywords: destinos;adobe experience platform;platform;información general sobre destinos;activar datos;activar;
title: Información general sobre los destinos
description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos desde Adobe Experience Platform. Puede usar Destinos en Adobe Experience Platform para activar los datos conocidos y desconocidos para campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Información general del [!DNL Destinations] {#overview}

![Banner de información general sobre destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinos y fuentes {#destinations-and-sources}

Una de las funcionalidades principales de Platform es la ingesta de sus datos de origen y su activación para sus necesidades comerciales. Uso [sources](../sources/home.md) para introducir datos en Platform y destinos para exportar datos desde Platform.

## Pasos de destinos {#steps}

* Elija entre [catálogo de autoservicio](./catalog/overview.md) de todos los destinos disponibles en Platform.
* Utilice destinos para enviar perfiles o segmentos a plataformas de automatización de marketing, plataformas de publicidad digital y mucho más.
* Programe exportaciones de datos a sus destinos preferidos en ocasiones regulares.

## Controles {#controls}

Los controles de la variable [espacio de trabajo de destinos](./ui/destinations-workspace.md) permita:

* Examine el catálogo de plataformas de destino donde puede activar los datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Cree una cuenta en una ubicación de almacenamiento o vincule Platform a la cuenta en la plataforma de destino;
* Seleccione qué segmentos deben activarse en los destinos;
* Seleccione cuál [Campos del Modelo de datos de experiencia (XDM)](../xdm/home.md) para exportar al activar segmentos en destinos de marketing por correo electrónico.

## Tipos y categorías de destino {#types-and-categories}

Con Experience Platform, puede activar datos en varios tipos de destinos para satisfacer los casos de uso de activación. Los destinos van desde integraciones basadas en API a integraciones con sistemas de recepción de archivos, destinos de búsqueda de perfiles y mucho más. Para obtener información detallada sobre todos los destinos disponibles, consulte la [información general sobre tipos de destino y categorías](./destination-types.md).

## Destinos y controles de acceso {#access-controls}

La funcionalidad de destinos de Platform funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede ver, administrar y activar destinos. Para obtener información sobre los permisos individuales, consulte [Control de acceso en Adobe Experience Platform](../access-control/home.md) y desplácese hacia abajo hasta la parte inferior de la página.

La siguiente tabla describe los permisos y combinaciones de permisos necesarios para realizar determinadas acciones en los destinos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **[!UICONTROL Administrar destinos]** | Para conectarse a destinos de , necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** | Para activar segmentos en destinos y habilitar la variable [paso de asignación](ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Activar segmentos sin asignación]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** | Para activar segmentos en destinos y ocultar la variable [paso de asignación](ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Activar segmentos sin asignación]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

Para obtener más información sobre los controles de acceso, consulte la [Guía del usuario de control de acceso](../access-control/ui/overview.md).

### Control de acceso basado en atributos para destinos {#attribute-based-access}

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos y/o funciones específicos según los atributos.

Con el control de acceso basado en atributos, puede aplicar configuraciones de asignación a campos a los que tenga permisos. Además, no puede exportar datos a un destino si no tiene acceso a todos los campos del conjunto de datos.

Para obtener más información sobre cómo funcionan los destinos con controles de acceso basados en atributos, lea la [información general sobre el control de acceso basado en atributos](../access-control/abac/overview.md#destinations).

## Supervisión de destinos {#destinations-monitoring}

Después de establecer una conexión con un destino y completar el flujo de trabajo de activación, puede controlar las exportaciones de datos al sistema de recepción. Lea el [guía sobre la monitorización de flujos de datos a destinos en la interfaz de usuario](/help/dataflows/ui/monitor-destinations.md) para obtener más información.

También puede validar si los datos llegan correctamente al destino. La mayoría de las páginas de documentación de destino del catálogo tienen un *Validar la sección de exportación de datos*, que indica cómo se puede registrar en la plataforma de destino que los datos se están introduciendo correctamente desde Experience Platform.

## Restricciones de control de datos sobre la activación de datos en destinos {#data-governance}

El control de datos se aplica a los destinos de Platform mediante:

* *Acciones de marketing* que puede seleccionar en el flujo de trabajo crear destinos ;
* *Políticas de uso de datos* que restringen la activación de datos que contienen determinadas etiquetas de uso en destinos con determinadas acciones de marketing.

Consulte Administración de datos en la documentación de Platform para obtener más información sobre [acciones de marketing](../data-governance/policies/overview.md) y [resolución de infracciones de directiva de datos](../data-governance/enforcement/auto-enforcement.md).

Para obtener más información sobre la selección de acciones de marketing en el flujo de trabajo crear destino , consulte las siguientes páginas para los distintos tipos de destino en Platform:

* [Destinos publicitarios: Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinos publicitarios - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinos publicitarios - Pantalla y vídeo de Google 360 ](./catalog/advertising/google-dv360.md)
* [Destinos de almacenamiento en la nube](./catalog/cloud-storage/overview.md)
* [Destinos de marketing por correo electrónico](./catalog/email-marketing/overview.md)
* [Destinos sociales](./catalog/social/overview.md)

Para obtener más información sobre las infracciones de la política de datos en el flujo de trabajo de activación de segmentos, consulte la **[!UICONTROL Consulte]** paso en las siguientes guías:

* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](./ui/activate-segment-streaming-destinations.md#review)
* [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](./ui/activate-streaming-profile-destinations.md#review)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](./ui/activate-batch-profile-destinations.md#review)
