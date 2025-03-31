---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2025'
description: Las notas de la versión de marzo de 2025 de Adobe Experience Platform.
exl-id: 3da1c912-2581-4afa-bd21-0b8303531dcd
source-git-commit: edcdf84a8cb954c15f7dd235fb14cf14e11e22c8
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 95%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de marzo de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Notas de la versión de Adobe Experience Platform](#adobe-experience-platform-release-notes)
   - [Paneles](#dashboards)
   - [Destinos](#destinations)
   - [Composición de público federado](#federated-audience-composition)
   - [Servicio de segmentación](#segmentation-service)
   - [Fuentes](#sources)

## Paneles {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Panel de uso de licencias basadas en métricas | El panel de uso de licencias ahora incluye una interfaz de usuario optimizada con dos pestañas: **Métricas** y **Productos**. La nueva pestaña **Métricas** ofrece una vista consolidada de todas las métricas de licencias de las que se puede realizar un seguimiento en los productos comprados. Cada métrica incluye un icono de información en línea que muestra las descripciones y los productos asociados. Los usuarios pueden seleccionar zonas protegidas de producción o desarrollo, ver las tendencias de uso históricas en gráficos interactivos y exportar datos específicos de zonas protegidas como archivos CSV. Estas actualizaciones agilizan el seguimiento de las licencias y ofrecen perspectivas más claras. Obtenga más información en la [guía del panel de uso de licencias](../../dashboards/guides/license-usage.md) para obtener más detalles. |
| Frecuencia de predicción actualizada | El panel de uso de licencias ahora proporciona una perspectiva más precisa del consumo proyectado al actualizar las predicciones de uso **semanalmente** en lugar de mensualmente. Estas previsiones muestran el uso estimado durante las seis próximas semanas en función de las tendencias recientes. Este cambio permite una toma de decisiones más rápida, una intervención más temprana y una mejor planificación de las licencias. Consulte la [Guía de paneles de uso de licencias](../../dashboards/guides/license-usage.md#predicted-usage) para obtener más detalles. |
| Descripciones de métricas actualizadas en la IU | Se han revisado las definiciones de las métricas en el panel de uso de licencias para mayor claridad y coherencia. Ahora puede ver las descripciones actualizadas directamente en el panel mediante los iconos de información en línea junto a cada métrica en la pestaña **Métricas**. Estas actualizaciones facilitan la comprensión de cómo se realiza el seguimiento de las métricas y a qué productos se aplican. Consulte la [Guía de paneles de uso de licencias](../../dashboards/guides/license-usage.md#available-metrics) para obtener más detalles. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [Conexión Personas de Demandbase](/help/destinations/catalog/advertising/demandbase-people.md) | Utilice la conexión [!DNL Demandbase People] para activar perfiles para sus campañas de Demandbase para la segmentación, personalización y supresión de audiencias. |
| [Conexión a cuenta de Bombora](/help/destinations/catalog/advertising/bombora.md) | Utilice la conexión [!DNL Bombora] para activar perfiles para sus campañas Bombora de segmentación, personalización y supresión de audiencias, según [audiencias de cuenta](/help/segmentation/types/account-audiences.md). |
| Actualización de [Atributos de Airship](/help/destinations/catalog/mobile-engagement/airship-attributes.md) | Desde el 25 de marzo de 2025, puede ver dos tarjetas de **[!UICONTROL Atributos de Airship]** una al lado de la otra en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino existente **[!UICONTROL Atributos de Airship]** por el de **[!UICONTROL (Obsoleto) Atributos de Airship]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Atributos de Airship]**. <br> Use la conexión **[!UICONTROL Atributos de Airship]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino [!DNL (Deprecated) Airship Attributes], se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. <br> Si está creando flujos de datos a través de la [API del servicio de flujo](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar su [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores: <ul><li> ID de especificación de flujo: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> ID de especificación de conexión: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| [Mejoras en la precisión de la creación de informes para destinos de streaming](../../dataflows/ui/monitor-destinations.md) | Desde marzo de 2025, Adobe está implementando gradualmente una actualización para aumentar la precisión de la creación de informes en los destinos de streaming. Esta mejora garantiza una mejor alineación entre la creación de informes en Experience Platform y la creación de informes en las plataformas de destino. <br> Antes de esta actualización, **[!UICONTROL Identities failed]** incluía todos los reintentos de activación. Después de esta actualización, solo se incluye el último reintento de activación en el recuento total. <br> Esta mejora se aplica a todos los destinos de streaming. <br>Tras esta mejora, es posible que los usuarios de los destinos de streaming puedan detectar un descenso previsto en su recuento de **[!UICONTROL Identidades fallidas]**. |
| [Compatibilidad de la exportación de campos de tipo de asignación para destinos de empresa y perimetrales](/help/destinations/ui/export-arrays-maps-objects.md) | Al exportar datos a los destinos [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [API HTTP](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) y [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), ahora puede seleccionar campos de tipo de asignación para la exportación en el paso de asignación del flujo de trabajo de activación. <br> ![Exporte el campo de tipo de asignación al destino de empresa.](../2025/assets/march/export-map.png "Exporte el campo de tipo de asignación al destino de empresa."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de destinos](../../destinations/home.md).

## Composición de público federado {#federated-audience-composition}

Para obtener información sobre las últimas actualizaciones de Federated Audience Composition, lea las [notas de la versión](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes) aquí.

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| ------- | ----------- |
| Mejoras en Account Audience Builder | En el creador de audiencias, ahora puede filtrar atributos para mostrar únicamente los atributos rellenados, así como ver los datos de resumen de estos atributos rellenados. Encontrará más información sobre esta nueva función en la documentación sobre [Audience Builder](../../rtcdp/segmentation/audience-builder.md). |
| Evaluación flexible de audiencias (disponibilidad general) | Ya está disponible de forma general una evaluación flexible de audiencias. Puede utilizar una evaluación flexible de audiencias para crear nuevas audiencias bajo demanda para comunicaciones urgentes. Encontrará más información sobre la evaluación flexible de audiencias en la [información general sobre la evaluación flexible de audiencias](../../segmentation/methods/flexible-audience-evaluation.md). |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Nuevos orígenes**

| Función | Descripción |
| --- | --- |
| [!DNL Bombora Intent] | La fuente de [!DNL Bombora Intent] ya está disponible en el catálogo de fuentes. Utilice esta fuente para: <ul><li>Integrar los datos de intención de Bombora&#39;s Company Surge para identificar cuentas que investiguen activamente sus productos o servicios.</li><li>Priorizar las cuentas en el mercado para crear segmentos precisos y ejecutar campañas de ABM con objetivos hiperdefinidos, lo que garantiza que los esfuerzos de marketing se centren en las cuentas que tienen más probabilidades de convertirse.</li><li>Aprovechar las estrategias basadas en la intención para optimizar el gasto en publicidad, impulsar la participación y maximizar el retorno de la inversión.</li></ul> Para obtener más información, lea la guía sobre [la conexión de su cuenta de  [!DNL Bombora]  a Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | La fuente de [!DNL Demandbase Intent] ya está disponible en el catálogo de fuentes. Utilice esta fuente para: <ul><li>Integrar los datos de intención de cuenta de Demandbase para identificar cuentas de alto interés en función de participaciones en tiempo real.</li><li>Al priorizar las señales de intención más sólidas, puede crear segmentos precisos y ofrecer campañas con objetivos hiperdefinidos para garantizar que los esfuerzos de marketing se centren en las cuentas con más probabilidades de conversión.</li><li>Activar estrategias basadas en la intención para permitir la optimización del gasto en publicidad, una mayor participación y un retorno de la inversión más alto.</li></ul> Para obtener más información, lea la guía sobre [la conexión de su cuenta de  [!DNL Demandbase]  a Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la fuente de [!DNL Google Ads] | Ahora puede usar la [[!DNL Google Ads] fuente](../../sources/connectors/advertising/ads.md) para ingerir datos agregados. Puede usar [!DNL Google Ads Query Builder] para especificar los atributos, segmentos y recursos que desea introducir en Experience Platform. Para obtener más información, lea la guía sobre [la conexión de su cuenta de  [!DNL Google Ads]  a Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Mejoras en la fuente de [!DNL Microsoft Dynamics] | Ahora puede especificar la clave principal de una tabla de [!DNL Microsoft Dynamics] determinada al explorar el contenido y la estructura de los datos. Utilice esta característica para optimizar las consultas con la fuente de [!DNL Microsoft Dynamics]. Para obtener más información, lea la guía sobre [la conexión de su fuente  [!DNL Microsoft Dynamics]  a Experience Platform con la API](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Compatibilidad con la autenticación de claves de API en Self-Serve Sources (Batch SDK) | Ahora puede utilizar la autenticación de claves de API como tipo de autenticación al integrar una nueva fuente con Self-Serve Sources (Batch SDK). Para obtener más información, lea la guía sobre [configuración de la especificación de autenticación en SDK por lotes](../../sources/sources-sdk/config/authspec.md). |
| Compatibilidad con el control de acceso basado en atributos en las fuentes | Ahora puede utilizar funciones de control de acceso basadas en atributos para los flujos de datos de sus fuentes. Lea las siguientes guías para obtener más información: <ul><li>[Aplicar etiquetas a los flujos de datos de sus fuentes mediante la API](../../sources/tutorials/api/labels.md)</li><li>[Aplicar etiquetas a los flujos de datos de sus fuentes mediante la interfaz de usuario](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).
