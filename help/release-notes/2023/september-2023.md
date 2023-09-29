---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de septiembre de 2023 de Adobe Experience Platform.
source-git-commit: c57845ab2bd9ce16fb34b6babfa90a393b101409
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 24%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 28 de septiembre de 2023**

Nuevas funciones de Adobe Experience Platform:

- [Atributos calculados](#computed-attributes)

Actualizaciones de las funciones existentes en Experience Platform:

- [Alertas](#alerts)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Servicio de identidad](#identity-service)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Atributos calculados {#computed-attributes}

Los atributos calculados permiten resumir fácilmente los datos de evento en atributos de perfil a través de una interfaz de usuario intuitiva para una segmentación, personalización y activación basadas en el comportamiento mejoradas. Con esta función, puede crear atributos calculados de forma automática, administrarlos y utilizarlos en la segmentación, destinos de Real-Time CDP o Adobe Journey Optimizer. Además, los atributos calculados simplifican la segmentación y los flujos de trabajo de recorrido para ayudarle a ofrecer sin problemas experiencias relevantes. Para obtener más información sobre los atributos calculados, lea la [información general sobre atributos calculados](../../profile/computed-attributes/overview.md).

## Alertas {#alerts}

Experience Platform permite suscribirse a alertas basadas en eventos para diversas actividades de Platform. Puede suscribirse a diferentes reglas de alerta a través de la variable [!UICONTROL Alertas] en la interfaz de usuario de Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o a través de notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Pestaña Historial de alertas | Las Alertas [!UICONTROL Historial] ahora incluirá todos los eventos, incluidos retrasos, inicios, aciertos y errores. Lea el [documentación de IU de alertas](../../observability/alerts/ui.md) para obtener más información sobre la pestaña history. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] descripción general](../../observability/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Secuencias de datos | Compatibilidad con la búsqueda de dispositivos | Al configurar una secuencia de datos, ahora puede seleccionar el nivel de información de búsqueda de dispositivos que desea recopilar. La información de búsqueda de dispositivos incluye datos sobre el dispositivo, el hardware, el sistema operativo y el explorador utilizados para interactuar con la página. <br>  La información de búsqueda de dispositivos no se puede recopilar junto con el agente de usuario y las sugerencias del cliente. Si elige recopilar información del dispositivo, se deshabilita la recopilación de sugerencias del agente de usuario y del cliente, y viceversa. Toda la información de búsqueda del dispositivo se almacena en `xdm:device` grupo de campos. Obtenga más información en la documentación sobre [configuración de flujos de datos](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensiones | [!DNL TikTok] extensión de API de eventos web | El [[!DNL TikTok] API de eventos web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) La extensión de le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL TikTok] en forma de eventos del lado del servidor que utilizan el [!DNL TikTok] API de eventos web. |

{style="table-layout:auto"}

Para obtener más información sobre la recopilación de datos, lea la [resumen de recopilación de datos](../../tags/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Nuevo o actualizado | Descripción |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Nuevo | Activar audiencias previamente incorporadas a [!DNL LiveRamp] a editores Premium en medios de TV móviles, web, de visualización y conectados. <br> Después de incorporar audiencias a su [!DNL LiveRamp] cuenta a través de [LiveRamp: incorporación](../../destinations/catalog/advertising/liveramp-onboarding.md) conexión, utilice el nuevo [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) para activar las audiencias en destinos de flujo descendente. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nuevo | [[!DNL HubSpot]](https://www.hubspot.com) es una plataforma CRM con todo el software, las integraciones y los recursos que necesita para conectar marketing, ventas, gestión de contenido y servicio al cliente. Permite conectar los datos, los equipos y los clientes en una plataforma CRM. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Actualizado   | Se ha añadido la compatibilidad con [!DNL Dynamics 365] prefijos de campo personalizados para campos personalizados que no se crearon dentro de la solución predeterminada en [!DNL Dynamics 365]. Un nuevo campo de entrada, **[!UICONTROL Prefijo de personalización]**, se ha añadido en la [Rellenar detalles de destino](#destination-details) paso. |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Actualizado   | El destino de Audiencias del Experience Cloud ya está disponible de forma general. Utilice este destino para activar audiencias de Real-Time CDP a Audience Manager y Adobe Analytics. Necesita una licencia de Audience Manager para enviar audiencias a Adobe Analytics. |

{style="table-layout:auto"}

<!-- 

Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 


-->

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Exportaciones de datos en Real-Time CDP | El [exportación de conjuntos de datos](../../destinations/ui/export-datasets.md) funcionalidad ya está disponible de forma general. Consulte [qué conjuntos de datos puede exportar en función de la aplicación del Experience Platform](../../destinations/ui/export-datasets.md#datasets-to-export) ha adquirido y consulte la [protecciones para exportar conjuntos de datos](/help/destinations/guardrails.md#dataset-exports). |
| (Beta) Compatibilidad con la exportación de objetos de tipo matriz | Exporte matrices de valores primitivos (valores de cadena, int o booleanos) como archivos de esquema plano a destinos de almacenamiento en la nube. Obtenga más información sobre la funcionalidad en la [documentación](../../destinations/ui/export-arrays-calculated-fields.md). |
| Selectores desplegables dinámicos en Destination SDK | Al crear un destino mediante Destination SDK, ahora puede utilizar [selectores desplegables dinámicos](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) para rellenar los campos de un selector desplegable con valores recuperados de una API. |

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Utilizar de [transparencia de supervisión](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) ahora disponible para destinos empresariales ([API HTTP](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) y [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) en el nivel de ejecución del flujo de datos para monitorizar las métricas de activación y el estado en [vista de detalles del flujo de datos](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), con información adicional a través de códigos de error y mensajes para la resolución de problemas.
- Cuando actualice el nombre de las audiencias asignadas al [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md)y otros destinos que utilizan [plantillas de actualización de audiencia](../../destinations/destination-sdk/metadata-api/update-audience-template.md)Sin embargo, estos cambios de nombre ahora se reflejan hacia abajo en el destino.

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la IU del servicio de identidad | Utilice la herramienta de creación de áreas de nombres personalizadas mejorada en la interfaz de usuario de Experience Platform para administrar mejor las áreas de nombres personalizadas y sus tipos de identidad correspondientes. La interfaz de usuario mejorada del servicio de identidad le proporciona lo siguiente: <ul><li>Experiencia contextual: Indicaciones visuales, claridad y contexto de lo que es un área de nombres de identidad y de los tipos de identidad.</li><li>Precisión: mejor gestión de errores, sin más nombres de identidad duplicados.</li><li>Capacidad de detección: acceso a la documentación desde un cuadro de diálogo dentro del producto.</li></ul> Para obtener más información, lea la guía de [crear áreas de nombres personalizadas](../../identity-service/namespaces.md#create-namespaces). |
| Cambios en los límites del gráfico de identidad | El límite del gráfico de identidades ha cambiado de 150 a 50 identidades. Cuando se incorpora una nueva identidad en un gráfico completo, se elimina la identidad más antigua en función de la marca de tiempo de ingesta y el tipo de identidad. Los tipos de identidad de cookies tienen prioridad para su eliminación. Póngase en contacto con el equipo de cuenta de Adobe para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene lo siguiente: <ul><li>un área de nombres personalizada donde los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.</li><li>un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.</li></ul> El personal de ingeniería de Adobes procesará manualmente estas solicitudes. Para obtener más información, lea la [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Para obtener más información sobre Identity Service, lea la [Introducción al servicio de identidad](../../identity-service/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Columnas personalizables | Ahora puede personalizar el diseño de Audience Portal con columnas cuyo tamaño se puede cambiar. Para obtener más información acerca de esta funcionalidad, lea la [Guía de IU de segmentación](../../segmentation/ui/overview.md#customize). |
| Desglose de frecuencia de actualización | Ahora puede ver un desglose de las frecuencias de actualización de las audiencias de su organización. Para obtener más información acerca de esta funcionalidad, lea la [Guía de IU de segmentación](../../segmentation/ui/overview.md#browse). |

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).

Para obtener más información sobre el servicio de segmentación, lea la [Resumen del servicio de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevos parámetros para `offset` paginación en orígenes de autoservicio (SDK por lotes) | Ahora puede especificar un `endConditionName` y `endConditionValue` para su origen al utilizar `offset` paginación. Estos parámetros le permiten indicar la condición que debe finalizar el bucle de paginación en la siguiente solicitud HTTP. Para obtener más información, lea la [Guía de paginación para orígenes de autoservicio (SDK por lotes)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).