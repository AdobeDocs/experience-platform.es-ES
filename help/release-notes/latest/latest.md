---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de marzo de 2023 para Adobe Experience Platform.
source-git-commit: c5061a759f1098ce1dcc7e3f00c52e064239d7c5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 29 de marzo de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Preparación de datos](#data-prep)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo flujo de trabajo de inicio rápido para la API de Meta Conversions (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. La variable [flujo de trabajo de inicio rápido para la API de Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite a los clientes recopilar y reenviar rápidamente datos de eventos, del lado del servidor a Meta para conversiones de anuncios en solo unos pasos sencillos. |
| [!DNL Braze] extensión de reenvío de eventos | La variable [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) la extensión de reenvío de eventos permite aprovechar los datos capturados en la red perimetral de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor utilizando la variable [!DNL Braze] API de seguimiento de usuarios. |
| [!DNL Mixpanel] extensión de reenvío de eventos | La variable [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) permite a los clientes aprovechar el reenvío de eventos para capturar información de eventos en la red perimetral de Adobe Experience Platform y enviarla a Mixpanel mediante la API de seguimiento de eventos. |

{style="table-layout:auto"}

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas funciones para codificar y descodificar cadenas URL | <ul><li>La variable `get_url_encoded` toma una URL como entrada y reemplaza o codifica caracteres especiales con caracteres ASCII.</li><li>La variable `get_url_decoded` toma una URL como entrada y descodifica los caracteres ASCII en caracteres especiales.</li></ul> Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). Para obtener una lista completa de los caracteres reservados y sus correspondientes caracteres codificados, lea la guía de [caracteres especiales](../../data-prep/functions.md#special-characters). |

Para obtener más información sobre la preparación de datos, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

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
