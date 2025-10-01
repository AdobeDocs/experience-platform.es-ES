---
title: Notas de la versión de Adobe Experience Platform, agosto de 2025
description: Las notas de la versión de agosto de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 93%

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

**Fecha de la versión: 23 de septiembre de 2025**

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
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator es la nueva capa agéntica de Adobe Experience Platform. Diseñado para aprovechar los abundantes datos y el conocimiento de los clientes de la plataforma, Experience Platform Agent Orchestrator potencia la inteligencia y el razonamiento que hay detrás de los agentes expertos de Adobe Experience Platform creados específicamente, lo que les permite ejecutar tareas complejas de toma de decisiones y resolución de problemas con rapidez y a gran escala, todo ello con supervisión humana. Cuando formula preguntas o solicita ayuda a través del lenguaje natural en una interfaz conversacional como el Asistente de IA, Agent Orchestrator llama automáticamente a agentes especializados para que le den las respuestas correctas. Agent Orchestrator recuerda el historial de sus conversaciones, lo que le permite basarse en preguntas anteriores de forma natural sin repetir el contexto, y combina la información de varios agentes para presentarle respuestas claras y unificadas. Para obtener más información, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). |
| Audience Agent | Audience Agent le permite ver información sobre los públicos, como la detección de cambios significativos en el tamaño del público, la detección de públicos duplicados, la exploración del inventario de públicos y la recuperación del tamaño de estos. Para obtener más información, lea la [documentación de Audience Agent](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Para obtener más información, lea la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/home).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Alertas de ingesta de perfiles de streaming | Ahora puede suscribirse a dos nuevas alertas para la ingesta de streaming a nivel de flujo de datos: <ul><li>Se ha superado la tasa de errores de ingesta de streaming</li><li>Se ha superado la tasa de omisión de ingesta de streaming</li></ul> Las alertas en la plataforma o por correo electrónico le avisarán cuando se superen los umbrales para el umbral predeterminado o un umbral personalizado que defina. Para obtener más información, lea la guía de [Alertas del perfiles](../../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| Conector [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md) | Ya está disponible un nuevo conector [!DNL Snowflake Batch] que proporciona una alternativa al conector de streaming para casos de uso específicos. |
| Compatibilidad con el cifrado de [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Ahora puede adjuntar claves públicas con formato RSA para cifrar los archivos exportados, lo que le proporciona el mismo nivel de seguridad que otros destinos de almacenamiento en la nube para la información confidencial. |
| Detalles de caducidad de la autenticación para destinos de [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md)  | La información de caducidad de autenticación de los destinos de [!DNL Pinterest] ahora es visible directamente en la interfaz de Experience Platform, por lo que puede ver cuándo caducará la autenticación y renovarla antes de que cause interrupciones en los flujos de datos. Puede monitorizar las fechas de caducidad de los tókenes desde la columna **[!UICONTROL Fecha de caducidad de la cuenta]** en las pestañas **[[!UICONTROL Cuentas]](../../destinations/ui/destinations-workspace.md#accounts)** o **[[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Funciones mejoradas de administración de destinos en la IU de Experience Platform | Mejore su flujo de trabajo de administración de destinos con las nuevas funciones de ordenación en las pestañas [[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse) y [[!UICONTROL Cuentas]](../../destinations/ui/destinations-workspace.md#accounts). Ahora también puede ver un indicador visual cuando la autenticación de la cuenta esté a punto de caducar. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| Configuración de ancho de columna persistente | La configuración del ancho de columna ahora persiste al salir de una página y volver a ella. Por ejemplo, si ajusta la anchura de una columna en la pestaña [[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse), la anchura de la columna personalizada se mantendrá igual cuando salga de la pestaña y vuelva a ella. |

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Esquemas basados en modelos | Simplifique el modelado de datos con esquemas basados en modelos. Ahora puede crear esquemas más fácilmente con ejemplos explicativos y directrices completos. En la actualidad, esta función está disponible para los titulares de licencias de orquestación de campañas y se ampliará a los clientes de Data Distiller a disponibilidad general, lo que hará que el modelado de datos sea más accesible y eficiente. La funcionalidad incluye compatibilidad con datos de series temporales y funciones de captura de datos de cambios. |
| Data Mirror | Introduzca cambios de nivel de fila de almacenes de datos en la nube (por ejemplo, Snowflake, Databricks, BigQuery) en Adobe Experience Platform mediante esquemas basados en modelos. Data Mirror elimina el ETL ascendente y conserva las relaciones, el control de versiones y las eliminaciones al duplicar las estructuras de base de datos existentes directamente en el lago de datos. Se admite el comportamiento de esquemas de series temporales y eventos de registro con capacidades de captura de datos modificados. Actualmente, esta función está disponible para los titulares de licencias de Campaign Orchestration y se ampliará con esta versión limitada, incluyendo también a los clientes de Customer Journey Analytics. Consulte la [documentación de Data Mirror](../../xdm/data-mirror/overview.md) para obtener más información. Póngase en contacto con su representante de Adobe para obtener acceso. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Mejoras del visor de perfiles | La versión de septiembre de 2025 de incluye las siguientes mejoras en el visor de perfiles. <ul><li>**Vista combinada**: los atributos, los eventos y los datos se han combinado en una sola vista.</li><li>**Información generada por IA**: la página de detalles del perfil ahora muestra información generada por IA, lo que le permite conocer detalles generados a partir de su perfil. Estos datos pueden incluir información como las puntuaciones de las tendencias y el análisis de tendencias.</li><li>**Actualización del estilo**: la página de detalles del perfil se ha actualizado visualmente.</li><li>**Examinar**: ahora puede explorar sus perfiles a través de un carrusel interactivo basado en tarjetas con búsqueda y personalización.</li></ul> |

Para obtener más información, lea la [información general sobre el perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Públicos de cuentas con eventos de experiencia en desuso | Después de la actualización de la arquitectura B2B, ya no se admiten los públicos de cuentas con eventos de experiencia. En su lugar, utilice el nuevo enfoque de segmentos del segmento: cree un público de personas con eventos de experiencia y, a continuación, haga referencia a ese público de personas al crear un público de cuentas. Esto ofrece un enfoque más flexible y mantenible para la creación de públicos B2B. |

**Actualizaciones importantes**

| Actualización | Descripción |
| ------- | ----------- |
| Reversión de la actualización automática para las estimaciones de público | Se ha revertido la mejora de actualización automática para las estimaciones de público. Las estimaciones de público se seguirán generando en el Generador de segmentos, pero se ha eliminado la funcionalidad de actualización automática. |
| Públicos externos | A partir del 30 de septiembre, los públicos externos se recuperarán mediante la búsqueda unificada en el Generador de segmentos. Si utiliza la coincidencia de segmentos, puede habilitar la experiencia heredada en el Generador de segmentos. |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas fuentes en GA (disponibilidad general) | Las siguientes fuentes ya están disponibles en GA (disponibilidad general): se han actualizado varios conectores de fuente de Beta a GA: <ul><li>[Ingesta de datos de Acxiom](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Ingesta de datos de clientes potenciales de Acxiom](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Estas fuentes ahora son totalmente compatibles y están listas para su uso en producción. |
| [!DNL Snowflake]: compatibilidad para la autenticación mediante par de claves | Mayor seguridad para las conexiones de Snowflake con compatibilidad para la autenticación mediante par de claves. La autenticación básica (nombre de usuario y contraseña) dejará de usarse en noviembre de 2025, por lo que se recomienda a los clientes migrar a la autenticación mediante par de claves para mejorar la seguridad. Para obtener más información, consulte esta [[!DNL Snowflake] documentación](../../sources/connectors/databases/snowflake.md). |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Utilice la [[!DNL Capillary Streaming Events] fuente](../../sources/connectors/loyalty/capillary.md) para transmitir datos desde su cuenta de [!DNL Capillary] a Experience Platform.  |
| [!BADGE Beta]{type=Informative} [!DNL Relay Connector] | Use [[!DNL Relay Connector]](../../sources/tutorials/ui/create/marketing-automation/relay-connector.md) para transmitir datos de eventos desde su integración de [!DNL Relay Network] a Experience Platform. |
| Disponibilidad general de la compatibilidad con vínculos privados en las fuentes | Ahora puede usar **vínculos privados** para un grupo selecto de fuentes. Utilice esta función para crear un punto final privado al que se pueda conectar la fuente. Con los puntos finales privados, puede configurar conexiones y flujos de datos que omiten el internet público, lo que le ofrece una seguridad mejorada y un aislamiento de red para sus datos confidenciales. La compatibilidad de los vínculos privados está disponible para las siguientes fuentes: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. Para obtener más información, lea las guías sobre la creación de vínculos privados [en la API](../../sources/tutorials/api/private-link.md) y [en la interfaz de usuario](../../sources/tutorials/ui/private-link.md). |

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).
