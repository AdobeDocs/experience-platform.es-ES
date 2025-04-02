---
title: Información general sobre los destinos
description: Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede usar Destinos en Adobe Experience Platform para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 8d57694ffe0ac962b988ebcf9f35fbb7bf816c04
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 3%

---

# Información general de [!DNL Destinations] {#overview}

![Titular de información general sobre destinos.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinos y fuentes {#destinations-and-sources}

Una de las funcionalidades principales de Platform es la ingesta de datos de origen y su activación para satisfacer las necesidades de su empresa. Use [orígenes](../sources/home.md) para introducir datos en Platform y destinos para exportar datos desde Platform.

## Pasos de destinos {#steps}

* Elija entre un [catálogo de autoservicio](./catalog/overview.md) de todos los destinos disponibles en Platform.
* Utilice destinos para enviar audiencias o conjuntos de datos a plataformas de automatización de marketing, plataformas de publicidad digital y mucho más.
* Programe exportaciones de datos a sus destinos preferidos en horas regulares.

## Controles {#controls}

Los controles del área de trabajo [destinos](./ui/destinations-workspace.md) le permiten:

* Examine el catálogo de plataformas de destino donde puede activar sus datos;
* Crear, editar, activar y desactivar flujos de datos a los destinos del catálogo;
* Crear una cuenta en una ubicación de almacenamiento o vincular Platform a la cuenta en la plataforma de destino.
* Seleccione qué audiencias o conjuntos de datos deben activarse en los destinos;
* Seleccione los [campos del modelo de datos de experiencia (XDM)](../xdm/home.md) que se exportarán al activar audiencias en determinados destinos como destinos de marketing por correo electrónico, plataformas CRM, ubicaciones de almacenamiento en la nube y más.
* Active diferentes tipos de perfiles y audiencias en destinos: personas, cuentas y clientes potenciales.

## Tipos y categorías de destino {#types-and-categories}

Con Experience Platform, puede activar datos en varios tipos de destinos para satisfacer los casos de uso de activación. Los destinos van desde integraciones basadas en API hasta integraciones con sistemas de recepción de archivos, destinos de búsqueda de perfiles y mucho más. Para obtener información detallada sobre todos los destinos disponibles, lea la [descripción general de tipos y categorías de destinos](./destination-types.md).

## Destinos creados por Adobe y por socios {#adobe-and-partner-built-destinations}

Algunos de los conectores del catálogo de destinos de Experience Platform los ha creado y mantenido Adobe, mientras que otros los crean y mantienen empresas asociadas que utilizan [Destination SDK](/help/destinations/destination-sdk/overview.md). Una nota en la parte superior de la página de documentación para cada conector creado por el socio indica si el socio crea y mantiene un destino. Por ejemplo, el [conector Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) lo crea Adobe, mientras que el [conector TikTok](/help/destinations/catalog/social/tiktok.md) lo crea y mantiene el equipo de TikTok.

En el caso de los conectores creados y mantenidos por el socio, esto significa que es posible que el equipo del socio tenga que resolver los problemas con el conector (método de contacto proporcionado en la nota de la página de documentación). Para problemas con los conectores creados y mantenidos por Adobe, póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente.

## Destinos y controles de acceso {#access-controls}

La funcionalidad de destinos de Platform funciona con permisos de control de acceso de Adobe Experience Platform. Según el nivel de permisos del usuario, puede ver, administrar y activar destinos. Para obtener información sobre los permisos individuales, ve a [control de acceso en Adobe Experience Platform](../access-control/home.md) y desplázate hacia abajo hasta la tabla en la parte inferior de la página.

En la tabla siguiente se describen los permisos y las combinaciones de permisos necesarias para realizar determinadas acciones en los destinos.

| Nivel de permisos | Descripción |
| ---- | ---- |
| **[!UICONTROL Ver destinos]** | Para acceder a la pestaña destinos en la interfaz de usuario de Experience Platform, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de [Ver destinos]**. |
| **[!UICONTROL Ver destinos]**, **[!UICONTROL Administrar destinos]** | Para conectarse a destinos, necesita los **[!UICONTROL permisos de control de acceso[Ver destinos]** y **[!UICONTROL Administrar destinos]**](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** | Para activar audiencias en destinos y habilitar el [paso de asignación](ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo, necesita **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar segmentos sin asignación]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** | Para agregar o quitar audiencias de flujos de datos existentes sin tener acceso al [paso de asignación](ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo, necesita los permisos de **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar segmentos sin asignación]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ver destinos]**, **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** | Para exportar conjuntos de datos a destinos, necesita **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** [permisos de control de acceso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ver gráfico de identidad]** | Para exportar *identidades* a destinos, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de [Ver gráfico de identidad]**. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

El diagrama siguiente muestra visualmente qué permisos necesita según las operaciones que desee realizar en los destinos.

![Diagrama que muestra los permisos necesarios para realizar determinadas acciones en los destinos.](/help/destinations/assets/overview/permissions-diagram.png)

Para obtener más información acerca de los controles de acceso, consulte la [Guía del usuario de control de acceso](../access-control/ui/overview.md).

### Control de acceso basado en atributos para destinos {#attribute-based-access}

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos específicos o funcionalidades basadas en atributos.

Con el control de acceso basado en atributos, puede aplicar configuraciones de asignación a campos para los que tiene permisos. Además, no puede exportar datos a un destino si no tiene acceso a todos los campos del conjunto de datos.

Para obtener más información sobre cómo funcionan los destinos con los controles de acceso basados en atributos, lea la [descripción general del control de acceso basado en atributos](../access-control/abac/overview.md#destinations).

## Eliminación de perfiles de destinos {#profile-removal}

Cuando se elimina un perfil de una audiencia activada en un destino, ese perfil también se elimina de la audiencia correspondiente en la plataforma de destino. Por ejemplo, si se quita un perfil de una audiencia previamente activada en LinkedIn, ese perfil se eliminará de la [!UICONTROL audiencia coincidente de LinkedIn] asociada.

La eliminación de perfiles de los destinos, también conocida como &quot;no segmentación&quot;, se produce en la misma cadencia que la segmentación. Tan pronto como un perfil se elimina de una audiencia en Experience Platform, el siguiente flujo de datos programado al destino refleja ese cambio y elimina el perfil de la audiencia de destino.

La velocidad real a la que se aplica la eliminación de perfiles en la plataforma de destino puede variar en función del comportamiento de ingesta y procesamiento del destino.

## Monitorización de destinos {#destinations-monitoring}

Después de establecer una conexión con un destino y completar el flujo de trabajo de activación, puede monitorizar las exportaciones de datos a su sistema de recepción. Lea la [guía sobre la supervisión de flujos de datos a destinos en la interfaz de usuario](/help/dataflows/ui/monitor-destinations.md) para obtener más información.

![Ejemplo de página de supervisión de destinos.](./assets/overview/monitoring-page-example.png)

También puede validar si los datos llegan a su destino correctamente. La mayoría de las páginas de documentación de destino del catálogo tienen una *sección Validar exportación de datos*, que indica cómo se puede comprobar en la plataforma de destino que los datos se están introduciendo correctamente desde Experience Platform. Vea un ejemplo de esta sección para [Amazon Ads destination](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Restricciones de la gobernanza de datos al activar datos en destinos {#data-governance}

La gobernanza de datos se aplica a los destinos de Platform mediante:

* *Acciones de marketing* que puede seleccionar en el flujo de trabajo Crear destinos;
* *Políticas de uso de datos* que restringen la activación de datos que contienen determinadas etiquetas de uso a destinos con determinadas acciones de marketing.

Consulte la Administración de datos en la documentación de Platform para obtener más información sobre [acciones de marketing](../data-governance/policies/overview.md) y [resolución de violaciones de políticas de datos](../data-governance/enforcement/auto-enforcement.md).

Para obtener más información sobre la selección de acciones de marketing en el flujo de trabajo Crear destino, consulte las siguientes páginas para los distintos tipos de destino en Platform:

* [Destinos de Advertising: Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Destinos Advertising - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinos Advertising - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Destinos de almacenamiento en nube](./catalog/cloud-storage/overview.md)
* [Destinos de marketing por correo electrónico](./catalog/email-marketing/overview.md)
* [Destinos sociales](./catalog/social/overview.md)

Para obtener más información sobre las infracciones de directivas de datos en el flujo de trabajo de activación de audiencia, consulte el paso **[!UICONTROL Revisar]** en las siguientes guías:

* [Activar datos de audiencia para transmitir audiencias y exportar destinos](./ui/activate-segment-streaming-destinations.md#review)
* [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](./ui/activate-streaming-profile-destinations.md#review)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](./ui/activate-batch-profile-destinations.md#review)

## Términos y condiciones {#terms-and-conditions}

Al usar cualquiera de los destinos etiquetados como beta (&quot;Beta&quot;), el Cliente reconoce por la presente que Beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo Beta. Se le aconseja utilizar Informativo y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dicho Beta y/o materiales de acompañamiento. Beta se considera información confidencial de Adobe.

Cualquier &quot;comentario&quot; (información sobre Beta, incluidos, entre otros, problemas o defectos que encuentre al utilizar Beta, sugerencias, mejoras y recomendaciones) proporcionado por usted a Adobe se asigna a Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

Envíe comentarios abiertos o cree un ticket de asistencia para compartir sus sugerencias o informar de un error, y busque una mejora de las funciones.