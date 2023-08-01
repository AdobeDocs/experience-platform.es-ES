---
keywords: destinos;adobe experience platform;platform;descripción general de destinos;activar datos;activar;
title: Información general sobre los destinos
description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede usar Destinos en Adobe Experience Platform para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: ce1aec87b827b6e8626018846bc6f438834fff54
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 4%

---

# Información general del [!DNL Destinations] {#overview}

![Titular de información general Destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinos y fuentes {#destinations-and-sources}

Una de las funcionalidades principales de Platform es la ingesta de datos de origen y su activación para satisfacer las necesidades de su empresa. Uso [orígenes](../sources/home.md) para introducir datos en Platform y destinos para exportar datos desde Platform.

## Pasos de destinos {#steps}

* Elija entre una [catálogo de autoservicio](./catalog/overview.md) de todos los destinos disponibles en Platform.
* Utilice destinos para enviar perfiles o audiencias a plataformas de automatización de marketing, plataformas de publicidad digital y mucho más.
* Programe exportaciones de datos a sus destinos preferidos en horas regulares.

## Controles {#controls}

Los controles del [destination workspace](./ui/destinations-workspace.md) le permite:

* Examine el catálogo de plataformas de destino donde puede activar sus datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Crear una cuenta en una ubicación de almacenamiento o vincular Platform a la cuenta en la plataforma de destino.
* Seleccione qué audiencias deben activarse en los destinos;
* Seleccione qué [Campos del modelo de datos de experiencia (XDM)](../xdm/home.md) para exportar al activar audiencias a destinos de marketing por correo electrónico.

## Tipos y categorías de destino {#types-and-categories}

Con Experience Platform, puede activar datos en varios tipos de destinos para satisfacer los casos de uso de activación. Los destinos van desde integraciones basadas en API hasta integraciones con sistemas de recepción de archivos, destinos de búsqueda de perfiles y mucho más. Para obtener información detallada sobre todos los destinos disponibles, consulte la [información general sobre tipos y categorías de destino](./destination-types.md).

## Destinos creados por Adobes y socios {#adobe-and-partner-built-destinations}

Algunos de los conectores del catálogo de destinos de Experience Platform se crean y mantienen mediante Adobe, mientras que otros se crean y mantienen mediante compañías asociadas que utilizan [Destination SDK](/help/destinations/destination-sdk/overview.md). Una nota en la parte superior de la página de documentación para cada conector creado por el socio indica si el socio crea y mantiene un destino. Por ejemplo, la variable [Conector de Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) se crea mediante el Adobe, mientras que la variable [Conector de TikTok](/help/destinations/catalog/social/tiktok.md) es creado y mantenido por el equipo de TikTok.

En el caso de los conectores creados y mantenidos por el socio, esto significa que es posible que el equipo del socio tenga que resolver los problemas con el conector (método de contacto proporcionado en la nota de la página de documentación). Para problemas con los conectores creados y mantenidos por el Adobe, póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente.

## Destinos y controles de acceso {#access-controls}

La funcionalidad de destinos de Platform funciona con permisos de control de acceso de Adobe Experience Platform. Según el nivel de permisos del usuario, puede ver, administrar y activar destinos. Para obtener información sobre los permisos individuales, consulte [Control de acceso en Adobe Experience Platform](../access-control/home.md) y desplácese hacia abajo hasta la parte inferior de la página.

En la tabla siguiente se describen los permisos y las combinaciones de permisos necesarias para realizar determinadas acciones en los destinos:

| Nivel de permisos | Descripción |
| ---- | ---- |
| **[!UICONTROL Administrar destinos]** | Para conectarse a destinos, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** | Para activar audiencias en destinos y habilitar la variable [paso de asignación](ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar segmentos sin asignación]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** | Para activar audiencias en destinos y ocultar [paso de asignación](ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar segmentos sin asignación]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

Para obtener más información sobre los controles de acceso, consulte la [Guía del usuario de control de acceso](../access-control/ui/overview.md).

### Control de acceso basado en atributos para destinos {#attribute-based-access}

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos específicos o funcionalidades basadas en atributos.

Con el control de acceso basado en atributos, puede aplicar configuraciones de asignación a campos para los que tiene permisos. Además, no puede exportar datos a un destino si no tiene acceso a todos los campos del conjunto de datos.

Para obtener más información sobre cómo funcionan los destinos con los controles de acceso basados en atributos, lea la [información general sobre el control de acceso basado en atributos](../access-control/abac/overview.md#destinations).

## Monitorización de destinos {#destinations-monitoring}

Después de establecer una conexión con un destino y completar el flujo de trabajo de activación, puede monitorizar las exportaciones de datos a su sistema de recepción. Lea el [Guía de monitorización de flujos de datos a destinos en la IU de](/help/dataflows/ui/monitor-destinations.md) para obtener más información.

También puede validar si los datos llegan a su destino correctamente. La mayoría de las páginas de documentación de destino del catálogo tienen un *Validar sección de exportación de datos*, que indica cómo se puede comprobar en la plataforma de destino que los datos se han introducido correctamente desde Experience Platform.

## Restricciones de control de datos al activar datos en destinos {#data-governance}

La gobernanza de datos se aplica a los destinos de Platform mediante:

* *Acciones de marketing* que puede seleccionar en el flujo de trabajo crear destinos;
* *Políticas de uso de datos* que restringen la activación de datos que contienen determinadas etiquetas de uso a destinos con determinadas acciones de marketing.

Consulte la documentación de Administración de datos en Platform para obtener más información sobre [acciones de marketing](../data-governance/policies/overview.md) y [resolver infracciones de directivas de datos](../data-governance/enforcement/auto-enforcement.md).

Para obtener más información sobre la selección de acciones de marketing en el flujo de trabajo Crear destino, consulte las siguientes páginas para los distintos tipos de destino en Platform:

* [Destinos publicitarios - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Destinos publicitarios - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinos publicitarios - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Destinos de almacenamiento en nube](./catalog/cloud-storage/overview.md)
* [Destinos de marketing por correo electrónico](./catalog/email-marketing/overview.md)
* [Destinos sociales](./catalog/social/overview.md)

Para obtener más información sobre las infracciones de directivas de datos en el flujo de trabajo de activación de audiencia, consulte **[!UICONTROL Revisar]** Siga estos pasos en las siguientes guías:

* [Activar datos de audiencia para transmitir audiencias y exportar destinos](./ui/activate-segment-streaming-destinations.md#review)
* [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](./ui/activate-streaming-profile-destinations.md#review)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](./ui/activate-batch-profile-destinations.md#review)
