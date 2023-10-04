---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de septiembre de 2023 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 35d72969946dd79c356212ce53ee75b8c84f036c
workflow-type: tm+mt
source-wordcount: '2284'
ht-degree: 26%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 28 de septiembre de 2023**

Nuevas funciones de Adobe Experience Platform:

- [Atributos calculados](#computed-attributes)

Actualizaciones de las funciones existentes en Experience Platform:

- [Alertas](#alerts)
- [Paneles](#dashboards)
- [Recopilación de datos](#data-collection)
- [Gobernanza de datos](#data-governance)
- [Higiene de los datos](#hygiene)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de consultas](#query-service)
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

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través del cual puede ver información importante acerca de los datos de su organización, tal como se capturan durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| [Mejora del tablero de uso de licencias](../../dashboards/guides/license-usage.md) | Mantenga el control de los acuerdos de licencia con visualizaciones mejoradas de informes y métricas clave con respecto al uso de licencias de su organización. Estas mejoras proporcionan un alto grado de granularidad sobre las métricas de uso de licencias de todos los productos de Experience Platform que ha adquirido. |

{style="table-layout:auto"}

Para obtener más información sobre el tablero de uso de licencias, consulte la [información general del tablero de uso de licencias](../../dashboards/guides/destinations.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Secuencias de datos | Compatibilidad con la búsqueda de dispositivos | Al configurar una secuencia de datos, ahora puede seleccionar el nivel de información de búsqueda de dispositivos que desea recopilar. La información de búsqueda de dispositivos incluye datos sobre el dispositivo, el hardware, el sistema operativo y el explorador utilizados para interactuar con la página. <br>  La información de búsqueda de dispositivos no se puede recopilar junto con el agente de usuario y las sugerencias del cliente. Si elige recopilar información del dispositivo, se deshabilita la recopilación de sugerencias del agente de usuario y del cliente, y viceversa. Toda la información de búsqueda del dispositivo se almacena en `xdm:device` grupo de campos. Obtenga más información en la documentación sobre [configuración de flujos de datos](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensiones | [!DNL TikTok] extensión de API de eventos web | El [[!DNL TikTok] API de eventos web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) La extensión de le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL TikTok] en forma de eventos del lado del servidor que utilizan el [!DNL TikTok] API de eventos web. |

{style="table-layout:auto"}

Para obtener más información sobre la recopilación de datos, lea la [resumen de recopilación de datos](../../tags/home.md).

## Control de datos {#data-governance}

La gobernanza de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña una función clave dentro de Experience Platform en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de acceso a los datos y el control de acceso de los datos para las acciones de marketing.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Nuevas etiquetas de Partner Ecosystem para datos de terceros | Hay disponibles nuevas etiquetas de uso de datos para el enriquecimiento y la prospección de terceros. Consulte la [documentación sobre etiquetas de Partner Ecosystem](../../data-governance/labels/reference.md#partner) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información acerca de la gobernanza de datos, lea la [información general de gobernanza de datos](../../data-governance/home.md).

## Higiene de los datos {#hygiene}

Experience Platform proporciona un conjunto de funciones de higiene de datos que le permiten administrar los datos almacenados mediante la eliminación mediante programación de registros de consumidores y conjuntos de datos. Con cualquiera de las [!UICONTROL Ciclo de datos] en la IU o a través de llamadas a la API de higiene de los datos, puede administrar de forma eficaz sus almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas de la organización lo consideran necesario.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} | Administre el ciclo de vida de los datos en todos los almacenes de datos para cumplir los compromisos de los clientes y los acuerdos de licencia con las funciones avanzadas de administración del ciclo de vida de los datos de Adobe Experience Platform: caducidad automatizada del conjunto de datos y eliminación de registros.<br>Con la caducidad automatizada de los conjuntos de datos, puede eliminar conjuntos de datos completos y establecer una fecha y una hora para que se eliminen.<br>La eliminación de registros permite eliminar perfiles de consumidores individuales segmentando sus identidades principales. Puede proporcionar las identidades principales individualmente a través de la interfaz de usuario o a través de la carga del archivo CSV/JSON. Consulte la [Documentación de eliminación de registros](../../hygiene/ui/record-delete.md) para obtener más información |
| Caducidad de conjuntos de datos | Minimice los datos y mantenga el control de los acuerdos de licencia con Caducidad automatizada del conjunto de datos. Reduzca los volúmenes de datos eliminando conjuntos de datos completos y establezca una fecha y una hora para eliminar el conjunto de datos. Consulte la [documentación sobre caducidades del conjunto de datos](../../hygiene/ui/dataset-expiration.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las capacidades de higiene de los datos de Platform, consulte la [resumen de higiene de datos](../../hygiene/home.md).

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

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Acciones rápidas agregadas al Editor de esquemas | Se han añadido nuevas acciones rápidas al lienzo del Editor de esquemas. Ahora puede copiar la estructura JSON o eliminar el esquema directamente desde el editor.<br>![Las acciones rápidas en el Editor de esquemas.](../2023/assets/schema-editor-copy-json.png "Se resaltan el Editor de esquemas con Más y Copiar a JSON."){width="100" zoomable="yes"} |
| Filtrado de recursos XDM por creador personalizado o estándar | Las listas de esquemas, grupos de campos, tipos de datos y clases disponibles ahora se filtran previamente según su método de creación. Esto le permite filtrar los recursos en función de si se han creado a medida o por Adobe.<br>![Los filtros Estándar y Personalizados del espacio de trabajo Esquemas.](../2023/assets/standard-and-custom-classes.png "Espacio de trabajo Esquemas con los filtros Estándar y Personalizado resaltados."){width="100" zoomable="yes"} <br> Consulte la [creación y edición de la documentación de recursos](../../xdm/ui/resources/classes.md#filter.md) para obtener más información. |

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Flujo de trabajo de creación de esquemas actualizado | Se ha implementado un nuevo flujo de trabajo de creación de esquemas para optimizar el proceso. <br> ![La nueva IU de creación de esquemas.](../2023/assets/schema-class-options.png "Nuevo selector de detalles de esquema resaltado."){width="100" zoomable="yes"} <br> Consulte la [documentación de creación de esquemas](../../xdm/ui/resources/schemas.md#create) para obtener más información. |

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Volver]](https://github.com/adobe/xdm/pull/1773/files) | La RMA (Autorización de Devolución de Mercancía) emitida. |
| Tipo de datos | [[!UICONTROL Devolver elemento]](https://github.com/adobe/xdm/pull/1773/files) | La información del artículo devuelto dentro de la RMA (Autorización de Devolución de Mercancías). |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Extensión | [!UICONTROL Campos de entidad de AJO] | El [[!UICONTROL indicador para varias variantes]](https://github.com/adobe/xdm/pull/1774/files) se ha añadido a [!UICONTROL Campos de entidad de AJO] para identificar si la variante es una variante múltiple o no. |
| Tipo de datos | [!UICONTROL Elemento de lista de productos] | [[!UICONTROL Devolver elemento]](https://github.com/adobe/xdm/pull/1773/files) para incluir la información de autorización de devolución de mercancía. |
| Tipo de datos | Pedido | [[!UICONTROL Información de retorno]](https://github.com/adobe/xdm/pull/1773/files) se añadió para incluir la autorización de devolución de material (RMA) emitida. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, consulte la [información general del sistema XDM](../../xdm/home.md)

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la IU del servicio de identidad | Utilice la herramienta de creación de áreas de nombres personalizadas mejorada en la interfaz de usuario de Experience Platform para administrar mejor las áreas de nombres personalizadas y sus tipos de identidad correspondientes. La interfaz de usuario mejorada del servicio de identidad le proporciona lo siguiente: <ul><li>Experiencia contextual: Indicaciones visuales, claridad y contexto de lo que es un área de nombres de identidad y de los tipos de identidad.</li><li>Precisión: mejor gestión de errores, sin más nombres de identidad duplicados.</li><li>Capacidad de detección: acceso a la documentación desde un cuadro de diálogo dentro del producto.</li></ul> Para obtener más información, lea la guía de [crear áreas de nombres personalizadas](../../identity-service/namespaces.md#create-namespaces). |
| Cambios en los límites del gráfico de identidad | El límite del gráfico de identidades ha cambiado de 150 a 50 identidades. Cuando se incorpora una nueva identidad en un gráfico completo, se elimina la identidad más antigua en función de la marca de tiempo de ingesta y el tipo de identidad. Los tipos de identidad de cookies tienen prioridad para su eliminación. Póngase en contacto con el equipo de cuenta de Adobe para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene lo siguiente: <ul><li>un área de nombres personalizada donde los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.</li><li>un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.</li></ul> El personal de ingeniería de Adobes procesará manualmente estas solicitudes. Para obtener más información, lea la [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Para obtener más información sobre Identity Service, lea la [Introducción al servicio de identidad](../../identity-service/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos de [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para usar en sistema de informes, espacio de trabajo de ciencia de datos o para su inserción en el perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones de IU de filtrado de registros | El filtrado mejorado de los registros de consultas mejora la visibilidad de los registros generados por el usuario para la supervisión, administración y solución de problemas. Puede filtrar la lista de registros de consultas en función de diferentes configuraciones. <br> ![Configuración del filtro de registro de consultas.](../2023/assets/log-filter-settings.png "Se resaltan los nuevos filtros de registro de consultas."){width="100" zoomable="yes"}  <br> Consulte la [documentación de registros de consultas](../../query-service/ui/query-logs.md#filter-logs) para obtener más información. |
| Varias actualizaciones de la IU del Editor de consultas | Ahora puede Ejecutar varias consultas secuenciales en el Editor de consultas o escribir más de una consulta y ejecutar todas las consultas de forma secuencial. Para añadir más flexibilidad a la ejecución de la consulta, puede resaltar la consulta elegida y seleccionar esa consulta específica para que se ejecute de forma independiente de las demás. Consulte la [Guía de IU del Editor de consultas](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, vea la [Información general del servicio de consulta](../../query-service/home.md).

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
