---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2025'
description: Las notas de la versión de marzo de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 16056a35624b4a053e9f50acef0ec3f63254a065
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 26%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 26 de marzo de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Notas de la versión de Adobe Experience Platform](#adobe-experience-platform-release-notes)

   - [Paneles](#dashboards)
   - [Destinos](#destinations)
   - [Servicio de segmentación](#segmentation-service)
   - [Fuentes](#sources)

## Paneles {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Panel de uso de licencias basado en métricas | El panel de uso de licencias ahora incluye una interfaz de usuario optimizada con dos fichas: **Métricas** y **Productos**. La nueva pestaña **Métricas** ofrece una vista consolidada de todas las métricas de licencias a las que se puede realizar un seguimiento en los productos comprados. Cada métrica incluye un icono de información en línea que muestra descripciones y productos asociados. Los usuarios pueden seleccionar zonas protegidas de producción o desarrollo, ver las tendencias de uso históricas en gráficos interactivos y exportar datos específicos de zonas protegidas como archivos CSV. Estas actualizaciones agilizan el seguimiento de las licencias y ofrecen perspectivas más claras. Obtenga más información en la [guía del tablero de uso de licencias](../../dashboards/guides/license-usage.md) para obtener más detalles. |
| Frecuencia de predicción actualizada | El panel de uso de licencias ahora proporciona información más precisa sobre el consumo proyectado al actualizar las predicciones de **uso semanalmente** en lugar de mensualmente. Estos pronósticos muestran el uso estimado para las próximas seis semanas en función de las tendencias recientes. Este cambio permite una toma de decisiones más rápida, una intervención más temprana y una mejor planificación de licencias. Consulte la guía](../../dashboards/guides/license-usage.md#predicted-usage) de panel sobre el uso de licencias [para obtener más información. |
| Se han actualizado las descripciones de Métrica en IU | Se han revisado las definiciones de métricas en el panel de uso de licencias para mantener la claridad y la coherencia. Ahora puede ver las descripciones actualizadas directamente en el panel mediante los iconos de información en línea junto a cada métrica en la pestaña **Métricas**. Estas actualizaciones facilitan la comprensión de cómo se realiza el seguimiento de las métricas y a qué productos se aplican. Consulte la guía de panel](../../dashboards/guides/license-usage.md#available-metrics) sobre el uso de licencias [para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [Conexión Personas de Demandbase](/help/destinations/catalog/advertising/demandbase-people.md) | Utilice la conexión [!DNL Demandbase People] para activar perfiles para sus campañas de Demandbase para la segmentación, personalización y supresión de audiencias. |
| [Conexión a cuenta de Bombora](/help/destinations/catalog/advertising/bombora.md) | Utilice la conexión [!DNL Bombora] para activar perfiles para sus campañas Bombora de segmentación, personalización y supresión de audiencias, según [audiencias de cuenta](/help/segmentation/types/account-audiences.md). |
| Actualización de [Atributos del dirigible](/help/destinations/catalog/mobile-engagement/airship-attributes.md) | A partir del 25 de marzo de 2025, verá dos tarjetas de **[!UICONTROL Atributos de dirigible]** en paralelo en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino **[!UICONTROL Atributos de dirigible]** existente a **[!UICONTROL (obsoleto) Atributos de dirigible]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Atributos de dirigible]**. <br> Use la conexión **[!UICONTROL Atributos de dirigible]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino [!DNL (Deprecated) Airship Attributes], se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. <br> Si está creando flujos de datos a través de la [API de Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar sus [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores: <ul><li> Id. de especificación de flujo: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> ID de especificación de conexión: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| [Mejoras en la precisión de la creación de informes para destinos de streaming](../../dataflows/ui/monitor-destinations.md) | A partir de marzo de 2025, Adobe Systems implementará una actualización para aumentar la precisión sistema de informes para los destinos de transmisión. Esta mejora garantiza una mejor alineación entre los informes de Experience Platform y las plataformas de destino. <br> Antes de esta actualización, **[!UICONTROL Identities failed]** incluía todos los reintentos de activación. Después de esta actualización, solo se incluye el último reintento de activación en el recuento total. <br> Esta mejora se aplica a todos los destinos de flujo continuo. <br> Tras esta mejora, es posible que los usuarios de destinos de streaming vean una caída esperada en su recuento de **[!UICONTROL Identidades con errores]**. |
| [Compatibilidad de exportación de campos de tipo mapa para destinos de empresa y Edge](/help/destinations/ui/export-arrays-maps-objects.md) | Al exportar datos a los destinos [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) y [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), ahora puede seleccionar campos de tipo mapa para exportar en el paso de asignación del flujo de trabajo de activación. <br> ![Exportar campo de tipo de mapa a destino de empresa.](../2025/assets/march/export-map.png "Exportar campo de tipo de asignación a destino de empresa."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de destinos](../../destinations/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| ------- | ----------- |
| Mejoras del Audience Builder de la cuenta | Dentro de Audience Builder, ahora puede filtrar atributos para mostrar solo los atributos completados, así como vista datos de resumen para estos atributos completados. Puede encontrar más información sobre estas mejoras en la documentación del [Audience Builder](../../rtcdp/segmentation/audience-builder.md) . |
| Evaluación de audiencia flexible disponibilidad general | Ya está disponible de forma general una evaluación flexible de audiencias. Puede utilizar la evaluación de audiencia flexible para crear nuevas audiencias bajo demanda para comunicaciones urgentes. Puede encontrar más información sobre la evaluación de audiencia flexible en la descripción general](../../segmentation/methods/flexible-audience-evaluation.md) de evaluación de [audiencia flexible. |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Orígenes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Nuevos orígenes**

| Función | Descripción |
| --- | --- |
| [!DNL Bombora Intent] | El origen [!DNL Bombora Intent] está ahora disponible en el catálogo de orígenes. Utilice esta fuente para: <ul><li>Integre los datos de la empresa Bombora Surge Intent para identificar cuentas que investiguen activamente sus productos o servicios.</li><li>Priorice las cuentas en el mercado para crear segmentos precisos y ejecutar campañas de ABM con objetivos hiperdefinidos, lo que garantiza que los esfuerzos de marketing se centren en las cuentas que tienen más probabilidades de convertirse.</li><li>Aproveche las estrategias basadas en la intención para optimizar el gasto en publicidad, impulsar la participación y maximizar el ROI.</li></ul> Para obtener más información, lee la guía de [conexión de tu cuenta de  [!DNL Bombora] a Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | El origen [!DNL Demandbase Intent] ahora está disponible en el catálogo de orígenes. Utilice esta fuente para: <ul><li>Integre los datos de intención de cuenta de Demandbase para identificar cuentas de alto interés en función de participaciones en tiempo real.</li><li>Al priorizar las señales de intención más fuertes, puede crear segmentos precisos y entregar campañas hiperorientadas para garantizar que sus esfuerzos de marketing enfocar en las cuentas con más probabilidades de convertir.</li><li>Active estrategias basadas en intención para permitir la optimización del gasto en anuncios, el aumento de la participación y una mayor Retorno de la inversión.</li></ul> Para obtener más información, lea el guía sobre [cómo conectar su [!DNL Demandbase] cuenta a Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en el [!DNL Google Ads] origen | Ahora puede utilizar el [[!DNL Google Ads] origen](../../sources/connectors/advertising/ads.md) para ingerir agregado datos. Puede utilizar el [!DNL Google Ads Query Builder] para especificar los atributos, segmentos y recursos que desea ingerir para Experience Platform. Para obtener más información, lea el guía sobre [cómo conectar su [!DNL Google Ads] cuenta a Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Mejoras en el [!DNL Microsoft Dynamics] origen | Ahora puede especificar la clave principal de una tabla determinada [!DNL Microsoft Dynamics] al explorar el contenido y la estructura de los datos. Utilice esta característica para optimizar las consultas con el origen [!DNL Microsoft Dynamics]. Para obtener más información, lee la guía sobre [conectar tu [!DNL Microsoft Dynamics] origen a Experience Platform mediante la API](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Compatibilidad con la autenticación de claves de API en fuentes de autoservicio (SDK por lotes) | Ahora puede utilizar la autenticación de clave de API como tipo de autenticación al integrar una nueva fuente con fuentes de autoservicio (SDK por lotes). Para obtener más información, lea la guía sobre [configuración de la especificación de autenticación en SDK por lotes](../../sources/sources-sdk/config/authspec.md). |
| Compatibilidad con el control de acceso basado en atributos en orígenes | Ahora puede utilizar funciones de control de acceso basadas en atributos en flujos de datos de origen. Lea las siguientes guías para obtener más información: <ul><li>[Aplicar etiquetas a los flujos de datos de origen mediante la API](../../sources/tutorials/api/labels.md)</li><li>[Aplicar etiquetas a los flujos de datos de origen mediante el IU](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de fuentes](../../sources/home.md).
