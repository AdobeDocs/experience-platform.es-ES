---
title: Notas de la versión de Adobe Experience Platform, enero de 2022
description: Notas de la versión de enero de 2022 de Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
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

Experience Platform permite suscribirse a alertas basadas en eventos para diversas actividades de Platform. Puede suscribirse a diferentes reglas de alerta a través de la variable [!UICONTROL Alertas] en la interfaz de usuario de Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o a través de notificaciones por correo electrónico.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas reglas de alerta | Ya hay disponibles varias reglas de alerta nuevas para los flujos de trabajo relacionados con la ingesta de datos, identidades, perfiles, segmentación y activación. Consulte la información general sobre [reglas de alerta](../../observability/alerts/rules.md) para obtener la lista actualizada de tipos de alerta. |
| Alertas en contexto para flujos de datos de origen | Ahora puede suscribirse para recibir mensajes de alerta con respecto al estado de los flujos de datos durante el flujo de trabajo de ingesta. Para obtener más información, consulte la guía de [suscripción a alertas de fuentes en la IU](../../sources/tutorials/ui/alerts.md). |

Para obtener más información sobre las alertas en Platform, consulte la [información general sobre alertas](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| Pies de ilustración inteligentes | Un algoritmo de aprendizaje automático proporciona automáticamente información sobre sus datos de perfil y audiencia, e ilustra patrones y tendencias en un periodo de 30 a 90 días o 12 meses. Los subtítulos incluyen información sobre <ul><li>Forma general y estadísticas</li><li>Tendencias y cambios abruptos</li><li>Patrones estacionales</li><li>Anomalías inesperadas</li></ul> Encontrará más información en la [paneles de perfiles](../../dashboards/guides/profiles.md#profiles-count-trend) y [paneles de segmentos](../../dashboards/guides/segments.md#audience-size-trend) documentación. |
| Inventario de paneles | Acceda a los informes preconfigurados de paneles de perfiles, segmentos y destinos, incluidas las integraciones instaladas como Power BI, en una ubicación centralizada. Para obtener más información, consulte la [[!DNL Dashboards] documentación de inventario](../../dashboards/inventory.md). |
| Plantillas de informe de Power BI | Cree, personalice o amplíe métricas a partir de los modelos de datos de perfil, segmentos y sistemas de informes de destino con nuevos gráficos de Power BI. El flujo de trabajo de instalación automatizada le permite compartir sus perspectivas de marketing con toda su organización desde el entorno de Power BI. Para obtener más información, consulte la [Documentación de plantilla de informe de Power BI](../../dashboards/integrations/power-bi.md). |

Para obtener más información sobre [!DNL Dashboards], consulte la [[!DNL Dashboards] descripción general](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Experiencia de asignación consolidada | La nueva interfaz de asignación de la IU de Platform le ofrece una experiencia de asignación coherente para aprovechar las recomendaciones de asignación inteligente, configurar manualmente las reglas de asignación y depurar cualquier error que se produzca en los conjuntos de asignación. Para obtener más información, consulte la [[!DNL Data Prep] Guía de IU](../../data-prep/ui/mapping.md). |

Para obtener más información sobre [!DNL Data Prep], consulte la [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Personalización de la misma página y de la página siguiente | El [función de personalización de la misma página y de la siguiente página](../../destinations/ui/activate-edge-personalization-destinations.md) proporciona una vista compartida y dirigida de los usuarios de las aplicaciones Experience Edge, para mantener la coherencia entre los canales de marketing y los de los clientes. Esta personalización es posible a través de [Conexión de Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y el [Conexión de personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md). Para configurar sus campañas de personalización de la misma página o de la página siguiente, consulte la [tutorial dedicado](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Monitorización de destino de lotes y métricas de nivel de segmento | La funcionalidad de monitorización de destino ahora se expande desde los destinos de streaming para incluir también destinos por lotes y métricas de nivel de segmento para los flujos de datos de activación. Para obtener más información, consulte [panel de supervisión de destinos](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [panel monitorización de trabajos de segmentos](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), y [vista de nivel de segmento](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Programar la edición en la IU para flujos de datos de activación por lotes existentes | Esta versión introduce la opción de editar la programación de los flujos de datos de activación existentes para los destinos por lotes. Para obtener más información, consulte [activar datos de perfil en destinos de perfil por lotes](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Mejoras de destino de Marketo | Los clientes de Experience Platform que utilizan Marketo Engage pueden maximizar su base de datos de Marketo con la nueva capacidad de insertar nuevos registros de persona netos en Marketo Engage desde Experience Platform a través de [Conector de destino de Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Al enviar segmentos de audiencia de Experience Platform a Marketo Engage, se pueden agregar automáticamente a él personas dentro del segmento que no existan en la base de datos de Marketo Engage. Para obtener más información, consulte [Insertar un segmento de Adobe Experience Platform en una lista estática de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (el paso 9 del tutorial indica cómo insertar nuevos registros de persona en Marketo). |

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [Conexión de Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target es una aplicación que proporciona personalización y experimentación en tiempo real impulsada por IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más. Adobe Target es una conexión de personalización en Adobe Experience Platform. |
| [Conexión de personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md) | Esta conexión de personalización proporciona una forma de recuperar información de segmentos de Adobe Experience Platform para plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en los sitios web de los clientes. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de consultas {#query-service}

[!DNL Query Service] permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unir cualquier conjunto de datos de [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para usar en sistema de informes, espacio de trabajo de ciencia de datos o para su inserción en el perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Bloque anónimo | La construcción SQL de bloque anónimo le permite desglosar trabajos de preparación de datos a gran escala en Query Service en tareas más pequeñas y luego reutilizarlos y ejecutarlos en secuencia para la carga de datos incrementales. Para obtener más información, consulte la [consultas de muestra para documentación de bloques anónimos](../../query-service/essential-concepts/anonymous-block.md). |
| Organización del conjunto de datos | Proporciona una estructura de datos lógica y coherente para organizar los recursos de datos y utilizarlos con el servicio de consultas a medida que aumenta la cantidad de recursos de datos dentro de la zona protegida. Para obtener más información, consulte la [documentación de organización de recursos de datos](../../query-service/best-practices/organize-data-assets.md). |

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] descripción general](../../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras de IU de Sandboxes | El indicador de zona protegida ahora está integrado en el encabezado para todas las aplicaciones de IU de Platform. El indicador de zona protegida muestra el nombre, la región y el tipo de la zona protegida y también le permite acceder a un menú desplegable para cambiar entre zonas protegidas. Para obtener más información, consulte la [guía de IU de sandbox](../../sandboxes/ui/user-guide.md). |

Para obtener más información sobre los entornos limitados, consulte la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Coincidencia de segmentos | La coincidencia de segmentos es un servicio de colaboración de datos que permite a dos o más usuarios de Platform intercambiar datos, basados en identificadores comunes, de una manera segura, controlada y compatible con la privacidad. La coincidencia de segmentos utiliza estándares de privacidad de Platform e identificadores personales como correos electrónicos con hash, números de teléfono con hash e identificadores de dispositivo como IDFA y GAID. Para obtener más información, consulte la [Resumen de coincidencia de segmentos](../../segmentation/ui/segment-match/overview.md). |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Fuentes beta que se trasladan a GA | Las siguientes fuentes se han promocionado de beta a GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] mejoras de origen | El [!DNL Event Hubs] El origen ahora admite el tipo de autenticación de clave SAS no raíz para conectarse y crear una conexión de origen. Para obtener más información, consulte la [[!DNL Event Hubs] descripción general](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] mejoras de origen | El [!DNL SFTP] El origen de ahora permite establecer un número establecido de un máximo de conexiones simultáneas que un flujo de datos puede utilizar para conectarse al servidor SFTP. Para obtener más información, consulte la [[!DNL SFTP] descripción general](../../sources/connectors/cloud-storage/sftp.md). |
