---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: de95e9a51c979e9249ddf9ceb262fc521d2b38f4
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 31%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: octubre de 2025**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Alerta de tasa de error de destino | Se ha agregado una nueva alerta para los destinos: **La tasa de error de destino supera el umbral**. Esta alerta le notifica cuando el número de registros con errores durante la activación de datos ha superado el umbral permitido, lo que le permite responder rápidamente a los problemas de activación. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../observability/home.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [!DNL AdForm] | Use este destino para enviar audiencias de Adobe Real-Time CDP a [!DNL AdForm] para su activación en función del Experience Cloud ID (ECID) y del ID Fusion de [!DNL AdForm]. ID Fusion de [!DNL AdForm] es un servicio de resolución de ID que le permite activar audiencias de origen basadas en el Experience Cloud ID (ECID). |
| [!DNL Amazon Ads] | Se ha agregado compatibilidad con identificadores personales adicionales, como `firstName`, `lastName`, `street`, `city`, `state`, `zip` y `country`. La asignación de estos campos como identidades de destino puede mejorar las tasas de coincidencia de audiencia. |
| [!DNL Snowflake Batch] (disponibilidad limitada) | Cree un recurso compartido de datos de [!DNL Snowflake] activo para recibir actualizaciones diarias de la audiencia directamente como tablas compartidas en su cuenta. Actualmente, esta integración está disponible para las organizaciones de clientes aprovisionadas en la región de VA7. |
| [!DNL Snowflake Streaming] (disponibilidad limitada) | Cree un recurso compartido de datos de [!DNL Snowflake] activo para recibir actualizaciones de audiencia de streaming directamente como tablas compartidas en su cuenta. Actualmente, esta integración está disponible para las organizaciones de clientes aprovisionadas en la región de VA7. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con el cifrado del lado del servidor [!DNL AES256] en [!DNL Amazon S3] destinos | [!DNL Amazon S3] destinos ahora admiten el cifrado del lado del servidor [!DNL AES256], lo que proporciona una seguridad mejorada para los datos exportados. Puede configurar este método de cifrado al configurar o actualizar las conexiones de destino de [!DNL Amazon S3], asegurándose de que los datos se cifren en reposo mediante algoritmos de cifrado de [!DNL AES256] estándar del sector. Para obtener más información, consulte esta [[!DNL Amazon] documentación](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Varios destinos nuevos que admiten la supervisión a nivel de audiencia](../dataflows/ui/monitor-destinations.md#audience-level-view) | Los siguientes destinos ahora admiten la monitorización a nivel de audiencia: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] participación de cuenta</li><li>[!DNL The Trade Desk]</li></ul> |
| Corrección de protecciones de exportación de conjuntos de datos | Se ha implementado una corrección en las protecciones de exportación del conjunto de datos. Anteriormente, algunos conjuntos de datos que incluían una columna de marca de tiempo pero que _no eran_ basados en el esquema de eventos de experiencia XDM se trataban incorrectamente como conjuntos de datos de eventos de experiencia, lo que limitaba las exportaciones a una ventana retrospectiva de 365 días. La protección retrospectiva de 365 días documentada ahora se aplica exclusivamente a los conjuntos de datos de eventos de experiencia. Los conjuntos de datos que utilizan cualquier esquema distinto del esquema de eventos de experiencia XDM ahora se rigen por la protección de 10 000 millones de registros. Es posible que algunos clientes vean números de exportación aumentados para conjuntos de datos que, erróneamente, caen dentro de la ventana retrospectiva de 365 días. Esto permite exportar conjuntos de datos para flujos de trabajo predictivos que tienen una larga ventana retrospectiva. Para obtener más información, lea las [protecciones de exportación del conjunto de datos](../destinations/guardrails.md#dataset-exports). |
| Informes mejorados a nivel de audiencia para destinos empresariales | Se ha mejorado la lógica de creación de informes en el nivel de audiencia para destinos empresariales. Después de esta versión, los clientes verán números de informes de audiencia más precisos que incluyen solo audiencias relevantes para el destino seleccionado. Este ajuste de monitorización garantiza que la creación de informes incluya solo audiencias asignadas en el flujo de datos, lo que proporciona una perspectiva más clara de la activación de datos real. Esto no afecta a la cantidad de datos que se activan, se trata simplemente de una mejora de la monitorización para mejorar la precisión de la creación de informes. |

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Monitorización de segmentación de streaming | La monitorización en tiempo real de la segmentación de streaming ofrece transparencia en la tasa de evaluación, la latencia y las métricas de calidad de datos en los niveles de zona protegida, conjunto de datos y audiencia. Esto admite alertas proactivas y perspectivas procesables para ayudar a los ingenieros de datos a identificar infracciones de capacidad y problemas de ingesta. Las métricas de monitorización incluyen la tasa de evaluación, la latencia de ingesta de P95, así como los registros recibidos, evaluados, fallidos y omitidos. Las funciones de vista por conjunto de datos y vista por audiencia proporcionan una visibilidad completa de los nuevos perfiles netos calificados y descalificados. |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] orígenes de datos de fidelidad | Utilice las fuentes [!DNL Talon.One] para ingerir datos de fidelidad por lotes y de flujo continuo en Experience Platform. El conector admite la transmisión de datos de perfil, datos de transacción y datos de fidelidad, incluidos los puntos obtenidos, los puntos canjeados, los puntos caducados y los datos de nivel. |

**Orígenes actualizados**

| Fuente | Descripción |
| --- | --- |
| Disponibilidad general del origen [!DNL Google Ads] (solo API) | La versión de API del origen [!DNL Google Ads] está ahora en General Availability. La documentación de la API se ha actualizado para reflejar que la versión más reciente ahora es `v21`, y Experience Platform es compatible con todas las versiones v19 y posteriores. La versión de la interfaz de usuario permanece en versión beta y solo admite la ingesta única. Para utilizar la ingesta de datos incremental, utilice la ruta de la API. |
| compatibilidad con la red virtual [!DNL Azure Event Hubs] | Adobe ahora admite explícitamente conexiones de red virtual a Azure Event Hubs, lo que permite la transferencia de datos a través de redes privadas en lugar de redes públicas. Los clientes pueden realizar una lista de permitidos de Experience Platform VNet para enrutar el tráfico de los Event Hubs de forma privada a través de la red troncal privada de Azure, lo que proporciona una seguridad y un cumplimiento mejorados para los flujos de trabajo de ingesta de datos. |

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).
