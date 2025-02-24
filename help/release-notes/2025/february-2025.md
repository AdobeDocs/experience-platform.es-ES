---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2025'
description: Las notas de la versión de febrero de 2025 de Adobe Experience Platform.
source-git-commit: 300be2f922f81f0666a794815cb27777802efb60
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 94%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Esta versión incluye mejoras en el complemento Composición de público federado. Para obtener más información, lea las [notas de la versión de Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes).

**Fecha de publicación: 18 de febrero de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Asistente de IA](#ai-assistant)
- [Servicio de catálogo](#catalog-service)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Orígenes](#sources)
- [Actualizaciones de la documentación](#documentation-updates)
   - [Comparación entre Edge Network y hub](#edge)
   - [API del servicio de flujo expandida para orígenes](#flow-service)
   - [Copia de seguridad de configuraciones de objeto mediante herramientas de zona protegida](#back-up-object-configurations)
   - [Habilitación de un centro de excelencia mediante herramientas de zona protegida](#center-of-excellence)
   - [Retención de conjuntos de datos de eventos de experiencia en el lago de datos](#experience-event-dataset-retention)

## Asistente de IA {#ai-assistant}

El Asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el Asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El Asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de la información operativa | La información operativa del Asistente de IA ya está disponible a nivel general. La información operativa se refiere a las respuestas que genera el Asistente de IA sobre los objetos de metadatos (atributos, públicos, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y orígenes), incluidos los recuentos, las búsquedas y el impacto en el linaje. La información operativa no examina ningún dato dentro de la zona protegida. Para obtener más información, lea la [Guía de la IU del Asistente de IA](../../ai-assistant/ui-guide.md). |
| Compatibilidad con la función de autocompletar preguntas | Al introducir una pregunta en el Asistente de IA, ahora puede seleccionar una lista de preguntas recomendadas que el Asistente de IA proporciona. Utilice esta función para acelerar aún más los flujos de trabajo con el Asistente de IA. Para obtener más información, lea la guía sobre el [uso de autocompletar preguntas con el Asistente de IA](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Compatibilidad con la observabilidad del conjunto de datos | Ahora puede utilizar el Asistente de IA para responder a preguntas sobre métricas de conjuntos de datos específicas, como los tamaños de almacenamiento y los recuentos de filas. Las preguntas de observabilidad de datos admiten cualificadores que puede utilizar para filtrar las consultas por un período de tiempo determinado. Para obtener más información, lea la [Guía de preguntas del Asistente de IA](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre el Asistente de IA](../../ai-assistant/home.md).

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

| Función | Descripción |
| --- | --- |
| Nuevo punto final de la API | Administre los metadatos del conjunto de datos de Adobe Experience Platform de forma más eficaz con el nuevo punto final de la [API de servicio de catálogo /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). Actualice fácilmente atributos de conjuntos de datos complejos y profundamente anidados, ya que el sistema crea automáticamente niveles de ruta que faltan para ahorrarle tiempo, reducir los pasos manuales y minimizar los errores. |

{style="table-layout:auto"}

Para obtener más información sobre el Servicio de catálogo, consulte la [información general sobre el Servicio de catálogo](../../catalog/home.md).

## Preparación de los datos {#data-prep}

Utilice la preparación de datos para asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad mejorada para importar y exportar asignaciones | Ahora puede exportar asignaciones a un archivo CSV y configurarlas localmente en una hoja de cálculo. A continuación, puede importar las asignaciones actualizadas a Experience Platform mediante la interfaz de asignación en la interfaz de usuario. Puede utilizar esta función para configurar grandes cantidades de asignaciones sin tener que crearlas manualmente en la interfaz de usuario. Además, al crear un nuevo flujo de datos, puede cargar una copia de las asignaciones directamente en Experience Platform para acelerar el flujo de trabajo. Para obtener más información, lea la guía sobre [importación y exportación de asignaciones](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre la preparación de los datos](../../data-prep/home.md).

## Destinos (actualizado el 20 de febrero) {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [(Beta) Sincronización de personas de Marketo Engage](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Utilice el conector [!DNL Marketo Engage Person Sync] para transmitir actualizaciones de públicos de personas a los registros correspondientes en su instancia de [!DNL Marketo Engage]. Este conector de destino está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con su representante de Adobe. |
| Disponibilidad general de la [conexión de Trade Desk CRM](/help/destinations/catalog/advertising/tradedesk-emails.md) | La conexión de [!DNL The Trade Desk CRM] ya está disponible de forma general. Use el destino de [!DNL The Trade Desk] para activar perfiles en su cuenta de [!DNL Trade Desk] para la segmentación y supresión de públicos en función de los datos de CRM. |
| [Conexión de perfiles de asistentes de RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Utilice el destino de [!DNL RainFocus Attendee Profiles] para transmitir perfiles de clientes de Adobe Experience Platform a la plataforma [!DNL RainFocus] con el fin de crear y actualizar perfiles de asistentes. |
| Disponibilidad general de la [conexión de Criteo](/help/destinations/catalog/advertising/criteo.md) | La conexión de [!DNL Criteo] ya está disponible de forma general. Criteo potencia una publicidad fiable e impactante para llevar experiencias más enriquecedoras a todos los consumidores a través de la internet abierta. Con el conjunto de datos de comercio más grande del mundo y la mejor IA de su clase, Criteo garantiza que cada punto de contacto a través del recorrido de compras esté personalizado para llegar a los clientes con el anuncio adecuado, en el momento adecuado. |
| [[!DNL Amazon Ads] conexión](../../destinations/catalog/advertising/amazon-ads.md) | El conector [!DNL Amazon Ads], anteriormente en la versión beta, ya está disponible de forma general. El conector también se ha actualizado para enviar una señal de consentimiento otorgada para todos los perfiles que han dado su consentimiento para que sus datos personales se utilicen para la publicidad. Obtenga más información sobre el nuevo control de [Amazon Ads Consent Signal](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| Utilice etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino | Como parte de la funcionalidad del [[!UICONTROL control de acceso basado en atributos]](/help/access-control/abac/overview.md) de Real-Time CDP, ahora puede aplicar etiquetas de acceso a [flujos de datos de destino](/help/dataflows/ui/monitor-destinations.md). De este modo, puede asegurarse de que solo un subconjunto de usuarios de su organización obtenga acceso a flujos de datos de destino específicos. <br> **Importante**: Al buscar flujos de datos de destino mediante el cuadro de búsqueda en la parte superior de la interfaz de usuario de Experience Platform, los resultados pueden incluir flujos de datos de destino que las etiquetas de acceso de usuario no le permiten ver. Este comportamiento se actualizará en una futura actualización. |
| [Sistema de informes a nivel de público](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) para la [conexión de Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Ahora puede [ver información](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sobre las identidades activadas, excluidas o fallidas desglosadas a nivel de público para cada público que forme parte de los flujos de datos de este destino. |
| Compatibilidad con públicos externos para las conexiones de [TikTok](/help/destinations/catalog/social/tiktok.md) y [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Puede activar públicos externos en estos destinos desde [cargas personalizadas](../../segmentation/ui/audience-portal.md#import-audience) y [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/start/audiences). |
| Exportar matrices, asignaciones y objetos a destinos de almacenamiento en la nube | Si usa la nueva opción **[!UICONTROL Exportar matrices, mapas y objetos]** al conectarse a un destino de almacenamiento en la nube, podrá exportar nuevos objetos complejos para seleccionar destinos. [Más información](/help/destinations/ui/export-arrays-calculated-fields.md) sobre la nueva funcionalidad. |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Se ha corregido un problema en las herramientas de prueba de Destination SDK. Algunos clientes o socios han detectado problemas con la [herramienta de generación de perfiles de muestra](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) debido a un formato no admitido cuando el esquema utilizado para generar perfiles incluía tipos de datos con un selector `No format`.
- Se ha corregido un problema al actualizar la especificación de destinos `targetConnection` mediante la API del servicio de flujo. En algunos casos, la operación PATCH se comportaría de manera similar a una operación POST, dañando los flujos de datos existentes. Este problema ya está solucionado y todos los clientes pueden usar la API del servicio de flujo para actualizar su especificación `targetConnection`. [Más información](/help/destinations/api/edit-destination.md#patch-target-connection).
- Al exportar perfiles a destinos basados en archivos, la deduplicación garantiza que solo se exporte un perfil cuando varios perfiles compartan la misma clave de deduplicación y la misma marca de tiempo de referencia. Esta versión incluye una actualización del proceso de deduplicación, lo que garantiza que las ejecuciones sucesivas con las mismas coordenadas siempre produzcan los mismos resultados, lo que mejora la coherencia. [Más información](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Para obtener más información, lea la [Información general de destinos](../../destinations/home.md).


## Orígenes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Característica actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con vistas en [!DNL Microsoft Dynamics] | Ahora puede ingerir `"entityType": "view"` al usar el origen [!DNL Microsoft Dynamics]. Para obtener más información, lea la guía sobre [la conexión de un origen  [!DNL Microsoft Dynamics]  a Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de fuentes](../../sources/home.md).

## Actualizaciones de la documentación {#documentation-updates}

### Comparación entre Edge Network y hub {#edge}

La [comparación entre Edge Network y hub](../../landing/edge-and-hub-comparison.md) proporciona información general que detalla las diferencias entre los dos tipos de servidor para Adobe Experience Platform (hub y Edge Network), incluidos los servicios disponibles en cada tipo de servidor, las ubicaciones de los servidores y los escenarios recomendados para utilizar cada tipo de servidor.

### Referencia de API del servicio de flujo ampliada para orígenes {#flow-service}

La [[!DNL Flow Service] referencia de API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) para los orígenes se ha actualizado con nuevos ejemplos de solicitud y respuesta de API. Utilice la referencia de API expandida para crear y actualizar las especificaciones de conexión al integrar su propio origen en Experience Platform. También puede utilizar la referencia de API expandida para realizar transiciones de estado en las entidades de origen, actualizar las conexiones de origen y destino existentes y recuperar flujos y especificaciones de flujo según un criterio de filtrado específico.

### Copia de seguridad de configuraciones de objeto mediante herramientas de zona protegida {#back-up-object-configurations}

Lea la [guía de configuración de objetos de copia de seguridad](../../sandboxes/use-cases/backup-object-configuration.md) para obtener instrucciones paso a paso sobre cómo crear un paquete de copia de seguridad con las herramientas de zona protegida para asegurarse de que las configuraciones de los objetos estén almacenadas y protegidas.

### Habilitación de un centro de excelencia mediante herramientas de zona protegida {#center-of-excellence}

Lea la [guía del centro de excelencia](../../sandboxes/use-cases/center-of-excellence.md) para obtener instrucciones paso a paso sobre cómo crear un paquete de &quot;zona protegida dorada&quot; que actúe como un centro de excelencia para compartir configuraciones clave de manera eficiente.

### Retención de conjuntos de datos de eventos de experiencia en el lago de datos {#experience-event-dataset-retention}

Tome el control de la retención de conjuntos de datos de eventos de experiencia en Adobe Experience Platform mediante el tiempo de vida (TTL). [Esta guía](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) le explica cómo evaluar, configurar y administrar la configuración de TTL para eliminar automáticamente registros obsoletos, optimizar el almacenamiento y mantener los datos relevantes. Descubra prácticas recomendadas, casos de uso reales y consideraciones clave para mejorar la administración del ciclo de vida de los datos.
