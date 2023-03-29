---
title: Notas de la versión de Adobe Experience Platform, marzo de 2023
description: Notas de la versión de marzo de 2023 para Adobe Experience Platform.
source-git-commit: 74b609572b6e5e9b5e641fe497f53f3463b900c4
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 3%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 29 de marzo de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Preparación de datos](#data-prep)
- [Destinos](#destinations)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo flujo de trabajo de inicio rápido para la API de Meta Conversions (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. La variable [flujo de trabajo de inicio rápido para la API de Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite a los clientes recopilar y reenviar rápidamente datos de eventos, del lado del servidor a Meta para conversiones de anuncios en solo unos pasos sencillos. |
| Nuevo flujo de trabajo de inicio rápido para el SDK de Mobile (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. La variable [flujo de trabajo de inicio rápido para el SDK de Mobile](https://developer.adobe.com/client-sdks/documentation/) le permite implementar rápidamente el SDK móvil y validar eventos móviles básicos en solo unos pasos sencillos. |
| [!DNL Braze] extensión de reenvío de eventos | La variable [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) la extensión de reenvío de eventos permite aprovechar los datos capturados en la red perimetral de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor utilizando la variable [!DNL Braze] API de seguimiento de usuarios. |
| [!DNL Mixpanel] extensión de reenvío de eventos | La variable [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) permite a los clientes aprovechar el reenvío de eventos para capturar información de eventos en la red perimetral de Adobe Experience Platform y enviarla a Mixpanel mediante la API de seguimiento de eventos. |

{style="table-layout:auto"}

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general del filtrado para los datos de Adobe Analytics | Ahora puede utilizar las funcionalidades de preparación de datos para aplicar reglas y condiciones para filtrar los datos de Analytics antes de ingerirlos en el perfil del cliente en tiempo real. Para obtener más información, consulte la guía de [filtrado de datos de Analytics para la ingesta de perfiles](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuevas funciones para codificar y descodificar cadenas URL | <ul><li>La variable `get_url_encoded` toma una URL como entrada y reemplaza o codifica caracteres especiales con caracteres ASCII.</li><li>La variable `get_url_decoded` toma una URL como entrada y descodifica los caracteres ASCII en caracteres especiales.</li></ul> Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). Para obtener una lista completa de los caracteres reservados y sus correspondientes caracteres codificados, lea la guía de [caracteres especiales](../../data-prep/functions.md#special-characters). |

Para obtener más información sobre la preparación de datos, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] conexión GA](../../destinations/catalog/personalization/adobe-commerce.md) | La variable [!DNL Adobe Commerce] el conector de destino (ahora disponible de forma general) le permite seleccionar una o varias audiencias de Real-Time CDP para activarlas en su [!DNL Adobe Commerce] para ofrecer una experiencia personalizada dinámica para sus compradores. |
| [[!DNL Snap Inc] conexión GA](../../destinations/catalog/advertising/snap-inc.md) | La variable [!DNL Snap Inc] conector de destino (ahora disponible de forma general) permite a los especialistas en marketing importar segmentos de usuario creados en Experience Platform a [!DNL Snapchat Ads] y úselo para dirigir sus anuncios. |
| [Conexión (API) Eloqua de Oracle](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilice la conexión basada en API para [!DNL Oracle Eloqua] para planificar y ejecutar campañas al tiempo que ofrece una experiencia de cliente personalizada para sus clientes potenciales en [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] connection](../../destinations/catalog/advertising/amazon-ads.md) | La variable [!DNL Amazon Ads] la integración con Adobe Experience Platform proporciona integración llave en mano a [!DNL Amazon Ads] los productos, incluido el [!DNL Amazon DSP (ADSP)]. Al usar la variable [!DNL Amazon Ads] destino en Adobe Experience Platform, los usuarios pueden definir audiencias de anunciante para el direccionamiento y la activación en el [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] connection](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) proporciona a los especialistas en marketing una perspectiva de cuáles son los esfuerzos de marketing más efectivos para generar ingresos y maximizar el retorno de la inversión para su empresa. El destino permite los flujos de datos de empresa a empresa (B2B) de Adobe Experience Platform a [!DNL Marketo Measure]. La tarjeta solo está disponible para [!DNL Marketo Measure Ultimate] clientes. |
| [Conexión TikTok](../../destinations/catalog/social/tiktok.md) | Cree audiencias personalizadas en TikTok con sus datos para segmentar con sus campañas de publicidad. |
| [Conexión de Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilice este destino para crear y actualizar identidades dentro de un segmento como contactos dentro de [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Nuevo permiso de control de acceso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | El nuevo permiso permite a los usuarios activar segmentos en destinos existentes, sin mostrar la variable [paso de asignación](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden agregar y eliminar segmentos en flujos de trabajo de activación, pero no pueden agregar ni eliminar atributos o identidades asignados. |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

Estamos publicando una corrección de errores para el cifrado PGP/GPG en destinos basados en archivos para CDP en tiempo real. Con este cambio, los destinos basados en archivos existentes que actualmente utilizan cifrado generarán un nombre de archivo con una extensión diferente a la anterior.

- Extensión actual al utilizar cifrado: `filename.csv`
- Extensión futura al utilizar el cifrado: `filename.csv.gpg`

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Métricas de perfil | Para proporcionar una representación más precisa de las métricas de perfil, el desglose de miembros y las métricas de pérdida se están combinando y ahora se calculan en un período de 24 horas. Encontrará más información en la [Guía de la interfaz de usuario de segmentación](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad beta de [!DNL Chatlio] | La variable [!DNL Chatlio] el origen ya está disponible en versión beta. Utilice la variable [!DNL Chatlio] fuente para transmitir su [!DNL Chatlio] datos de eventos a Experience Platform. Para obtener más información, lea la [[!DNL Chatlio] información general](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidad beta de [!DNL Customer.io] | La variable [!DNL Customer.io] el origen ya está disponible en versión beta. Utilice la variable [!DNL Customer.io] fuente para transmitir los datos de eventos del cliente al Experience Platform. Para obtener más información, lea la [[!DNL Customer.io] información general](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidad beta de [!DNL Pendo] | La variable [!DNL Pendo] el origen ya está disponible en versión beta. Utilice la variable [!DNL Pendo] para transmitir los datos de análisis de productos al Experience Platform. Para obtener más información, lea la [[!DNL Pendo] información general](../../sources/connectors/analytics/pendo-webhook.md). |
| Compatibilidad con flujos de datos de borrador | Ahora puede utilizar la API de servicio de flujo para establecer los flujos de datos en un estado de borrador. Los flujos de datos borrados se pueden actualizar y publicar posteriormente con nueva información. Para obtener más información, consulte la guía de [definición de los flujos de datos de origen como borradores](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
