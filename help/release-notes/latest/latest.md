---
title: Notas de la versión de Adobe Experience Platform, agosto de 2025
description: Las notas de la versión de agosto de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 40%

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

**Fecha de la versión: miércoles, 23 de septiembre de 2025**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Alertas](#alerts)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator es la nueva capa agéntica de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator es la nueva capa agéntica de Adobe Experience Platform. Diseñado para aprovechar los abundantes datos y el conocimiento de los clientes de la plataforma, Experience Platform Agent Orchestrator potencia la inteligencia y el razonamiento detrás de los agentes de Adobe Experience Platform expertos creados específicamente, lo que les permite ejecutar tareas complejas de toma de decisiones y resolución de problemas a velocidad y escala, todo ello con supervisión humana. Cuando hace preguntas o solicita ayuda a través del lenguaje natural en una interfaz conversacional como el asistente de IA, Agent Orchestrator llama automáticamente a agentes especializados para que le obtengan las respuestas correctas. Agent Orchestrator recuerda el historial de sus conversaciones, lo que le permite basarse en preguntas anteriores de forma natural sin repetir el contexto, y combina las perspectivas de varios agentes para presentarle respuestas claras y unificadas. Para obtener más información, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). |
| Audience Agent | Audience Agent le permite ver información sobre las audiencias, como la detección de cambios significativos en el tamaño de la audiencia, la detección de audiencias duplicadas, la exploración del inventario de audiencias y la recuperación del tamaño de estas. Para obtener más información, lea la [documentación de Audience Agent](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Para obtener más información, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/home).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Alertas de ingesta de perfil de streaming | Ahora puede suscribirse a dos nuevas alertas para la transmisión de ingesta a nivel de flujo de datos: <ul><li>Tasa de errores de ingesta de transmisión superada</li><li>Tasa de ingesta omitida de streaming superada</li></ul> Las alertas en plataforma o por correo electrónico le avisarán cuando se superen los umbrales para el umbral predeterminado o un umbral personalizado que defina. Para obtener más información, lea la guía [Alertas de perfil](../../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| Conector [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md) | Ya está disponible un nuevo conector [!DNL Snowflake Batch] que proporciona una alternativa al conector de flujo continuo para casos de uso específicos. |
| Compatibilidad con cifrado [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Ahora puede adjuntar claves públicas con formato RSA para cifrar los archivos exportados, lo que le proporciona el mismo nivel de seguridad que otros destinos de almacenamiento en la nube para la información confidencial. |
| Detalles de caducidad de autenticación para [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) destinos | La información de caducidad de autenticación de los destinos de [!DNL Pinterest] ahora es visible directamente en la interfaz de Experience Platform, por lo que puede ver cuándo caducará la autenticación y renovarla antes de que cause interrupciones en los flujos de datos. Puede monitorizar las fechas de caducidad de los tókenes desde la columna **[!UICONTROL Fecha de caducidad de la cuenta]** en las pestañas **[[!UICONTROL Cuentas]](../../destinations/ui/destinations-workspace.md#accounts)** o **[[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Funciones mejoradas de administración de destinos en la IU de Experience Platform | Mejore su flujo de trabajo de administración de destinos con nuevas capacidades de ordenación en las fichas [[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse) y [[!UICONTROL Cuentas]](../../destinations/ui/destinations-workspace.md#accounts). Ahora también puede ver un indicador visual cuando la autenticación de la cuenta esté a punto de caducar. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| Configuración de ancho de columna persistente | La configuración del ancho de columna ahora persiste al salir de una página y volver a ella. Por ejemplo, si ajusta el ancho de una columna en la ficha [[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse), el ancho de la columna personalizada seguirá siendo el mismo cuando se desplace y vuelva a esa ficha. |

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Esquemas basados en modelos | Simplifique el modelado de datos con esquemas basados en modelos. Ahora puede crear esquemas más fácilmente con ejemplos explicativos y directrices completos. Actualmente, esta función está disponible para los titulares de licencias de Campaign Orchestration y se ampliará a los clientes de Data Distiller en GA, lo que hace que el modelado de datos sea más accesible y eficiente. La funcionalidad incluye compatibilidad con datos de series temporales y capacidades de captura de datos de cambios. |
| Data Mirror | Introduzca cambios de nivel de fila de almacenes de datos en la nube (por ejemplo, Snowflake, Databricks, BigQuery) en Adobe Experience Platform mediante esquemas basados en modelos. Data Mirror elimina el ETL ascendente y conserva las relaciones, el control de versiones y las eliminaciones al duplicar las estructuras de base de datos existentes directamente en el lago de datos. Se admite el comportamiento de esquemas de series temporales y eventos de registro con capacidades de captura de datos modificados. Actualmente, esta función está disponible para los titulares de licencias de Campaign Orchestration y se ampliará con esta versión limitada, incluyendo también a los clientes de Customer Journey Analytics. Consulte la [documentación de Data Mirror](../../xdm/data-mirror/overview.md) para obtener más información. Póngase en contacto con su representante de Adobe para obtener acceso. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Mejoras del visor de perfiles | La versión de septiembre de 2025 de incluye las siguientes mejoras en el visualizador de perfiles. <ul><li>**Vista combinada**: los atributos, los eventos y las perspectivas se han combinado en una sola vista.</li><li>**Información generada por IA**: La página de detalles del perfil ahora muestra información generada por IA, lo que le permite conocer detalles generados a partir de su perfil. Estas perspectivas pueden incluir información como puntuaciones de tendencia y análisis de tendencias.</li><li>**Actualización de estilo**: la página de detalles del perfil se ha actualizado visualmente.</li><li>**Examinar**: ahora puede explorar sus perfiles a través de un carrusel interactivo basado en tarjetas con búsqueda y personalización.</li></ul> |

Para obtener más información, lea la [Descripción general del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Audiencias de cuenta con eventos de experiencia en desuso | Después de la actualización de la arquitectura B2B, ya no se admiten las audiencias de cuenta con eventos de experiencia. En su lugar, utilice el nuevo enfoque de segmento de segmentos: cree una audiencia de Personas con Eventos de experiencia y, a continuación, consulte esa audiencia de Personas al crear una Audiencia de cuenta. Esto ofrece un enfoque más flexible y mantenible de la creación de audiencias B2B. |

**Actualizaciones importantes**

| Actualización | Descripción |
| ------- | ----------- |
| Estimaciones de audiencia: reversión de actualización automática | Se ha revertido la mejora de actualización automática para estimaciones de audiencia. Las estimaciones de audiencia se seguirán generando en el Generador de segmentos, pero se ha eliminado la funcionalidad de actualización automática. |
| Audiencia externa | A partir del 30 de septiembre, las audiencias externas se recuperarán mediante la búsqueda unificada en el Generador de segmentos. Si utiliza Coincidencia de segmentos, puede habilitar la experiencia heredada en el Generador de segmentos. |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas fuentes en General Availability | Las siguientes fuentes están ahora en General Availability: Se han actualizado varios conectores de fuente de Beta a GA: <ul><li>[Ingesta de datos de Acxiom](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Ingesta de datos de clientes potenciales de Acxiom](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Estas fuentes ahora son totalmente compatibles y están listas para su uso en producción. |
| [!DNL Snowflake]: compatibilidad con la autenticación de par de claves | Seguridad mejorada para conexiones de Snowflake compatible con la autenticación de par de claves. La autenticación básica (nombre de usuario y contraseña) dejará de usarse en noviembre de 2025, por lo que se recomienda a los clientes migrar a la autenticación de par de claves para mejorar la seguridad. Para obtener más información, consulte la [[!DNL Snowflake] documentación](../../sources/connectors/databases/snowflake.md). |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Use [[!DNL Capillary Streaming Events] source](../../sources/connectors/loyalty/capillary.md) para transmitir datos de fidelidad de su cuenta de [!DNL Capillary] a Experience Platform. |
| [!BADGE Beta]{type=Informative} [!DNL Relay Connector] | Use [[!DNL Relay Connector]](../../sources/tutorials/ui/create/marketing-automation/relay-connector.md) para transmitir datos de eventos desde su integración de [!DNL Relay Network] a Experience Platform. |
| Disponibilidad general de la compatibilidad con vínculos privados en las fuentes | Ahora puede usar **vínculos privados** para un grupo selecto de orígenes. Utilice esta función para crear un punto final privado al que se pueda conectar la fuente. Con los puntos finales privados, puede configurar conexiones y flujos de datos que omiten el internet público, lo que le ofrece una seguridad mejorada y un aislamiento de red para sus datos confidenciales. La compatibilidad con vínculos privados está disponible para las siguientes fuentes: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. Para obtener más información, lea las guías sobre la creación de vínculos privados [en la API](../../sources/tutorials/api/private-link.md) y [en la interfaz de usuario](../../sources/tutorials/ui/private-link.md). |

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).
