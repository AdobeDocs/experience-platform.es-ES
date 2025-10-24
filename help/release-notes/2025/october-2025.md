---
title: 'Notas de la versión de Adobe Experience Platform: octubre de 2025'
description: Las notas de la versión de octubre de 2025 de Adobe Experience Platform.
source-git-commit: 7f37ba35111f6fa96d1889d74a66e32302b8ab85
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 24%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: jueves, 22 de octubre de 2025**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Alertas](#alerts)
- [Destinos](#destinations)
- [Orígenes](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator es la nueva capa agéntica de Adobe Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Audience Agent | Audience Agent ahora admite audiencias basadas en cuentas para la exploración de audiencias conversacionales y la detección de audiencias duplicadas. Para obtener más información, lea la [documentación de Audience Agent](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Para obtener más información sobre los agentes, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/home).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a distintas reglas de alerta a través de la ficha [!UICONTROL Alerts] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o mediante notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Alerta de tasa de error de activación | Se ha agregado una nueva alerta para los destinos: **La tasa de errores de activación supera el umbral**. Esta alerta le notifica cuando el número de registros con errores durante la activación de datos ha superado el umbral permitido, lo que le permite responder rápidamente a los problemas de activación. Lea la documentación sobre [reglas de alertas estándar](../../observability/alerts/rules.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [!DNL Adform] | Use este destino para enviar audiencias de Adobe Real-Time CDP a [!DNL Adform] para su activación en función del Experience Cloud ID (ECID) y del ID Fusion de [!DNL Adform]. ID Fusion de [!DNL Adform] es un servicio de resolución de ID que le permite activar audiencias de origen basadas en el Experience Cloud ID (ECID). Lea la [[!DNL Adform] documentación](../../destinations/catalog/advertising/adform.md) para obtener más información |
| [!DNL Amazon Ads] | Se ha añadido compatibilidad con identificadores personales adicionales. Esto incluye campos como `firstName`, `lastName`, `street`, `city`, `state`, `zip` y `country`. La asignación de estos campos como identidades de destino puede mejorar las tasas de coincidencia de audiencia. Lea la [[!DNL Amazon Ads] documentación](../../destinations/catalog/advertising/amazon-ads.md) para obtener más información. |
| [!DNL Snowflake Batch] (disponibilidad limitada) | Cree un recurso compartido de datos de [!DNL Snowflake] activo para recibir actualizaciones diarias de la audiencia directamente como tablas compartidas en su cuenta. Actualmente, esta integración está disponible para las organizaciones de clientes aprovisionadas en la región de VA7. Lea la [[!DNL Snowflake Batch] documentación](../../destinations/catalog/warehouses/snowflake-batch.md) para obtener más información. |
| [!DNL Snowflake Streaming] (disponibilidad limitada) | Cree un recurso compartido de datos de [!DNL Snowflake] activo para recibir actualizaciones de audiencia de streaming directamente como tablas compartidas en su cuenta. Actualmente, esta integración está disponible para las organizaciones de clientes aprovisionadas en la región de VA7. Lea la [[!DNL Snowflake Streaming] documentación](../../destinations/catalog/warehouses/snowflake.md) para obtener más información. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| [Varios destinos nuevos que admiten la supervisión a nivel de audiencia](../../dataflows/ui/monitor-destinations.md#audience-level-view) | Los siguientes destinos ahora admiten la monitorización a nivel de audiencia: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] participación de cuenta</li><li>[!DNL The Trade Desk]</li></ul> |
| Corrección de protecciones de exportación de conjuntos de datos | Se ha implementado una corrección en las protecciones de exportación del conjunto de datos. Anteriormente, algunos conjuntos de datos que incluían una columna de marca de tiempo pero que _no eran_ basados en el esquema de eventos de experiencia XDM se trataban incorrectamente como conjuntos de datos de eventos de experiencia, lo que limitaba las exportaciones a una ventana retrospectiva de 365 días. La protección retrospectiva de 365 días documentada ahora se aplica exclusivamente a los conjuntos de datos de eventos de experiencia. Los conjuntos de datos que utilizan cualquier esquema distinto del esquema de eventos de experiencia XDM ahora se rigen por la protección de 10 000 millones de registros. Es posible que algunos clientes vean números de exportación aumentados para conjuntos de datos que, erróneamente, caen dentro de la ventana retrospectiva de 365 días. Esto permite exportar conjuntos de datos para flujos de trabajo predictivos que tienen una larga ventana retrospectiva. Para obtener más información, lea las [protecciones de exportación del conjunto de datos](../../destinations/guardrails.md#dataset-exports). |
| Informes mejorados a nivel de audiencia para destinos empresariales | Después de esta versión, los clientes verán números de informes de audiencia más precisos que incluyen solo audiencias relevantes para el destino seleccionado. Este ajuste de monitorización garantiza que la creación de informes incluya solo audiencias asignadas en el flujo de datos, lo que proporciona una perspectiva más clara de la activación de datos real. Esto no afecta a la cantidad de datos que se activan, se trata simplemente de una mejora de la monitorización para mejorar la precisión de la creación de informes. |
| Flujos de datos desactivados en la IU debido a etiquetas de acceso | Para solucionar el problema de que algunos usuarios veían páginas en blanco porque los flujos de datos de destino a los que no tenían acceso estaban completamente ocultos, la interfaz de usuario ahora muestra esos flujos de datos restringidos en un estado atenuado en lugar de omitirlos por completo. Para obtener más información, lea la documentación sobre [uso de etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know). |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambio en la creación de conjuntos de datos para Adobe Analytics | Como parte del proceso de creación de flujo de datos entre Adobe Analytics y Experience Platform, se crea un conjunto de datos mediante el servicio de catálogo. Este conjunto de datos sirve como contenedor para que los datos aterricen. Actualmente, este proceso implica un ID de fuente de datos que se extrae del grupo de informes de Analytics, se envía al servicio de catálogo y, a continuación, se asocia al conjunto de datos recién creado. Después del cambio, la opción de proporcionar el ID de origen de datos dejará de estar disponible durante la creación del conjunto de datos. Por lo tanto, los nuevos conjuntos de datos creados por el origen de Analytics ya no tendrán un ID de origen de datos asociado en el servicio de catálogo. Este cambio se aplica solo a los metadatos y no cambia el almacenamiento de datos en el conjunto de datos de ninguna manera. Sin embargo, es importante saber que el ID de origen de datos proporcionado por el servicio de catálogo ya no estará disponible en los conjuntos de datos recién creados para Adobe Analytics. Lea la [documentación de origen de Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md) para obtener más información sobre el conector de origen de Adobe Analytics. |
| Disponibilidad general del origen [!DNL Google Ads] (solo API) | La [versión de API del origen  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md) está ahora en General Availability. La documentación de la API se ha actualizado para reflejar que la versión más reciente ahora es `v21`, y Experience Platform es compatible con todas las versiones v19 y posteriores. [La versión de la interfaz de usuario](../../sources/tutorials/ui/create/advertising/ads.md) permanece en la versión beta y solo admite la ingesta única. Para utilizar la ingesta de datos incremental, utilice la ruta de la API. |
| compatibilidad con la red virtual [!DNL Azure Event Hubs] | Adobe ahora admite explícitamente conexiones de red virtual a [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), lo que permite la transferencia de datos a través de redes privadas en lugar de redes públicas. Los clientes pueden realizar una lista de permitidos de Experience Platform VNet para enrutar el tráfico de los Event Hubs de forma privada a través de la red troncal privada de Azure, lo que proporciona una seguridad y un cumplimiento mejorados para los flujos de trabajo de ingesta de datos. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->