---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2024'
description: Las notas de la versión de marzo de 2024 de Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1188'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 19 de marzo de 2024**

>[!TIP]
>
>Utilice el [glosario de Adobe Experience Platform](/help/landing/glossary.md) para familiarizarse con la terminología utilizada en Real-time Customer Data Platform y Adobe Experience Platform. Si no encuentra un término específico que esté buscando, utilice las opciones de comentarios de la página para solicitar que se añadan nuevos términos al glosario.

Actualizaciones de funciones existentes en Experience Platform:

- [Servicio de catálogo](#catalog-service)
- [Recopilación de datos](#data-collection)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

| Función | Descripción |
| --- | --- |
| Más acciones | Para que las operaciones sean más flexibles y le ayuden a administrar sus datos, ahora puede utilizar la función “Más acciones” de la vista de detalles para realizar tareas adicionales en un conjunto de datos. Puede eliminar el conjunto de datos o habilitarlo para utilizarlo con el Perfil del cliente en tiempo real desde la página de detalles de un conjunto de datos elegido.<br>**Nota:** si habilita un conjunto de datos para la ingesta de perfiles, el esquema del conjunto de datos debe ser compatible con el Perfil del cliente en tiempo real.<br>![Espacio de trabajo de conjuntos de datos con el menú desplegable [!UICONTROL ... Más] resaltado.](../2024/assets/march/more-actions.png "Espacio de trabajo de conjuntos de datos con el menú desplegable Más resaltado."){width="100" zoomable="yes"}.<br>Lea la documentación de la [guía del usuario de conjuntos de datos](../../catalog/datasets/user-guide.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre el servicio de consultas, consulte la [información general del servicio de catálogo](../../catalog/home.md).

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas funciones de asignación para Adobe Analytics | Ahora puede utilizar las siguientes funciones para extraer datos de evento de Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Para obtener más información sobre estas funciones, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea [Información general de preparación de datos](../../data-prep/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Extensiones | [!DNL Merkury] Extensión de etiqueta | La [[!DNL Merkury] extensión de etiqueta](https://exchange.adobe.com/apps/ec/600027/merkury-tag) proporciona tasas de coincidencia líderes en el sector para visitantes anónimos del sitio web con un ID [!DNL Merkury]. Las marcas pueden aprovechar la potencia de la etiqueta [!DNL Merkury] y Adobe para ofrecer experiencias de sitio web personalizadas en tiempo real. Además, la etiqueta [!DNL Merkury] permite el crecimiento de datos digitales de origen junto con perfiles de clientes conectados en línea y sin conexión. |

{style="table-layout:auto"}

Para obtener más información acerca de la recopilación de datos, lea la [información general de recopilación de datos](../../tags/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Tipo | Descripción |
| ----------- | --------- | ----------- |
| [(Beta): conexión de mejora de datos de Acxiom](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Nuevo | Utilice este conector para activar perfiles de origen de Real-Time CDP a Acxiom para el enriquecimiento de datos y su uso en todos los canales de marketing. A continuación, puede utilizar la fuente Acxiom para importar los perfiles con datos mejorados y trabajar con ellos en Real-Time CDP. |
| [Conexión de supresión de clientes potenciales de Acxiom (Beta)](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Nuevo | Exporte sus públicos de origen al destino de Acxiom para permitir que Acxiom elimine clientes conocidos o convertidos. A continuación, utilice el conector de origen de [importación de datos de clientes potenciales de Acxiom](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) para ingestar y activar listas de clientes potenciales de Acxiom, con sus clientes conocidos o convertidos eliminados. |
| [Conexión de Amazon Ads](../../destinations/catalog/advertising/amazon-ads.md) | Actualización | Al exportar datos al destino de Amazon Ads, ahora puede enrutar los datos al DSP de Amazon o a Amazon Marketing Cloud (nuevo). |
| [Conexión de incorporación a LiveRamp](../../destinations/catalog/advertising/liveramp-onboarding.md) | Actualización | El destino de incorporación de LiveRamp ahora es compatible con envíos a instancias de Europa y Australia [!DNL LiveRamp] [!DNL SFTP]. El tamaño máximo de archivo exportado también se aumentó a 10 millones de filas (de 5 millones, anteriormente). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con tipos de datos de mapa de IU de Experience Platform | Personalice aún más la estructura de datos del Modelo de datos de experiencia (XDM) definiendo campos de asignación en la IU de Experience Platform. Ahora puede crear campos de asignación en el Editor de esquemas para modelar estructuras de datos flexibles o almacenar de forma eficaz pares clave-valor. Seleccione “Asignar” en el menú desplegable Tipo al definir un nuevo campo para configurar subcampos y asignarlos a grupos de campos. Los tipos de valores de asignación admitidos son cadena y entero.<br>![Editor de esquemas con los campos Tipo y Tipo de valor de asignación resaltados.](../2024/assets/march/maps.png "Editor de esquemas con los campos Tipo y Tipo de valor de asignación resaltados."){width="100" zoomable="yes"}<br> Para obtener información sobre cómo [definir campos de asignación en la IU](../../xdm/ui/fields/map.md), consulte la guía de la IU. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Experience Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Nueva funcionalidad**

| Función | Descripción |
| ------- | ----------- |
| Acciones masivas | El inventario de públicos ahora admite acciones masivas. Con las acciones por lotes, puede seleccionar rápidamente varios públicos para moverlos a una carpeta, aplicar etiquetas, aplicar etiquetas de acceso o eliminar. <br> ![Acciones masivas en el espacio de trabajo de la IU de Públicos.](../2024/assets/march/bulk-actions.png "Acciones masivas en el espacio de trabajo de la IU de Públicos."){width="100" zoomable="yes"} <br>Para obtener más información acerca de esta característica, lea la [información general de Audience Portal](../../segmentation/ui/audience-portal.md#bulk-actions). |

{style="table-layout:auto"}

Para obtener más información acerca del Servicio de segmentación, lea la [Información general del Servicio de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Orígenes nuevos y actualizados**

| Función | Tipo | Descripción |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Acxiom Data Ingestion] | Nuevo | Utilice la [[!DNL Acxiom Data Ingestion] fuente](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) para ingerir datos de [!DNL Acxiom] en Real-time Customer Data Platform y enriquecer perfiles de origen. A continuación, puede usar sus perfiles de origen enriquecidos con [!DNL Acxiom] para mejorar los públicos y activarlos en todos los canales de marketing. <br> ![Origen de ingesta de datos de Acxiom.](../2024/assets/march/acxiom-data-ingestion.png "Nuevo origen de ingesta de datos de Acxiom."){width="100" zoomable="yes"} <br> Lea la [[!DNL Acxiom Data Ingestion] información general](../../sources/connectors/data-partners/acxiom-data-ingestion.md) para obtener información sobre cómo empezar. |
| [!BADGE Beta]{type=Informative}[!DNL Stripe] | Nuevo | Use [[!DNL Stripe] fuente](../../sources/connectors/payments/stripe.md) para ingerir en Experience Platform los datos capturados durante el flujo de compra por sus clientes. Una vez ingeridos, puede utilizar estos datos para crear ofertas personalizadas y desbloquear perspectivas comerciales más enriquecidas. <br> ![La fuente de Stripe.](../2024/assets/march/stripe.png "Nuevo origen de Stripe."){width="100" zoomable="yes"} <br> Lea la [[!DNL Stripe] información general](../../sources/connectors/payments/stripe.md) para obtener información sobre cómo empezar. |
| Compatibilidad con la IU para [!DNL Snowflake Streaming] | Nuevo | Ahora puede usar el [[!DNL Snowflake Streaming] origen](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) en la IU de Experience Platform para transmitir datos desde la base de datos de [!DNL Snowflake]. <br> ![La fuente de streaming de Snowflake.](../2024/assets/march/snowflake-streaming.png "Nueva fuente de streaming de Snowflake."){width="100" zoomable="yes"} <br> Lea la [[!DNL Snowflake Streaming] información general](../../sources/connectors/databases/snowflake-streaming.md) para obtener información sobre cómo empezar. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
