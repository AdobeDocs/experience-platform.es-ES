---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2024'
description: Las notas de la versión de febrero de 2024 de Adobe Experience Platform.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1238'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 21 de febrero de 2024**

Actualizaciones de funciones existentes en Experience Platform:

- [Alertas](#alerts)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Pestaña Historial de alertas | Como administrador de Experience Platform, puede utilizar la función Gestionar suscriptores de alertas para asignar una alerta a un ID de usuario de Adobe, a una dirección de correo electrónico externa o a una lista de grupos de correo electrónico. Para obtener más información, consulte la [documentación de la IU de alertas](../../observability/alerts/ui.md) para obtener más información sobre la pestaña del historial. |

{style="table-layout:auto"}

Para obtener más información acerca de las alertas, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [Compatibilidad con mensajería en la aplicación web en el SDK web](../../web-sdk/personalization/web-in-app-messaging.md) | El SDK web de Adobe Experience Platform ahora admite la configuración de mensajería web en la aplicación para campañas de Adobe Journey Optimizer. |

{style="table-layout:auto"}

Para obtener más información acerca de las colecciones de datos, lea la [información general de colecciones de datos](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [Conexión PX de Gainsight](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX es una plataforma de experiencia del producto que permite a los equipos de productos comprender cómo utilizan los usuarios sus productos, recopilar comentarios y crear participaciones en la aplicación, como tutoriales de productos, para impulsar la incorporación del usuario y la adopción del producto. |
| [Conexión de etiquetas de Mailchimp](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp es una popular plataforma de automatización de marketing y servicio de marketing por correo electrónico. Puede usar el conector de Etiquetas de Mailchimp para estructurar, etiquetar o categorizar sus contactos. |
| [Conexión de SAP Commerce](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce es una solución de plataforma de comercio electrónico basada en la nube para empresas B2B y B2C, y está disponible como parte del catálogo de productos de SAP Customer Experience. Puede utilizar este destino para actualizar los detalles del cliente en SAP Commerce desde un público de Experience Platform existente. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Activar públicos de cuenta disponibles de forma general | La funcionalidad para activar públicos de cuenta en determinados destinos ya está disponible de forma general para empresas que compran las ediciones de Real-time Customer Data Platform [De empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [De empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p). Lea el tutorial sobre [activación de públicos de cuenta](/help/destinations/ui/activate-account-audiences.md) para obtener información completa, incluidos los destinos admitidos. |
| Herramientas de aplicación de consentimientos de Ley de mercados digitales para destinos de Google | Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) y la [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para admitir los requisitos relacionados con el cumplimiento y el consentimiento definidos en la [Ley de mercados digitales](https://digital-markets-act.ec.europa.eu/index_es) (DMA) de la Unión Europea ([Política de consentimiento del usuario de la UE](https://www.google.com/about/company/user-consent-policy/)). Se espera que la aplicación de estos cambios en los requisitos de consentimiento entre en vigor a partir del 6 de marzo de 2024. <br/><br/> Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de público para usuarios del Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que aprueban el consentimiento del usuario final al cargar datos de público. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según la DMA en la Unión Europea.<br/><br/>Los clientes que hayan adquirido Adobe Privacy &amp; Security Shield y hayan configurado una [política de consentimiento](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos no necesitan realizar ninguna acción.<br/><br/>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben usar las funciones de [definición de segmento](../../segmentation/home.md#segment-definitions) del [Generador de segmentos](../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos y así poder seguir usando los destinos de Real-Time CDP Google existentes sin interrupción. |
| [!BADGE Beta]{type=Informative} Reordenar los campos de asignación para destinos por lotes | Ahora puede cambiar el orden de las columnas en sus exportaciones de CSV arrastrando y soltando los campos de asignación en el paso de [asignación](../../destinations/ui/activate-batch-profile-destinations.md#mapping). El orden de los campos asignados en la IU se refleja en el orden de las columnas del archivo CSV exportado, de arriba a abajo, siendo la fila superior la columna situada más a la izquierda en el archivo CSV. <br/><br/> Esta función está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso a esta función, póngase en contacto con el representante del Adobe. |
| [!BADGE Beta]{type=Informative} Programaciones de exportación predeterminadas preseleccionadas para destinos por lotes | Experience Platform ahora establece automáticamente una programación predeterminada para cada exportación de archivo. Consulte la documentación sobre [exportaciones de público de programación](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) para obtener información sobre cómo modificar la programación predeterminada. <br/><br/> Esta función está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso a esta función, póngase en contacto con el representante del Adobe. |
| [!BADGE Beta]{type=Informative} Editar programaciones de activación de público por lotes para destinos por lotes | Ahora puede editar de forma masiva la programación de activación para varios públicos desde la página [Datos de activación](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br/><br/> Esta función está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso a esta función, póngase en contacto con el representante del Adobe. |
| [!BADGE Beta]{type=Informative} Exportación masiva de archivos On-demand a destinos por lotes | Ahora puede exportar públicos de forma masiva a destinos por lotes mediante la funcionalidad [exportar archivos bajo demanda](../../destinations/ui/export-file-now.md). <br/><br/> Esta función está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso a esta función, póngase en contacto con el representante del Adobe. |

{style="table-layout:auto"}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para responder a esta necesidad, Experience Platform proporciona zonas protegidas que dividen una única instancia de Experience Platform en entornos virtuales separados para ayudar a que se desarrollan y evolucionen las aplicaciones de experiencia digital.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Herramientas de zona protegida | Además de admitir tipos de objetos para reglas de consentimiento y control, utilice las herramientas de la zona protegida para importar esquemas sin perfiles unificados habilitados, compruebe la ausencia de atributos en la zona protegida de destino al importar un segmento y utilice de forma predeterminada la política de combinación existente. Para obtener más información sobre estas características, consulte la [guía de la IU de herramientas de zona protegida](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Experience Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Nueva funcionalidad**

| Función | Descripción |
| ------- | ----------- |
| Públicos de la cuenta | Los públicos de cuenta ya están disponibles de forma general. Ahora puede utilizar la segmentación de cuentas para proporcionar facilidad y sofisticación totales de la experiencia de segmentación de marketing de públicos basados en personas a públicos basados en cuentas en las ediciones B2B y B2P de Real-Time Customer Experience Platform. Esta versión permite utilizar públicos basados en personas como predicado para públicos basados en cuentas, añade funcionalidades de búsqueda, admite el uso de entidades personalizadas y cumple con la gobernanza de datos. Para obtener más información acerca de esta característica, lea la [información general de los públicos de la cuenta](../../segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] origen | Use la [[!DNL Acxiom Prospecting Data Import] fuente](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) para recuperar y asignar datos del servicio del cliente potencial [!DNL Acxiom] a Experience Platform. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
