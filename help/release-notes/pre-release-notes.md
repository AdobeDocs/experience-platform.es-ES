---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

---

# Notas previas al lanzamiento de Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento está diseñado como **vista previa** de las notas de la versión del mes actual. Los elementos de la versión están sujetos a cambios y se pueden añadir o eliminar en la versión final.

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: marzo de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Administración avanzada del ciclo de vida de los datos](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Destinos](#destinations)
- [Servicio de consultas](#query-service)
- [Perfil del cliente en tiempo real](#profile)
- [Ejecutar y operar](#run-and-operate)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Administración avanzada del ciclo de vida de los datos {#advanced-data-lifecycle-management}

Experience Platform proporciona un conjunto de funcionalidades de higiene de datos que le permiten administrar los datos almacenados mediante eliminaciones programáticas de registros de consumidores y conjuntos de datos. Con el espacio de trabajo de Data Lifecycle en la interfaz de usuario o a través de llamadas a la API de Data Hygiene, puede administrar de forma eficaz los almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas organizativas lo consideran necesario.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Eliminación de registros solo de perfil y de conjuntos de datos múltiples (solo API) | Puede enviar un solo ID de conjunto de datos, una lista de ID de conjunto de datos separados por comas o el literal `ALL` en `datasetId` para eliminar identidades en uno, varios o todos los conjuntos de datos. También puede limitar la eliminación a los servicios de perfil estableciendo `targetServices` en `["identity","profile","ajo"]`, lo que no modifica el conjunto de datos. Consulte la [Guía de eliminación de registros de órdenes de trabajo](../hygiene/api/workorder.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [información general de la administración avanzada del ciclo de vida de los datos](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator le permite crear e implementar agentes con tecnología de IA que pueden automatizar flujos de trabajo e interactuar con los clientes en varios canales.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] | Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] es su agente incrustado que incorpora el conocimiento de marketing de Adobe directamente en herramientas cotidianas como [!DNL Teams], [!DNL Word], [!DNL PowerPoint] y otras aplicaciones de [!DNL Microsoft 365]. Puede utilizar este agente para extraer información de campañas de confianza de aplicaciones de Adobe mientras planea campañas, revisa audiencias o colabora con compañeros, responde a preguntas de clientes y toma decisiones basadas en datos sin abandonar el flujo de trabajo de [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Para obtener más información, consulte la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [Lote de Snowflake](../destinations/catalog/warehouses/snowflake-batch.md) selector de región | Ahora puede encontrar su región más fácilmente con la nueva lista desplegable de búsqueda, que combina la búsqueda y la lista desplegable en un control. |
| Exportar metadatos de audiencia a [destinos por lotes de Snowflake](../destinations/catalog/warehouses/snowflake-batch.md) | Los archivos exportados a este destino ahora incluyen metadatos de audiencia. La nueva estructura de tabla se aplica a todas las conexiones de destino nuevas configuradas a partir de ahora. La estructura de tabla antigua se mantendrá durante otros tres meses antes de quedar obsoleta. |
| [!DNL Adobe Advertising Cloud DSP] conexión | La nueva conexión de Adobe Advertising DSP ofrece la misma funcionalidad que la conexión heredada, además de compatibilidad con identidades adicionales. |
| Compatibilidad con audiencias externas para [The Trade Desk CRM](../destinations/catalog/advertising/tradedesk-emails.md), [Criteo](../destinations/catalog/advertising/criteo.md) y [Pinterest](../destinations/catalog/advertising/pinterest.md) | Ahora puede activar audiencias que vayan más allá de los segmentos del servicio de segmentación en Trade Desk CRM, Criteo y Pinterest, incluidas las audiencias de carga personalizadas (importadas desde CSV), audiencias de similitud, audiencias federadas y audiencias creadas en otras aplicaciones de Experience Platform como Adobe Journey Optimizer. Consulte la sección [audiencias admitidas](../destinations/catalog/advertising/criteo.md#supported-audiences) en la página del catálogo de cada destino para obtener más información. |
| Límite de audiencias de carga personalizada aumentado | Ahora puede activar hasta 20 audiencias de carga personalizadas por instancia de destino. Anteriormente, este límite era de 10. |
| [Exportar archivo ahora](../destinations/ui/export-file-now.md) y [compatibilidad con la API de activación ad hoc](../destinations/api/ad-hoc-activation-api.md) para audiencias externas | Ahora puede utilizar la interfaz de usuario y la API de activación ad-hoc de Exportar archivo ahora con audiencias externas (como carga personalizada, similitud, federación y audiencias de otras aplicaciones de Experience Platform) al activar en destinos basados en archivos por lotes. |
| Destinos de API HTTP con OAuth 2 y mTLS | Ahora puede crear y autenticar destinos de API HTTP que utilicen OAuth 2 cuando el extremo de autenticación requiera TLS mutuo (mTLS); la recuperación de tokens durante la configuración de destino ahora admite mTLS. |
| Destino de cuenta de ZoomInfo | Ahora puede enviar audiencias de cuenta a ZoomInfo desde Real-Time Customer Data Platform (B2B). |

{style="table-layout:auto"}

**Correcciones y mejoras**

| Se ha corregido un problema que hacía que se mostrara | Descripción |
| --- | --- |
| Validación de ID de cuenta de [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) | Se ha agregado un validador de expresiones regulares al paso ID de cuenta. Al introducir su ID, ahora se valida para garantizar que el ID de organización y el ID de cuenta tengan el formato correcto (separados por un punto). |
| hash del número de teléfono del conector [TikTok](../destinations/catalog/social/tiktok.md) | Se ha corregido un problema por el cual una configuración incorrecta en la tarjeta de destino significaba que las identidades marcadas desde números de teléfono no se activaban en TikTok. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Selector de tiempo de eventos de perfil | Ahora puede establecer una ventana de tiempo en la pestaña de eventos de perfil para ver y analizar eventos dentro de ese intervalo. Puede establecer la ventana de tiempo en un máximo de 30 días. De forma predeterminada, muestra los eventos de las últimas 48 horas. |

{style="table-layout:auto"}

Para obtener más información, lea la [información general sobre el perfil del cliente en tiempo real](../profile/home.md).

## Servicio de consultas {#query-service}

El Servicio de consultas le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Data Distiller Accelerators | Ahora puede seleccionar un acelerador de la pestaña Aceleradores, introducir los parámetros necesarios y ejecutar o programar el SQL generado sin escribirlo usted mismo; clone cualquier acelerador en una plantilla personalizada para editarlo. |

{style="table-layout:auto"}

Para obtener más información, lea [Introducción al servicio de consultas](../query-service/home.md).

## Ejecutar y operar {#run-and-operate}

Inspeccione, solucione problemas y optimice las implementaciones de Experience Platform con las herramientas Ejecutar y operar. Obtenga visibilidad sobre las activaciones por lotes programadas, identifique los problemas de configuración y mejore la fiabilidad del sistema.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de [horarios de trabajo](../run-and-operate/job-schedules.md) | [!DNL Job Schedules] proporciona una vista unificada de todos los trabajos de procesamiento por lotes programados en toda la canalización de datos, desde la ingesta hasta la activación de destino. Inspeccione el estado de ejecución, identifique los conflictos de programación y diagnostique los problemas de configuración antes de que afecten a las operaciones empresariales. |
| Comprobación de estado disponibilidad general | Las configuraciones de esquema e identidad deficientes derivan en problemas descendentes significativos, como la creación incorrecta de perfiles, la calificación fallida de segmentos y la activación inexacta. <br>Las comprobaciones de estado cambian su enfoque de la solución de problemas reactiva al mantenimiento preventivo y proactivo. Las comprobaciones de estado son análisis siempre activos de los esquemas e identidades utilizados en la zona protegida y proporcionan un resumen de los problemas que puede utilizar para explorar y solucionar problemas. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre la ejecución y el funcionamiento](../run-and-operate/overview.md), [Inspeccionar las programaciones de trabajos](../run-and-operate/job-schedules.md) y la [guía de la interfaz de usuario de la plataforma](../landing/ui-guide.md).

## Servicio de segmentación {#segmentation}

Experience Platform le permite crear segmentos de audiencia a partir de los datos de sus clientes y permite una administración completa del ciclo de vida de esas audiencias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Fuente de ingesta en el Generador de audiencias | Ahora puede ver si cada atributo proviene de un lote, una transmisión por secuencias o un origen perimetral dentro de Audience Builder para evitar la creación de audiencias de transmisión por secuencias no válidas o ineficientes. |
| Mostrar solo campos con datos en el Generador de audiencias de cuenta | Ahora puede filtrar para mostrar solo los atributos que contienen datos al crear audiencias de cuenta. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre audiencias](../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| Compatibilidad mejorada con la captura de datos modificados | Ahora puede usar Cambiar captura de datos con los orígenes [!DNL Marketo Engage], [!DNL Microsoft Dynamics] y [!DNL Salesforce CRM]. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->