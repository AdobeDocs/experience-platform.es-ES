---
title: Notas de la versión de Adobe Experience Platform, enero de 2022
description: Notas de la versión de enero de 2022 para Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 3%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de enero de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Servicio de consultas](#query-service)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Platform. Puede suscribirse a distintas reglas de alerta a través de la [!UICONTROL Alertas] en la interfaz de usuario de Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o mediante notificaciones por correo electrónico.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas reglas de alerta | Ya hay disponibles varias reglas de alerta nuevas para flujos de trabajo relacionados con la ingesta de datos, identidades, perfiles, segmentación y activación. Consulte la descripción general sobre [reglas de alerta](../../observability/alerts/rules.md) para la lista actualizada de tipos de alertas. |
| Alertas en contexto para flujos de datos de origen | Ahora puede suscribirse para recibir mensajes de alerta sobre el estado de sus flujos de datos durante el flujo de trabajo de ingesta. Para obtener más información, consulte la guía de [suscripción a alertas de fuentes en la interfaz de usuario](../../sources/tutorials/ui/alerts.md). |

Para obtener más información sobre las alertas en Platform, consulte la [información general sobre alertas](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| Subtítulos inteligentes | Un algoritmo de aprendizaje automático proporciona automáticamente perspectivas sobre sus datos de perfil y audiencia, e ilustra patrones y tendencias durante un período de 30 a 90 días o 12 meses. Los subtítulos incluyen información sobre <ul><li>Forma general y estadísticas</li><li>Tendencias y cambios bruscos</li><li>Patrones estacionales</li><li>Anomalías inesperadas</li></ul> Puede encontrar más información en la [tableros de perfiles](../../dashboards/guides/profiles.md#profiles-count-trend) y [tableros de segmentos](../../dashboards/guides/segments.md#audience-size-trend) documentación. |
| Inventario de tableros | Acceda a los informes preconfigurados de paneles de perfil, segmentos y destinos, incluidas las integraciones instaladas, como Power BI, en una ubicación centralizada. Para obtener más información, consulte la [[!DNL Dashboards] documentación de inventario](../../dashboards/inventory.md). |
| Plantillas de informe de PowerBI | Cree, personalice o amplíe métricas a partir de los modelos de datos de informes de perfil, segmentos y destino usando los nuevos gráficos de Power BI. El flujo de trabajo de instalación automatizada le permite compartir sus perspectivas de marketing en su organización desde el entorno de PowerBI. Para obtener más información, consulte la [Documentación de plantilla de informe de PowerBI](../../dashboards/integrations/power-bi.md). |

Para obtener más información, consulte [!DNL Dashboards], consulte la [[!DNL Dashboards] información general](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Experiencia de asignación consolidada | La nueva interfaz de asignación en la interfaz de usuario de Platform le ofrece una experiencia de asignación coherente para aprovechar las recomendaciones de asignación inteligente, configurar manualmente las reglas de asignación y depurar cualquier error que se produzca en los conjuntos de asignación. Para obtener más información, consulte la [[!DNL Data Prep] Guía de la interfaz de usuario](../../data-prep/ui/mapping.md). |

Para obtener más información, consulte [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Personalización de la misma página y de la página siguiente | La variable [función de personalización de la misma página y de la siguiente página](../../destinations/ui/configure-personalization-destinations.md) proporciona una vista compartida y objetivo de los usuarios para las aplicaciones en Experience Edge, para mantener la coherencia entre los canales de marketing y del cliente. Esta personalización es posible a través del [Conexión Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y [Conexión personalizada personalizada](../../destinations/catalog/personalization/custom-personalization.md). Para configurar las campañas de personalización de la misma página o de la página siguiente, consulte la [tutorial dedicado](../../destinations/ui/configure-personalization-destinations.md). |
| Supervisión del destino por lotes y métricas a nivel de segmento | La funcionalidad de monitorización de destino ahora se expande de los destinos de flujo continuo a también incluye destinos de lote y métricas de nivel de segmento para los flujos de datos de activación. Para obtener más información, lea [panel de destinos de monitorización](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [monitorización del panel de trabajos de segmentos](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard)y [vista de nivel de segmento](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Programar la edición en la interfaz de usuario para flujos de datos de activación por lotes existentes | Esta versión introduce la opción de editar la programación de los flujos de datos de activación existentes en destinos por lotes. Para obtener más información, lea [activar datos de perfil en destinos de perfil por lotes](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Mejoras de destino de Marketo | Los clientes Experience Platform que utilizan Marketo Engage pueden maximizar su base de datos Marketo con la nueva capacidad de insertar registros de personas nuevas en el Marketo Engage desde el Experience Platform a través del [Conector de destino de Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Al enviar segmentos de audiencia de Experience Platform a Marketo Engage, se pueden añadir automáticamente personas dentro del segmento que no existan en la base de datos de Marketo Engage. Para obtener más información, lea [Insertar un segmento de Adobe Experience Platform en una lista estática de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (el paso 9 del tutorial indica cómo insertar registros de persona nueva en Marketo). |

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [Conexión Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target es una aplicación que proporciona personalización y experimentación en tiempo real con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más. Adobe Target es una conexión personalizada en Adobe Experience Platform. |
| [Conexión personalizada personalizada](../../destinations/catalog/personalization/custom-personalization.md) | Esta conexión de personalización proporciona una forma de recuperar información de segmentos de Adobe Experience Platform a plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en sitios web de clientes. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de consultas {#query-service}

[!DNL Query Service] permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y captura los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Bloque anónimo | La construcción SQL de bloque anónimo permite desglosar los trabajos de preparación de datos a gran escala en el servicio de consulta en tareas más pequeñas y, a continuación, reutilizarlos y ejecutarlos en secuencia para la carga de datos incremental. Para obtener más información, consulte la [consultas de ejemplo para documentación de bloques anónimos](../../query-service/best-practices/anonymous-block.md). |
| Organización de conjuntos de datos | Proporciona una estructura de datos lógica y coherente para organizar los recursos de datos y utilizarlos con el servicio de consulta a medida que crezca la cantidad de recursos de datos dentro del entorno limitado. Para obtener más información, consulte la [organizar la documentación de recursos de datos](../../query-service/best-practices/organize-data-assets.md). |

Para obtener más información, consulte [!DNL Query Service], consulte la [[!DNL Query Service] información general](../../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la interfaz de usuario de los Simuladores para pruebas | El indicador del simulador para pruebas ahora está integrado en el encabezado de todas las aplicaciones de interfaz de usuario de Platform. El indicador del simulador de pruebas muestra el nombre, la región y el tipo del simulador de pruebas, y también le permite acceder a un menú desplegable para alternar entre entornos limitados. Para obtener más información, consulte la [guía de la interfaz de usuario de sandbox](../../sandboxes/ui/user-guide.md). |

Para obtener más información sobre los entornos limitados, consulte la [información general sobre los entornos limitados](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Coincidencia de segmentos | Segment Match es un servicio de colaboración de datos que permite a dos o más usuarios de Platform intercambiar datos, en función de identificadores comunes, de forma segura, regulada y compatible con la privacidad. La coincidencia de segmentos utiliza estándares de privacidad de plataforma e identificadores personales como correos electrónicos con hash, números de teléfono con hash y identificadores de dispositivo como IDFA y GAID. Para obtener más información, consulte la [Información general sobre la coincidencia de segmentos](../../segmentation/ui/segment-match/overview.md). |

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] mejoras de la fuente | La variable [!DNL Event Hubs] el origen ahora admite un tipo de autenticación de clave SAS no raíz para conectarse y crear una conexión de origen. Para obtener más información, consulte la [[!DNL Event Hubs] información general](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] mejoras de la fuente | La variable [!DNL SFTP] source ahora le permite establecer un número establecido de conexiones simultáneas máximas que un flujo de datos puede utilizar para conectarse al servidor SFTP. Para obtener más información, consulte la [[!DNL SFTP] información general](../../sources/connectors/cloud-storage/sftp.md). |
