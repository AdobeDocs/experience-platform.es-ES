---
title: 'Notas de la versión de Adobe Experience Platform: septiembre de 2023'
description: Las notas de la versión de septiembre de 2023 de Adobe Experience Platform.
exl-id: ff7fb0c1-6941-4339-8648-58f9b9e9a91f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 28%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: viernes, 28 de septiembre de 2023**

Nuevas funciones de Adobe Experience Platform:

- [Atributos calculados](#computed-attributes)

Actualizaciones de funciones existentes en Experience Platform:

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

Los atributos calculados permiten resumir fácilmente los datos de evento en atributos de perfil a través de una interfaz de usuario intuitiva para una segmentación, personalización y activación basadas en el comportamiento mejoradas. Con esta función, puede crear atributos calculados de forma automática, administrarlos y utilizarlos en la segmentación, destinos de Real-Time CDP o Adobe Journey Optimizer. Además, los atributos calculados simplifican la segmentación y los flujos de trabajo de recorrido para ayudarle a ofrecer sin problemas experiencias relevantes. Para obtener más información sobre los atributos calculados, lea [descripción general de los atributos calculados](../../profile/computed-attributes/overview.md).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a distintas reglas de alerta a través de la ficha [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o mediante notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Pestaña Historial de alertas | La ficha Alertas [!UICONTROL Historial] ahora incluirá todos los eventos, incluidos retrasos, inicios, aciertos y errores. Lea la [documentación de la interfaz de usuario de alertas](../../observability/alerts/ui.md) para obtener más información sobre la ficha historial. |

{style="table-layout:auto"}

Para obtener más información acerca de las alertas, lea la [[!DNL Observability Insights] descripción general](../../observability/home.md).

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios(as) [!DNL dashboards] a través de los cuales puede ver información importante acerca de los datos de su organización, según se capturan durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| [Mejora del tablero de uso de licencias](../../dashboards/guides/license-usage.md) | Mantenga el control de los acuerdos de licencia con visualizaciones mejoradas de informes y métricas clave con respecto al uso de licencias de su organización. Estas mejoras proporcionan un alto grado de granularidad sobre las métricas de uso de licencias de todos los productos de Experience Platform que ha adquirido. |

{style="table-layout:auto"}

Para obtener más información sobre el tablero de uso de licencias, consulte la [descripción general del tablero de uso de licencias](../../dashboards/guides/destinations.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Secuencias de datos | Compatibilidad con la búsqueda de dispositivos | Al configurar una secuencia de datos, ahora puede seleccionar el nivel de información de búsqueda de dispositivos que desea recopilar. La información de búsqueda de dispositivos incluye datos sobre el dispositivo, el hardware, el sistema operativo y el explorador utilizados para interactuar con la página. No se puede recopilar la información de búsqueda del dispositivo <br> junto con las sugerencias del agente de usuario y del cliente. Si elige recopilar información del dispositivo, se deshabilita la recopilación de sugerencias del agente de usuario y del cliente, y viceversa. Toda la información de búsqueda del dispositivo se almacena en el grupo de campos `xdm:device`. Obtenga más información en la documentación sobre [configuración de flujos de datos](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensiones | Extensión de la API de eventos web [!DNL TikTok] | La extensión de la API [[!DNL TikTok] Web Events](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL TikTok] en forma de eventos del lado del servidor mediante la API de eventos web [!DNL TikTok]. |

{style="table-layout:auto"}

Para obtener más información acerca de la recopilación de datos, lea la [información general de recopilación de datos](../../tags/home.md).

## Control de datos {#data-governance}

La gobernanza de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña una función clave dentro de Experience Platform en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de acceso a los datos y el control de acceso de los datos para las acciones de marketing.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Nuevas etiquetas de Partner Ecosystem para datos de terceros | Hay disponibles nuevas etiquetas de uso de datos para el enriquecimiento y la prospección de terceros. Consulte la [documentación sobre etiquetas de ecosistema de socio](../../data-governance/labels/reference.md#partner) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información acerca de la gobernanza de datos, lea la [información general de gobernanza de datos](../../data-governance/home.md).

## Higiene de datos {#hygiene}

Experience Platform proporciona un conjunto de funciones de higiene de los datos que le permiten administrar los datos almacenados mediante la eliminación mediante programación de registros de consumidores y conjuntos de datos. Con el área de trabajo [!UICONTROL Data Lifecycle] en la interfaz de usuario o a través de llamadas a la API de higiene de datos, puede administrar de manera eficaz sus almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas organizativas lo consideran necesario.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} Eliminación de registro (versión limitada) | Administre el ciclo vital de los datos en todos los almacenes de datos para cumplir los compromisos de los clientes y los acuerdos de licencia con las funciones de administración avanzada del ciclo vital de los datos en Adobe Experience Platform: caducidad automatizada del conjunto de datos y eliminación de registros.<br>Con la caducidad automatizada del conjunto de datos, puede eliminar conjuntos de datos completos y establecer una fecha y una hora para que se eliminen.La eliminación de registro <br>le permite eliminar perfiles de consumidores individuales mediante la segmentación de sus identidades principales. Puede proporcionar las identidades principales individualmente a través de la interfaz de usuario o a través de la carga del archivo CSV/JSON. Consulte la [documentación de eliminación de registros](../../hygiene/ui/record-delete.md) para obtener más información |
| Caducidades de los conjuntos de datos | Minimice los datos y mantenga el control de los acuerdos de licencia con Caducidad automatizada del conjunto de datos. Reduzca los volúmenes de datos eliminando conjuntos de datos completos y establezca una fecha y una hora para eliminar el conjunto de datos. Consulte la [documentación sobre la caducidad de los conjuntos de datos](../../hygiene/ui/dataset-expiration.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las capacidades de higiene de datos de Experience Platform, consulte la [descripción general de higiene de datos](../../hygiene/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Nuevo o actualizado | Descripción |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Nuevo | Active las audiencias previamente incorporadas a [!DNL LiveRamp] para editores Premium en medios móviles, web, de visualización y de TV conectados. <br> Después de incorporar audiencias a su cuenta de [!DNL LiveRamp] a través de la conexión de [LiveRamp - Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md), use la nueva conexión de [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) para activar las audiencias en destinos de flujo descendente. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nuevo | [[!DNL HubSpot]](https://www.hubspot.com) es una plataforma CRM con todo el software, las integraciones y los recursos que necesita para conectar el marketing, las ventas, la administración de contenido y el servicio al cliente. Permite conectar los datos, los equipos y los clientes en una plataforma CRM. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Actualizado   | Se agregó compatibilidad con [!DNL Dynamics 365] prefijos de campo personalizados para campos personalizados que no se crearon dentro de la solución predeterminada en [!DNL Dynamics 365]. Se ha agregado un nuevo campo de entrada **[!UICONTROL Prefijo de personalización]** en el paso [Rellenar detalles de destino](#destination-details). |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Actualizado   | El destino de Audiencias de Experience Cloud ya está disponible de forma general. Utilice este destino para activar audiencias de Real-Time CDP a Audience Manager y Adobe Analytics. Necesita una licencia de Audience Manager para enviar audiencias a Adobe Analytics. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Exportaciones de datos en Real-Time CDP | La funcionalidad [exportación de conjuntos de datos](../../destinations/ui/export-datasets.md) ya está disponible de forma general. Vea [qué conjuntos de datos puede exportar en función de la aplicación de Experience Platform](../../destinations/ui/export-datasets.md#datasets-to-export) que compró y compruebe las [protecciones para exportar conjuntos de datos](/help/destinations/guardrails.md#dataset-exports). |
| (Beta) Compatibilidad con la exportación de objetos de tipo matriz | Exporte matrices de valores primitivos (valores de cadena, int o booleanos) como archivos de esquema plano a destinos de almacenamiento en la nube. Obtenga más información acerca de la funcionalidad en la [documentación](../../destinations/ui/export-arrays-maps-objects.md). |
| Selectores desplegables dinámicos en Destination SDK | Al crear un destino mediante Destination SDK, ahora puede usar [selectores desplegables dinámicos](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) para rellenar los campos de un selector desplegable con los valores recuperados de una API. |

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Use [transparencia de supervisión](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) ahora disponible para destinos empresariales ([API HTTP](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) y [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) en el nivel de ejecución del flujo de datos para supervisar las métricas de activación y el estado en la [vista de detalles del flujo de datos](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), con información adicional a través de códigos de error y mensajes para solucionar problemas.
- Cuando actualiza el nombre de las audiencias asignadas a [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md) y otros destinos que usan [plantillas de actualización de audiencias](../../destinations/destination-sdk/metadata-api/update-audience-template.md), estos cambios de nombre ahora se reflejan en el flujo descendente del destino.

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Acciones rápidas agregadas al Editor de esquemas | Se han añadido nuevas acciones rápidas al lienzo del Editor de esquemas. Ahora puede copiar la estructura JSON o eliminar el esquema directamente desde el editor.<br>![Acciones rápidas en el Editor de esquemas.](../2023/assets/schema-editor-copy-json.png "Se resaltó el Editor de esquemas con más y Copiar a JSON."){width="100" zoomable="yes"} |
| Filtrado de recursos XDM por creador personalizado o estándar | Las listas de esquemas, grupos de campos, tipos de datos y clases disponibles ahora se filtran previamente según su método de creación. Esto le permite filtrar los recursos en función de si fueron creados o creados por Adobe.<br>![Filtros estándar y personalizados en el área de trabajo Esquemas.](../2023/assets/standard-and-custom-classes.png "Espacio de trabajo de esquemas con los filtros estándar y personalizados resaltados."){width="100" zoomable="yes"} <br> Consulte la [documentación de creación y edición de recursos](../../xdm/ui/resources/classes.md#filter.md) para obtener más información. |

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Flujo de trabajo de creación de esquemas actualizado | Se ha implementado un nuevo flujo de trabajo de creación de esquemas para optimizar el proceso. <br> ![Nueva interfaz de usuario para la creación de esquemas.](../2023/assets/schema-class-options.png "Nuevo selector de detalles de esquema resaltado."){width="100" zoomable="yes"} <br> Consulte la [documentación de creación de esquemas](../../xdm/ui/resources/schemas.md#create) para obtener más información. |

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Devolver]](https://github.com/adobe/xdm/pull/1773/files) | La RMA (Autorización de Devolución de Mercancía) emitida. |
| Tipo de datos | [[!UICONTROL Devolver elemento]](https://github.com/adobe/xdm/pull/1773/files) | La información del artículo devuelto dentro de la RMA (Autorización de Devolución de Mercancías). |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Extensión | [!UICONTROL Campos de entidad de AJO] | El indicador [[!UICONTROL para múltiples variantes]](https://github.com/adobe/xdm/pull/1774/files) se agregó a [!UICONTROL Campos de entidad de AJO] para identificar si la variante es multivariante o no. |
| Tipo de datos | [!UICONTROL Elemento de lista de productos] | Se agregó [[!UICONTROL artículo de devolución]](https://github.com/adobe/xdm/pull/1773/files) para incluir la información de autorización de devolución de mercancía. |
| Tipo de datos | Pedido | [[!UICONTROL Se agregó la información de devolución]](https://github.com/adobe/xdm/pull/1773/files) para incluir la autorización de devolución de material (RMA) emitida. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [descripción general del sistema XDM](../../xdm/home.md)

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la IU del servicio de identidad | Utilice la herramienta mejorada de creación de áreas de nombres personalizadas en la interfaz de usuario de Experience Platform para administrar mejor las áreas de nombres personalizadas y sus tipos de identidad correspondientes. La interfaz de usuario mejorada del servicio de identidad le proporciona lo siguiente: <ul><li>Experiencia contextual: Indicaciones visuales, claridad y contexto de lo que es un área de nombres de identidad y de los tipos de identidad.</li><li>Precisión: mejor gestión de errores, sin más nombres de identidad duplicados.</li><li>Capacidad de detección: acceso a la documentación desde un cuadro de diálogo dentro del producto.</li></ul> Para obtener más información, lea la guía sobre [creación de áreas de nombres personalizadas](../../identity-service/features/namespaces.md#create-namespaces). |
| Cambios en los límites del gráfico de identidad | El límite del gráfico de identidades ha cambiado de 150 a 50 identidades. Cuando se incorpora una nueva identidad en un gráfico completo, se elimina la identidad más antigua en función de la marca de tiempo de ingesta y el tipo de identidad. Los tipos de identidad de cookies tienen prioridad para su eliminación. Póngase en contacto con el equipo de cuenta de Adobe para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene lo siguiente: <ul><li>un área de nombres personalizada donde los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.</li><li>un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.</li></ul> El personal de ingeniería de Adobe procesará manualmente estas solicitudes. Para obtener más información, lea las [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md) y la guía sobre las [prácticas recomendadas de asignación de derechos de licencia para la administración de datos](../../landing/license-usage-and-guardrails/data-management-best-practices.md). |

{style="table-layout:auto"}

Para obtener más información acerca del Servicio de identidad, lea la [Información general del Servicio de identidad](../../identity-service/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones de IU de filtrado de registros | El filtrado mejorado de los registros de consultas mejora la visibilidad de los registros generados por el usuario para la supervisión, administración y solución de problemas. Puede filtrar la lista de registros de consultas en función de diferentes configuraciones. <br> ![La configuración del filtro de registro de consultas.](../2023/assets/log-filter-settings.png "Se resaltan los nuevos filtros de registro de consultas."){width="100" zoomable="yes"} <br> Consulte la [documentación de registros de consulta](../../query-service/ui/query-logs.md#filter-logs) para obtener más información. |
| Varias actualizaciones de la IU del Editor de consultas | Ahora puede Ejecutar varias consultas secuenciales en el Editor de consultas o escribir más de una consulta y ejecutar todas las consultas de forma secuencial. Para añadir más flexibilidad a la ejecución de la consulta, puede resaltar la consulta elegida y seleccionar esa consulta específica para que se ejecute de forma independiente de las demás. Consulte la [guía de la interfaz de usuario del editor de consultas](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, vea la [Información general del servicio de consulta](../../query-service/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Experience Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Columnas personalizables | Ahora puede personalizar el diseño de Audience Portal con columnas cuyo tamaño se puede cambiar. Para obtener más información sobre esta característica, lea la [descripción general del portal de audiencia](../../segmentation/ui/audience-portal.md#customize). |
| Desglose de frecuencia de actualización | Ahora puede ver un desglose de las frecuencias de actualización de las audiencias de su organización. Para obtener más información sobre esta característica, lea la [guía de segmentación de la interfaz de usuario](../../segmentation/ui/overview.md#browse). |

Para obtener más información sobre el servicio de segmentación, lea la [descripción general del servicio de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevos parámetros para la paginación de `offset` en orígenes de autoservicio (SDK por lotes) | Ahora puede especificar `endConditionName` y `endConditionValue` para el origen al usar la paginación de `offset`. Estos parámetros le permiten indicar la condición que debe finalizar el bucle de paginación en la siguiente solicitud HTTP. Para obtener más información, lea la [guía de paginación para orígenes de autoservicio (SDK por lotes)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea [información general de fuentes](../../sources/home.md).
