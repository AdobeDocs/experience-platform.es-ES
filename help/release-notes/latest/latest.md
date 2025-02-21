---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2025'
description: Las notas de la versión de febrero de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b29c63942b00fdf597ebfd3ab105519a6b05a476
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 22%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Esta versión incluye mejoras en el complemento Federated Audience Composition. Para obtener más información, lea las [notas de la versión de Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes).

**Fecha de publicación: miércoles, 18 de febrero de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Asistente de IA](#ai-assistant)
- [Servicio de catálogo](#catalog-service)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Fuentes](#sources)
- [Actualizaciones de la documentación](#documentation-updates)
   - [Comparación de red y concentrador de Edge](#edge)
   - [API de servicio de flujo expandida para orígenes](#flow-service)
   - [Hacer copia de seguridad de configuraciones de objeto mediante herramientas de zona protegida](#back-up-object-configurations)
   - [Activación de un centro de excelencia mediante herramientas de zona protegida](#center-of-excellence)
   - [Retención de conjuntos de datos de eventos de experiencia en el lago de datos](#experience-event-dataset-retention)

## Asistente de IA {#ai-assistant}

El Asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el Asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El asistente de IA es compatible con Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con el completado automático de preguntas | Al introducir una pregunta en el asistente de inteligencia artificial, ahora puede seleccionar una lista de preguntas recomendadas que proporciona el asistente de inteligencia artificial. Utilice esta función para acelerar aún más los flujos de trabajo con AI Assistant. Para obtener más información, lea la guía de [uso del completado automático de preguntas con el Asistente de IA](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Compatibilidad con la observabilidad del conjunto de datos | Ahora puede utilizar el Asistente de IA para responder preguntas sobre métricas de conjuntos de datos específicas, como tamaños de almacenamiento y recuentos de filas. Las preguntas de observabilidad de datos admiten calificadores que puede utilizar para filtrar las consultas por un período de tiempo determinado. Para obtener más información, lea la [guía de preguntas del Asistente de IA](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general del Asistente de IA](../../ai-assistant/home.md).

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

| Función | Descripción |
| --- | --- |
| Nuevo extremo de API | Administre los metadatos del conjunto de datos de Adobe Experience Platform de forma más eficaz con el nuevo extremo [Catalog Service API /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). Actualice fácilmente atributos de conjuntos de datos complejos y profundamente anidados, ya que el sistema crea automáticamente niveles de ruta que faltan para ahorrarle tiempo, reducir los pasos manuales y minimizar los errores. |

{style="table-layout:auto"}

Para obtener más información sobre el servicio de catálogo, lea la [descripción general del servicio de catálogo](../../catalog/home.md).

## Preparación de los datos {#data-prep}

Utilice la preparación de datos para asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad mejorada para importar y exportar asignaciones | Ahora puede exportar asignaciones a un archivo CSV y configurarlas localmente en una hoja de cálculo. A continuación, puede importar las asignaciones actualizadas a Experience Platform mediante la interfaz de asignación de la interfaz de usuario. Puede utilizar esta capacidad para configurar grandes cantidades de asignaciones sin tener que crearlas manualmente en la interfaz de usuario. Además, al crear un nuevo flujo de datos, puede cargar una copia de las asignaciones directamente en Experience Platform para acelerar el flujo de trabajo. Para obtener más información, lea la guía sobre [importación y exportación de asignaciones](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Para obtener más información, lea [Resumen de la preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [(Beta) Sincronización de persona de Marketo Engage](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Utilice el conector [!DNL Marketo Engage Person Sync] para transmitir actualizaciones de audiencias de personas a los registros correspondientes de su instancia de [!DNL Marketo Engage]. Este conector de destino está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con su representante de Adobe. |
| [Disponibilidad general de la conexión CRM de Trade Desk](/help/destinations/catalog/advertising/tradedesk-emails.md) | La conexión de [!DNL The Trade Desk CRM] ya está disponible de forma general. Use [!DNL The Trade Desk] destino de CRM para activar perfiles en su cuenta de [!DNL Trade Desk] para la segmentación y supresión de audiencias en función de los datos de CRM. |
| [Conexión de perfiles de asistente de RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Utilice el destino [!DNL RainFocus Attendee Profiles] para transmitir perfiles de clientes de Adobe Experience Platform a la plataforma [!DNL RainFocus] con el fin de crear y actualizar perfiles de asistentes. |
| [Disponibilidad general de la conexión de Criteo](/help/destinations/catalog/advertising/criteo.md) | La conexión [!DNL Criteo] ya está disponible de forma general. Criteo potencia la publicidad de confianza e impactante para llevar experiencias más ricas a todos los consumidores a través de la internet abierta. Con el conjunto de datos de comercio más grande del mundo y la mejor IA de su clase, Criteo garantiza que cada punto de contacto a través del recorrido de compras esté personalizado para llegar a los clientes con el anuncio adecuado, en el momento adecuado. |
| [[!DNL Amazon Ads] conexión](../../destinations/catalog/advertising/amazon-ads.md) | El conector [!DNL Amazon Ads], anteriormente en la versión beta, ya está disponible de forma general. El conector también se ha actualizado para enviar una señal de consentimiento otorgada para todos los perfiles que han consentido que sus datos personales se utilicen para la publicidad. Obtenga más información sobre el nuevo control [Señal de consentimiento de Amazon Ads](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| Utilice etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino | Como parte de la funcionalidad [[!UICONTROL control de acceso basado en atributos]](/help/access-control/abac/overview.md) de Real-Time CDP, ahora puede aplicar etiquetas de acceso a [flujos de datos de destino](/help/dataflows/ui/monitor-destinations.md). De este modo, puede asegurarse de que solo un subconjunto de usuarios de su organización obtenga acceso a flujos de datos de destino específicos. <br> **Importante**: Al buscar flujos de datos de destino mediante el cuadro de búsqueda en la parte superior de la interfaz de usuario de Experience Platform, los resultados pueden incluir flujos de datos de destino que las etiquetas de acceso de usuario no permiten ver. Este comportamiento se corregirá en una actualización futura. |
| [Informes de nivel de audiencia](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) para la [conexión de Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Ahora puede [ver información](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sobre las identidades activadas, excluidas o fallidas desglosadas a nivel de audiencia para cada audiencia que forme parte de los flujos de datos de este destino. |
| Compatibilidad con audiencias externas para las conexiones de [TikTok](/help/destinations/catalog/social/tiktok.md) y [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Puede activar audiencias externas en estos destinos desde [cargas personalizadas](../../segmentation/ui/audience-portal.md#import-audience) y [Composición de audiencias federada](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Se ha corregido un problema en las herramientas de prueba de Destination SDK. Algunos clientes o socios encontraban problemas con la [herramienta de generación de perfiles de muestra](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) debido a un formato no admitido cuando el esquema utilizado para generar perfiles incluía tipos de datos con un selector `No format`.
- Se ha corregido un problema al actualizar la especificación de destinos `targetConnection` mediante la API de Flow Service. En algunos casos, la operación de PATCH se comportaría de manera similar a una operación de POST, lo que dañaría los flujos de datos existentes. Este problema ya está solucionado y todos los clientes pueden usar la API de Flow Service para actualizar su especificación `targetConnection`. [Más información](/help/destinations/api/edit-destination.md#patch-target-connection).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Característica actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con vistas en [!DNL Microsoft Dynamics] | Ahora puede ingerir `"entityType": "view"` al usar el origen [!DNL Microsoft Dynamics]. Para obtener más información, lee la guía de [conexión de un [!DNL Microsoft Dynamics] origen a Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de fuentes](../../sources/home.md).

## Actualizaciones de la documentación {#documentation-updates}

### Comparación de Edge Network y hub {#edge}

La comparación de [Edge Network y hub](../../landing/edge-and-hub-comparison.md) proporciona información general que detalla las diferencias entre los dos tipos de servidor para Adobe Experience Platform (hub y Edge Network), incluidos los servicios disponibles en cada tipo de servidor, las ubicaciones de los servidores y los escenarios recomendados para utilizar cada tipo de servidor.

### Referencia de API de Flow Service ampliada para fuentes de datos {#flow-service}

La [[!DNL Flow Service] referencia de API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) para las fuentes se ha actualizado con nuevos ejemplos de solicitud y respuesta de API. Utilice la referencia de API expandida para crear y actualizar las especificaciones de conexión al integrar su propio origen en Experience Platform. También puede utilizar la referencia de API expandida para realizar transiciones de estado en las entidades de origen, actualizar las conexiones de origen y destino existentes y recuperar flujos y especificaciones de flujo según un criterio de filtrado específico.

### Hacer copia de seguridad de configuraciones de objeto mediante herramientas de zona protegida {#back-up-object-configurations}

Lea la [guía de configuración de objetos de copia de seguridad](../../sandboxes/use-cases/backup-object-configuration.md) para obtener instrucciones paso a paso sobre cómo crear un paquete de copia de seguridad con las herramientas de espacio aislado para asegurarse de que las configuraciones de los objetos estén almacenadas y protegidas.

### Activación de un centro de excelencia mediante herramientas de zona protegida {#center-of-excellence}

Lea la [guía del centro de excelencia](../../sandboxes/use-cases/center-of-excellence.md) para obtener instrucciones paso a paso sobre cómo crear un paquete de &quot;zona protegida dorada&quot; que actúe como un centro de excelencia para compartir configuraciones clave de manera eficiente.

### Retención de conjuntos de datos de eventos de experiencia en el lago de datos {#experience-event-dataset-retention}

Tome el control de la retención de conjuntos de datos de eventos de experiencia en Adobe Experience Platform mediante el tiempo de vida (TTL). [Esta guía](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) le explica cómo evaluar, configurar y administrar la configuración de TTL para eliminar automáticamente registros obsoletos, optimizar el almacenamiento y mantener los datos relevantes. Descubra prácticas recomendadas, casos de uso reales y consideraciones clave para mejorar la administración del ciclo de vida de los datos.
