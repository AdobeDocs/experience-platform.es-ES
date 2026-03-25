---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2026'
description: Las notas de la versión de marzo de 2026 de Adobe Experience Platform.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 381d1f952067cece9f9a9618a00bbed304214906
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 20%

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

Experience Platform proporciona un conjunto de funciones de higiene de los datos para ayudarle a administrar los datos almacenados mediante la eliminación mediante programación de registros de consumidores y conjuntos de datos. Con el espacio de trabajo del ciclo vital de datos en la interfaz de usuario o las llamadas a la API de higiene de datos, puede administrar de forma eficaz los almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas organizativas lo consideran necesario.

| Función | Descripción |
| --- | --- |
| Eliminación de registros solo de perfil y de varios conjuntos de datos (solo API) | Puede enviar un solo ID de conjunto de datos, una lista de ID de conjunto de datos separados por comas o el literal `ALL` en `datasetId` para eliminar identidades en uno, varios o todos los conjuntos de datos. También puede limitar la eliminación a los servicios relacionados con perfiles estableciendo `targetServices` en `["identity","profile","ajo"]`, lo que no modifica el conjunto de datos; esta funcionalidad solo está disponible a través de la API de higiene de datos. Consulte la [Guía de eliminación de pedidos de trabajo](../../hygiene/api/workorder.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [información general de la administración avanzada del ciclo de vida de los datos](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Utilice Agent Orchestrator para crear e implementar agentes con tecnología de IA que automaticen flujos de trabajo e interactúen con los clientes en varios canales.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [Adobe Marketing Agent para [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] es su agente incrustado que incorpora el conocimiento de marketing de Adobe directamente en herramientas cotidianas como [!DNL Teams], [!DNL Word], [!DNL PowerPoint] y otras aplicaciones de [!DNL Microsoft 365]. Puede utilizar este agente para extraer información de campañas de confianza de las aplicaciones de Adobe mientras planea campañas, revisa audiencias y colabora con compañeros para responder preguntas de clientes y tomar decisiones basadas en datos sin abandonar el flujo de trabajo de [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Para obtener más información, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Corrientes de datos {#datastreams}

Un conjunto de datos representa la configuración del lado del servidor al implementar los SDK web y móvil de Adobe Experience Platform y la API de servidor de Adobe Experience Platform Edge Network. El comando de configuración de la secuencia de datos en los SDK gestiona todos los servicios con los que interactúa un cliente.

| Función | Descripción |
| --- | --- |
| Disponibilidad general de las configuraciones de flujo de datos dinámico | Ya están disponibles de forma general las configuraciones de flujo de datos dinámico. Con las configuraciones de flujo de datos dinámico, puede definir conjuntos de reglas configurables por el usuario para cada servicio habilitado para el flujo de datos, que dictan qué solución de Experience Cloud debe recibir cada tipo de datos. Consulte la [guía de configuraciones de secuencia de datos dinámica](../../datastreams/configure-dynamic-datastream.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de flujos de datos](../../datastreams/overview.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino. Utilice destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [Lote de Snowflake](../../destinations/catalog/warehouses/snowflake-batch.md) selector de región | Ahora puede encontrar su región más fácilmente con la nueva lista desplegable de búsqueda, que combina la búsqueda y la lista desplegable en un control. Esta actualización se estará publicando hasta finales de marzo. |
| Nueva estructura de tabla para [destinos del lote Snowflake](../../destinations/catalog/warehouses/snowflake-batch.md) | Las tablas compartidas en la cuenta de Snowflake ahora tienen una nueva estructura que incluye columnas de nombre de audiencia y origen de audiencia independientes. La nueva estructura de tabla se aplica a todas las conexiones de destino nuevas configuradas a partir de ahora. Para cualquier nueva conexión que configure, se crean ambas estructuras de tabla: la nueva estructura tiene el prefijo V2 y la estructura antigua se mantiene hasta finales de junio de 2026, después de lo cual quedará obsoleta. Obtenga más información en la sección [Datos exportados](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) de la documentación por lotes de Snowflake. Esta actualización se estará publicando hasta finales de marzo. |
| [Conexión de Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md) | La nueva conexión de Adobe Advertising DSP ofrece la misma funcionalidad que la conexión heredada, además de compatibilidad con identidades adicionales. Con el nuevo conector, también puede exportar identidades basadas en cookies a Adobe Advertising DSP. |
| Conexión de [FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Envíe audiencias de [!DNL Real-Time CDP] a FreeWheel como archivos por lotes diarios para que pueda segmentarlas en ofertas y campañas de FreeWheel en CTV, vídeo y pantalla. Póngase en contacto con el equipo de su cuenta de Adobe para obtener acceso. |
| Compatibilidad con audiencias externas para [The Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) y [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Ahora puede activar audiencias desde orígenes que van más allá del servicio de segmentación hasta Trade Desk CRM, Criteo y Pinterest, incluidas audiencias de carga personalizadas (importadas desde CSV), audiencias similares, audiencias federadas y audiencias creadas en otras aplicaciones de Experience Platform como [!DNL Adobe Journey Optimizer]. Esta actualización se estará publicando hasta finales de marzo. Consulte la sección [audiencias admitidas](../../destinations/catalog/advertising/criteo.md#supported-audiences) en la página del catálogo de cada destino para obtener más información. |
| Se ha aumentado el límite de audiencias de carga personalizadas | Ahora puede activar hasta 20 audiencias de carga personalizadas por instancia de destino. Anteriormente, este límite era de 10. Consulte las [protecciones de destinos](../../destinations/guardrails.md#batch-file-based-activation) para obtener más información. |
| [Exportar archivo ahora](../../destinations/ui/export-file-now.md) y [compatibilidad con la API de activación ad hoc](../../destinations/api/ad-hoc-activation-api.md) para audiencias externas | Ahora puede utilizar la interfaz de usuario y la API de activación ad-hoc de Exportar archivo ahora con audiencias externas (como carga personalizada, similitud, federación y audiencias de otras aplicaciones de Experience Platform) al activar en destinos basados en archivos por lotes. Esta actualización se estará publicando hasta finales de marzo. |
| [Destinos de la API HTTP](../../destinations/catalog/streaming/http-destination.md) con OAuth 2 y mTLS | Ahora puede crear y autenticar destinos de API HTTP que utilicen OAuth 2 cuando el extremo de autenticación requiera TLS mutuo (mTLS); la recuperación de tokens durante la configuración de destino ahora admite mTLS. Esta actualización se estará publicando hasta finales de marzo. |

{style="table-layout:auto"}

**Correcciones y mejoras**

| Se ha corregido un problema que hacía que se mostrara | Descripción |
| --- | --- |
| hash del número de teléfono del conector [TikTok](../../destinations/catalog/social/tiktok.md) | Se ha corregido un problema por el cual una configuración incorrecta en la tarjeta de destino significaba que las identidades marcadas desde números de teléfono no se activaban en TikTok. Para beneficiarse de esta corrección, configure un nuevo flujo de activación o elimine la asignación del número de teléfono del flujo existente, guárdelo y agréguelo de nuevo. |
| [Transmisión de Snowflake](../../destinations/catalog/warehouses/snowflake.md) y [Validación de ID de cuenta por lotes de Snowflake](../../destinations/catalog/warehouses/snowflake-batch.md) | Se ha agregado un validador de expresiones regulares al paso ID de cuenta. Al introducir su ID, ahora se valida para garantizar que el ID de organización y el ID de cuenta tengan el formato correcto (separados por un punto). Esta actualización se estará publicando hasta finales de marzo. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

| Función | Descripción |
| --- | --- |
| Acciones de entidad XDM y compatibilidad de eliminación | Acceda a acciones para esquemas, clases, grupos de campos y tipos de datos directamente desde menús de tablas en línea y menús de encabezados de páginas de detalles. Si tiene los permisos necesarios, también puede eliminar las entidades de su organización cuando no las utilicen los conjuntos de datos y no estén habilitadas para el perfil. Consulte la [guía de la interfaz de usuario de XDM](../../xdm/ui/explore.md) para obtener más información. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#real-time-customer-profile}

El Perfil del cliente en tiempo real proporciona una vista completa de cada cliente individual combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. Utilice el perfil para consolidar los datos de sus clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Eventos | Ahora puede establecer el período retroactivo de eventos al examinar los perfiles. Esto le permite ver los eventos a los que está asociado el perfil para el período de tiempo especificado. Para obtener más información, lea la [guía de la interfaz de usuario del perfil](../../profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Real-Time Customer Profile] información general](../../profile/home.md).

## Ejecutar y operar {#run-and-operate}

Inspeccione, solucione problemas y optimice las implementaciones de Experience Platform con las herramientas Ejecutar y operar. Obtenga visibilidad sobre las activaciones por lotes programadas, identifique los problemas de configuración y mejore la fiabilidad del sistema.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de [horarios de trabajo](../../run-and-operate/job-schedules.md) | [!DNL Job Schedules] proporciona una vista unificada de todos los trabajos de procesamiento por lotes programados en toda la canalización de datos, desde la ingesta hasta la activación de destino. Inspeccione el estado de ejecución, identifique los conflictos de programación y diagnostique los problemas de configuración antes de que afecten a las operaciones empresariales. |
| Disponibilidad general de [comprobaciones de estado](../../run-and-operate/health-checks.md) | Las configuraciones de esquema e identidad deficientes derivan en problemas descendentes significativos, como la creación incorrecta de perfiles, la calificación fallida de segmentos y la activación inexacta. <br>Las comprobaciones de estado cambian su enfoque de la solución de problemas reactiva al mantenimiento preventivo y proactivo. Las comprobaciones de estado son análisis siempre activos de los esquemas e identidades utilizados en la zona protegida y proporcionan un resumen de los problemas que puede utilizar para explorar y solucionar problemas. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre la ejecución y el funcionamiento](../../run-and-operate/overview.md), [Inspeccionar las programaciones de trabajos](../../run-and-operate/job-schedules.md) y la [guía de la interfaz de usuario de la plataforma](../../landing/ui-guide.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Tipo de ingesta | Ahora puede ver el tipo de ingesta de sus atributos. Esto le permite conocer el origen de los datos y crear mejores audiencias. Para obtener más información acerca de esta característica, lea la [guía del Generador de segmentos](../../segmentation/ui/segment-builder.md). |
| Datos de resumen | Ahora puede ver los datos de resumen de los atributos de las audiencias basadas en cuentas y personas. Para obtener más información acerca de esta característica en las audiencias de la cuenta, lea la cuenta [Guía del generador de audiencias](../../rtcdp/segmentation/audience-builder.md). Para obtener más información sobre esta característica en audiencias basadas en personas, lee la [guía del Generador de segmentos](../../segmentation/ui/segment-builder.md). |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Utilice estas conexiones de origen para autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| [!DNL Talon.One] | Ahora puede conectar Experience Platform a [!DNL Talon.One] con las nuevas fuentes [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) y [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Utilice las nuevas fuentes para introducir datos del perfil de lealtad, así como eventos de transacciones y actividades de lealtad en Experience Platform. |
| Nuevas direcciones IP para la lista de permitidos | Nuevas direcciones IP para GBR9: Reino Unido se han añadido a la lista de direcciones que debe lista de permitidos para garantizar conexiones de origen por lotes correctas a Experience Platform en Azure. Vea la lista en la [guía de lista de permitidos de direcciones IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) para obtener más información. |
| Compatibilidad mejorada con la captura de datos modificados | Ahora puede usar Cambiar captura de datos con los orígenes [!DNL Marketo Engage], [!DNL Microsoft Dynamics] y [!DNL Salesforce CRM]. |
| Guía de autenticación mejorada para [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | La guía de autenticación para el origen [!DNL Google BigQuery] se ha expandido con la siguiente información: <ul><li>Los ámbitos necesarios para el token de actualización.</li><li>Los roles de IAM necesarios para la identidad [!DNL Google].</li><li>Instrucciones adicionales sobre el uso de `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).
