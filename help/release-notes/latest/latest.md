---
title: Notas de la versión de Adobe Experience Platform, junio de 2025
description: Las notas de la versión de junio de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c78dc0e83976499403e066b314a0889df803c976
workflow-type: ht
source-wordcount: '1665'
ht-degree: 100%

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

**Fecha de publicación: 18 de junio de 2025**

Estas son las nuevas funciones y actualizaciones de las existentes en Adobe Experience Platform:

- [Control de acceso](#access-control)
- [Administración avanzada del ciclo de vida de los datos](#advanced-data-lifecycle-management)
- [Servicio de catálogo](#catalog-service)
- [Paneles](#dashboards)
- [Gobernanza de datos](#data-governance)
- [Destinos](#destinations)
- [Composición de público federado](#fac)
- [Privacy Service](#privacy-service)
- [Zonas protegidas](#sandboxes)
- [Segmentación](#segmentation-service)
- [Fuentes](#sources)

## Control de acceso {#access-control}

Experience Platform aprovecha los perfiles de producto de [Adobe Admin Console](https://adminconsole.adobe.com) para vincular a usuarios con permisos y zonas protegidas. Los permisos controlan el acceso a una variedad de funciones de Experience Platform, incluido el modelado de datos, la administración de perfiles y la administración de zonas protegidas.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Permiso para exportar datos del panel | Las opciones **[!UICONTROL Descargar CSV]** y **[!UICONTROL Enviar como correo electrónico]** en los paneles ahora requieren el permiso **[!UICONTROL Exportar datos del panel]**. Este permiso garantiza que solo los usuarios autorizados puedan exportar los datos de conocimiento tabulados, lo que admite una gobernanza y políticas de control de acceso a datos más estrictas. Lea la sección de [permisos de la guía de control de acceso](../../access-control/home.md#permissions) para obtener más información. |

Para obtener más información, lea la [información general del control de acceso](../../access-control/home.md).

## Administración avanzada del ciclo de vida de los datos {#advanced-data-lifecycle-management}

Experience Platform proporciona un conjunto de funcionalidades de higiene de datos que le permiten administrar los datos almacenados mediante eliminaciones programáticas de registros de consumidores y conjuntos de datos. Con el espacio de trabajo de Data Lifecycle en la interfaz de usuario o a través de llamadas a la API de Data Hygiene, puede administrar de forma eficaz los almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas organizativas lo consideran necesario.

**Nueva documentación**

| Nueva documentación | Descripción |
| --- | --- |
| Disponibilidad para eliminar registros generales | Ahora puede eliminar registros individuales basados en campos de identidad mediante la interfaz de usuario o la API. Esta función reduce el almacenamiento, aplica gobernanzas y mejora la higiene de los datos al permitir eliminaciones de un único conjunto de datos o de todos ellos. Se aplican límites de volumen y requisitos de derechos. Lea la [guía para eliminar registros](../../hygiene/ui/record-delete.md) para obtener más información. |

Para obtener más información, lea la [información general de la administración avanzada del ciclo de vida de los datos](../../hygiene/home.md).

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Vista previa de conjunto de datos mejorada: navegación más rápida y perspectivas más claras | Obtenga una vista previa rápida de los datos del conjunto de datos, vea las consultas SQL subyacentes y explore hasta 100 filas con un filtrado mejorado y una visibilidad de estructura más clara, todo ello dentro de la conocida experiencia de vista previa del conjunto de datos. Lea la [guía del usuario de los conjuntos de datos](../../catalog/datasets/user-guide.md#preview) para obtener más información. |

{style="table-layout:auto"}

## Paneles {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Opción Enviar como exportación de correo electrónico | Ahora puede exportar hasta 10 000 registros desde los paneles del modo Query Pro seleccionando **[!UICONTROL Enviar como correo electrónico]** en el menú **[!UICONTROL Ver más]**. Esta opción envía de forma segura un vínculo de descarga al correo electrónico asociado a Adobe para exportaciones más grandes. Lea la [guía Ver más](../../dashboards/sql-insights-query-pro-mode/view-more.md#export) para obtener más información. |

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Gobernanza de datos {#data-governance}

La gobernanza de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña una función clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de acceso a los datos y el control de acceso de los datos para las acciones de marketing.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Configuración de alertas CMK de Azure y Listas de IP permitidas | Ahora puede añadir a la lista de permitidas la dirección IP estática de Adobe en Azure Key Vault para garantizar un acceso continuo cuando las restricciones de red estén habilitadas. Esto evita interrupciones en los servicios de Platform debido al acceso restringido a las claves. |
| Alertas y resoluciones de configuración de CMK | Experience Platform ahora genera alertas cuando los servicios de Adobe pierden el acceso a Azure Key Vault (por ejemplo, debido a entradas eliminadas de la lista de IP permitidas o claves deshabilitadas). Esta nueva guía le ayuda a comprender cada alerta y a tomar acciones correctivas. |

Para obtener más información, consulte la [Información general sobre la gobernanza de datos](../../data-governance/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| --- | --- |
| [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md) conexión | Utilice el destino [!DNL Algolia] para ofrecer una personalización coherente en todos los sitios desde la página de inicio hasta la búsqueda. Cree audiencias enriquecidas a partir de varias fuentes de datos y compártalas en varios canales para mejorar las estrategias de segmentación y la personalización de campañas. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de la [Segmentación por lista de clientes de Google + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) | El destino de la Segmentación por lista de clientes de Google + DV360 ya está disponible para todos los usuarios de Experience Platform. La documentación ahora incluye instrucciones detalladas para [vincular cuentas publicitarias](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) entre [!DNL Adobe] y [!DNL Google]. |
| [Monitorización a nivel de audiencia](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) para destinos de streaming | La monitorización a nivel de audiencia ya está disponible para los siguientes destinos: <ul><li>[[!DNL (API) Oracle Eloqua] conexión](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Compatibilidad con identificadores adicionales para destinos de [Facebook](../../destinations/catalog/social/facebook.md#supported-identities) | El destino [!DNL Facebook] ahora admite la asignación de nuevos campos de direcciones relacionados para mejorar la segmentación y la coincidencia con perfiles en propiedades de Facebook. Para obtener más información sobre los nuevos campos relacionados con direcciones, consulte la sección [identidades admitidas](../../destinations/catalog/social/facebook.md#supported-identities). <br> ![Imagen de la interfaz de usuario de la plataforma que muestra los campos adicionales para Facebook.](../2025/assets/june/facebook-destination-fields.png "Imagen de la interfaz de usuario de la plataforma que muestra los campos adicionales para Facebook."){width="200" align="center" zoomable="yes"} |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) actualización de destino | Desde el 19 de junio de 2025, puede ver dos tarjetas **[!DNL Braze]** una al lado de la otra en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino [!DNL Braze] existente a **[!UICONTROL Braze (obsoleto)]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Braze]**. <br> Use la conexión **[!UICONTROL Braze]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino **[!UICONTROL Braze (obsoleto)]**, se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. <br> Si está creando flujos de datos a través de la [API del servicio de flujo](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar su [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores: <ul><li>ID de especificación de flujo: `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>ID de especificación de conexión: `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Composición de público federado {#fac}

La composición de público federado permite a las empresas componer datos para una mejor aplicación en varios casos de uso. Con este nuevo enfoque, como usuario de Adobe Real-time Customer Data Platform y/o Adobe Journey Optimizer, puede federar conjuntos de datos directamente desde su almacén de datos existente para crear y enriquecer públicos y atributos de Adobe Experience Platform en un solo sistema.

| Nueva función | Descripción |
| ----------- | ----------- |
| Disponibilidad general para clientes de Adobe Healthcare Shield | A finales de junio, la composición de público federado estará disponible para los clientes de Adobe Healthcare Shield para la creación de audiencias y casos de uso de enriquecimiento y enriquecimiento de perfiles. Para obtener más información sobre las medidas de seguridad y privacidad de la Composición de público federado, lea la [información general sobre la seguridad y la privacidad en la Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/start/privacy-security). Para obtener más información sobre la conformidad con HIPAA de los productos de Experience Platform en general, lea la [Información general sobre HIPAA y los productos y servicios de Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Para obtener más información, lea la documentación de la [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Varias regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos personales de clientes y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
| --- | ---|
| Compatibilidad con las leyes de privacidad de Tennessee y Minnesota | Privacy Service ahora es compatible con la Ley de Protección de Información de Tennessee (`tipa_tn_usa`) y la Ley de Privacidad de Datos del Consumidor de Minnesota (`mcdpa_mn_usa`). Puede procesar las solicitudes de acceso y eliminación de acuerdo con estas nuevas regulaciones de nivel de estado. Consulte la [información general sobre regulaciones](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/regulations/overview) para obtener más detalles. |

Consulte la [información general de Privacy Service](../../privacy-service/home.md) para obtener más información sobre el servicio.

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Migración de actualizaciones de configuraciones de objeto | Ahora puede migrar las actualizaciones de configuraciones de objeto iterativas entre zonas protegidas después de la replicación inicial. Esta mejora admite flujos de trabajo de desarrollo en los que las configuraciones deben actualizarse y propagarse entre entornos sin volver a crear toda la configuración de la zona protegida. Para obtener más información, lea la guía sobre [transferencia de actualizaciones de configuración entre zonas protegidas](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de disponibilidad de perspectivas de similitud | Las perspectivas y audiencias de similitud se desactivan automáticamente en entornos que muestran un uso bajo. Un uso bajo se define como no ver perspectivas de similitud durante los últimos tres meses o no crear un público de similitud durante los últimos seis meses. Encontrará más detalles sobre este cambio en la [Guía de públicos de similitud](../../segmentation/types/lookalike-audiences.md). |

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la interfaz de usuario [!BADGE Beta]{type=Informative} para [!DNL Azure Databricks] | Ahora puede conectar su cuenta de [!DNL Azure Databricks] a Experience Platform mediante el espacio de trabajo de fuentes en la interfaz de usuario. Lea la guía de [conexión [!DNL Databricks] con Experience Platform en la interfaz de usuario](../../sources/connectors/databases/databricks.md) para obtener más información. |
| Compatibilidad con un nuevo tipo de autenticación para [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] ahora también admitirá la autenticación principal de servicio, además de la autenticación de cadena de conexión existente. Para obtener más información, consulte la [[!DNL Azure Synapse Analytics] información general sobre autenticación](../../sources/connectors/databases/synapse-analytics.md). |
| [!DNL Salesforce] desuso de autenticación básica | La autenticación básica de [Salesforce CRM](../../sources/connectors/crm/salesforce.md) y [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) quedará obsoleta en enero de 2026. Los clientes deben migrar a la autenticación OAuth 2.0 para mantener la conectividad. Este cambio afecta a los conectores de origen y garantiza una seguridad mejorada y el cumplimiento de los estándares de autenticación de Salesforce. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).
