---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2026'
description: Las notas de la versión de marzo de 2026 de Adobe Experience Platform.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 30b66420e9cee6b4d85cf41a31e9595d5a240fda
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 32%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: miércoles, 24 de marzo de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Administración avanzada del ciclo de vida de los datos](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Corrientes de datos](#datastreams)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#real-time-customer-profile)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Administración avanzada del ciclo de vida de los datos {#advanced-data-lifecycle-management}

Experience Platform proporciona un conjunto de funcionalidades de higiene de datos que le permiten administrar los datos almacenados mediante eliminaciones programáticas de registros de consumidores y conjuntos de datos. Con el espacio de trabajo del ciclo vital de datos en la interfaz de usuario o las llamadas a la API de higiene de datos, puede administrar de forma eficaz los almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas organizativas lo consideran necesario.

| Función | Descripción |
| --- | --- |
| Eliminación de registros solo de perfil y de varios conjuntos de datos (solo API) | Puede enviar un solo ID de conjunto de datos, una lista de ID de conjunto de datos separados por comas o el literal `ALL` en `datasetId` para eliminar identidades en uno, varios o todos los conjuntos de datos. También puede limitar la eliminación a los servicios relacionados con perfiles estableciendo `targetServices` en `["identity","profile","ajo"]`, lo que no modifica el conjunto de datos; esta funcionalidad solo está disponible a través de la API de higiene de datos. Consulte la [Guía de eliminación de pedidos de trabajo](../../hygiene/api/workorder.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [información general de la administración avanzada del ciclo de vida de los datos](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator le permite crear e implementar agentes con tecnología de IA que pueden automatizar flujos de trabajo e interactuar con los clientes en varios canales.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [Adobe Marketing Agent para [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] es su agente incrustado que incorpora el conocimiento de marketing de Adobe directamente en herramientas cotidianas como [!DNL Teams], [!DNL Word], [!DNL PowerPoint] y otras aplicaciones de [!DNL Microsoft 365]. Puede utilizar este agente para extraer información de campañas de confianza de las aplicaciones de Adobe mientras planea campañas, revisa audiencias y colabora con compañeros para responder preguntas de clientes y tomar decisiones basadas en datos sin abandonar el flujo de trabajo de [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Para obtener más información, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Corrientes de datos {#datastreams}

Un conjunto de datos representa la configuración del lado del servidor al implementar los SDK web y móvil de Adobe Experience Platform y la API de servidor de Adobe Experience Platform Edge Network. El comando de configuración de la secuencia de datos en los SDK gestiona todos los servicios con los que interactúa un cliente.

| Función | Descripción |
| --- | --- |
| Disponibilidad general de las configuraciones de flujo de datos dinámico | Ya están disponibles de forma general las configuraciones de flujo de datos dinámico. Las configuraciones de flujo de datos dinámico le permiten definir conjuntos de reglas configurables por el usuario para cada servicio habilitado para el flujo de datos, que dictan qué solución de Experience Cloud debe recibir cada tipo de datos. Consulte la [guía de configuraciones de secuencia de datos dinámica](../../datastreams/configure-dynamic-datastream.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de flujos de datos](../../datastreams/overview.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [Conexión de Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | La nueva conexión de Adobe Advertising DSP ofrece la misma funcionalidad que la conexión heredada, además de compatibilidad con identidades adicionales. Con el nuevo conector, también puede exportar identidades basadas en cookies a Adobe Advertising DSP. |
| Conexión de [FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Envíe audiencias de [!DNL Real-Time CDP] a FreeWheel como archivos por lotes diarios para que pueda segmentarlas en ofertas y campañas de FreeWheel en CTV, vídeo y pantalla. Póngase en contacto con el equipo de su cuenta de Adobe para obtener acceso. |
| Compatibilidad con audiencias externas para [The Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) y [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Ahora puede activar audiencias desde orígenes que van más allá del servicio de segmentación hasta Trade Desk CRM, Criteo y Pinterest, incluidas audiencias de carga personalizadas (importadas desde CSV), audiencias similares, audiencias federadas y audiencias creadas en otras aplicaciones de Experience Platform como [!DNL Adobe Journey Optimizer]. Esta actualización se estará publicando hasta finales de marzo. Consulte la sección [audiencias admitidas](../../destinations/catalog/advertising/criteo.md#supported-audiences) en la página del catálogo de cada destino para obtener más información. |
| Se ha aumentado el límite de audiencias de carga personalizadas | Ahora puede activar hasta 20 audiencias de carga personalizadas por instancia de destino. Anteriormente, este límite era de 10. Consulte las [protecciones de destinos](../../destinations/guardrails.md#batch-file-based-activation) para obtener más información. |
| [Exportar archivo ahora](../../destinations/ui/export-file-now.md) y [compatibilidad con la API de activación ad hoc](../../destinations/api/ad-hoc-activation-api.md) para audiencias externas | Ahora puede utilizar la interfaz de usuario y la API de activación ad-hoc de Exportar archivo ahora con audiencias externas (como carga personalizada, similitud, federación y audiencias de otras aplicaciones de Experience Platform) al activar en destinos basados en archivos por lotes. Esta actualización se estará publicando hasta finales de marzo. |

{style="table-layout:auto"}

**Correcciones y mejoras**

| Se ha corregido un problema que hacía que se mostrara | Descripción |
| --- | --- |
| hash del número de teléfono del conector [TikTok](../../destinations/catalog/social/tiktok.md) | Se ha corregido un problema por el cual una configuración incorrecta en la tarjeta de destino significaba que las identidades marcadas desde números de teléfono no se activaban en TikTok. Para beneficiarse de esta corrección, configure un nuevo flujo de activación o elimine la asignación del número de teléfono del flujo existente, guárdelo y agréguelo de nuevo. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

| Función | Descripción |
| --- | --- |
| Acciones de entidad XDM y compatibilidad de eliminación | Acceda a acciones para esquemas, clases, grupos de campos y tipos de datos directamente desde menús de tablas en línea y menús de encabezados de páginas de detalles. Si tiene los permisos necesarios, también puede eliminar las entidades de su organización cuando no las utilicen los conjuntos de datos y no estén habilitadas para el perfil. Consulte la [guía de la interfaz de usuario de XDM](../../xdm/ui/explore.md) para obtener más información. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#real-time-customer-profile}

El perfil del cliente en tiempo real permite ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Eventos | Ahora puede establecer el período retroactivo de eventos al examinar los perfiles. Esto le permite ver los eventos a los que está asociado el perfil para el período de tiempo especificado. Para obtener más información, lea la [guía de la interfaz de usuario del perfil](/help/profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Real-Time Customer Profile] información general](../../profile/home.md).

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Tipo de ingesta | Ahora puede ver el tipo de ingesta de sus atributos. Esto le permite conocer el origen de los datos y crear mejores audiencias. Para obtener más información acerca de esta característica, lea la [guía del Generador de segmentos](/help/segmentation/ui/segment-builder.md). |
| Datos de resumen | Ahora puede ver los datos de resumen de los atributos de las audiencias basadas en cuentas y personas. Para obtener más información acerca de esta característica en las audiencias de la cuenta, lea la cuenta [Guía del generador de audiencias](/help/rtcdp/segmentation/audience-builder.md). Para obtener más información sobre esta característica en audiencias basadas en personas, lee la [guía del Generador de segmentos](/help/segmentation/ui/segment-builder.md). |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| [!DNL Talon.One] | Ahora puede conectar Experience Platform a [!DNL Talon.One] con las nuevas fuentes [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) y [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Utilice las nuevas fuentes para introducir datos del perfil de lealtad, así como eventos de transacciones y actividades de lealtad en Experience Platform. |
| Nuevas direcciones IP para la lista de permitidos | Nuevas direcciones IP para GBR9: Reino Unido se han añadido a la lista de direcciones que debe lista de permitidos para garantizar conexiones de origen por lotes correctas a Experience Platform en Azure. Vea la lista en la [guía de lista de permitidos de direcciones IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) para obtener más información. |
| Compatibilidad mejorada con la captura de datos modificados | Ahora puede usar Cambiar captura de datos con los orígenes [!DNL Marketo Engage], [!DNL Microsoft Dynamics] y [!DNL Salesforce CRM]. |
| Guía de autenticación mejorada para [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | La guía de autenticación para el origen [!DNL Google BigQuery] se ha expandido con la siguiente información: <ul><li>Los ámbitos necesarios para el token de actualización.</li><li>Los roles de IAM necesarios para la identidad [!DNL Google].</li><li>Instrucciones adicionales sobre el uso de `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->
