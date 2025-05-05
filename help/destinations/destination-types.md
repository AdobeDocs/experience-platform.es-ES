---
keywords: destinos;destino;tipos de destino
title: Tipos y categorías de destino
description: Obtenga información sobre los distintos tipos y categorías de destinos en Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# Tipos y categorías de destino

Lea esta página para comprender los diferentes tipos y categorías de destinos de Adobe Experience Platform.

## Tipos de destino {#destination-types}

En Adobe Experience Platform, distinguimos entre diferentes tipos de destino: conexiones, exportaciones de conjuntos de datos y extensiones. Existen varios tipos de destinos de conexión, que le permiten exportar datos a destinos basados en API, destinos sociales, plataformas CRM y muchos más.

Por último, las conexiones también se pueden distinguir entre destinos públicos disponibles en todas las organizaciones del catálogo de destinos y destinos privados que los clientes de Real-Time CDP Ultimate pueden crear para satisfacer sus casos de uso de exportación específicos.

>[!BEGINSHADEBOX]

![Diagrama de tipos de destinos.](./assets/destination-types/types-of-destinations-no-highlight.png "Diagrama de tipos de destinos."){zoomable="yes"}

>[!ENDSHADEBOX]

## Conexiones {#connections}

**[!UICONTROL Exportación de perfiles]**, **[!UICONTROL Exportación de audiencias de streaming]** y **[!DNL Edge Personalization]** destinos en los datos del evento de captura de Adobe Experience Platform, combínelos con otras fuentes de datos para formar el [Perfil del cliente en tiempo real](../profile/home.md), aplique la segmentación y exporte audiencias y perfiles calificados a destinos.

## Destinos de exportación de perfil {#profile-export}

Los destinos de exportación de perfiles reciben datos sin procesar, a menudo con la dirección de correo electrónico como clave principal. Actualmente, Experience Platform admite dos tipos de destinos de exportación de perfiles:

* [Destinos por lotes (basados en archivos)](#file-based)
* [Destinos empresariales avanzados (destinos de exportación de perfiles de flujo continuo)](#advanced-enterprise-destinations)

### Destinos empresariales avanzados (destinos de exportación de perfiles de flujo continuo) {#advanced-enterprise-destinations}

>[!IMPORTANT]
>
>Los destinos empresariales avanzados o los destinos de exportación de perfiles de flujo continuo solo están disponibles para los clientes de [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html?lang=es).

Utilice los conectores de datos de destino empresariales avanzados para ofrecer perfiles de Adobe Real-Time Customer Data Platform en tiempo casi real a sistemas internos o a otros sistemas de terceros para la sincronización de datos, el análisis y más casos de uso de enriquecimiento de perfiles.

Estos destinos reciben datos de audiencia y perfil como flujos de datos de Experience Platform.

Los destinos empresariales avanzados incluyen:

* [Destino de API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Destinos por lotes (basados en archivos) {#file-based}

Los destinos basados en archivos reciben `.csv` archivos que contienen perfiles o atributos. [Amazon S3](catalog/cloud-storage/amazon-s3.md) es un ejemplo de destino donde puede exportar archivos que contengan exportaciones de perfiles.

## Destinos de exportación de audiencia de streaming {#streaming-destinations}

Los destinos de exportación de audiencia reciben datos de audiencia de Experience Platform. Estos destinos utilizan ID de audiencia o ID de usuario. Advertising y destinos sociales como [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) o [Facebook](catalog/social/facebook.md) son ejemplos de estos destinos.

## Destinos de personalización de Edge {#edge-personalization-destinations}

Los destinos de personalización de Edge en Experience Platform incluyen [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) y [Personalization destination](/help/destinations/catalog/personalization/custom-personalization.md). Al utilizar estos destinos, puede habilitar casos de uso de personalización de la misma página y de la siguiente página para sus clientes.

Obtenga más información sobre cómo [configurar destinos de personalización para la personalización de la misma página y de la página siguiente](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Exportación de perfiles y destinos de exportación de audiencias: vídeo introductorio {#video}

El siguiente vídeo le muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/32690?quality=12&captions=spa)

## Tipos de audiencias exportadas {#exported-audiences-types}

Puede exportar tres tipos de audiencias desde Experience Platform a varios destinos:

* Audiencias de personas
* Públicos de la cuenta
* Públicos de clientes potenciales

Más información sobre los [distintos tipos de audiencia](/help/segmentation/types/account-audiences.md#terminology).

Un símbolo en la tarjeta de destino muestra qué tipos de audiencias puede exportar a cada destino.

![Tarjeta de destino de ejemplo con símbolos que muestran los tipos de audiencia que se pueden exportar.](/help/destinations/assets/destination-types/types-of-audiences.png "Tarjeta de destino de ejemplo con símbolos que muestran los tipos de audiencia que se pueden exportar."){zoomable="yes"}


## Destinos de exportación de conjuntos de datos {#dataset-export-destinations}

Algunos destinos de almacenamiento en la nube del catálogo de destinos admiten exportaciones de conjuntos de datos. Utilice estos destinos para exportar conjuntos de datos sin procesar a ubicaciones de almacenamiento en la nube.

Obtenga más información sobre cómo [exportar conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Extensiones {#extensions}

Experience Platform aprovecha la potencia y flexibilidad de la administración de etiquetas, lo que le permite configurar las extensiones de etiquetas en la interfaz de usuario.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de etiquetas, incluidos los casos de uso y cómo encontrarlas en la interfaz, consulte [descripción general de las extensiones de etiquetas](./catalog/launch-extensions/overview.md).

Las extensiones de etiquetas reenvían datos de evento sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino **Reenvío de eventos**. Se trata de un tipo de integración más sencillo con las plataformas de destino, que solo reenvía datos de evento sin procesar. Algunos ejemplos son la [extensión de personalización Gainsight](./catalog/personalization/gainsight.md) o la [extensión de confirmación de voz del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Extensiones de etiquetas comparadas con otros destinos](./assets/common/launch-and-other-destinations.png)

## Cuándo utilizar conexiones y extensiones {#when-to-use}

Como experto en marketing, puede utilizar una combinación de conexiones y extensiones para tratar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o una audiencia de cliente para la activación. Por ejemplo, utilice conexiones si va a unir datos de comportamiento de un sistema de análisis con datos CRM cargados para clasificar a un usuario para una audiencia determinada antes de enviarle un mensaje personalizado.

Las extensiones son útiles cuando los datos de evento se utilizan para almacenar en déclencheur una acción o para llevar a cabo la segmentación en un entorno externo. Por ejemplo, si es necesario reenviar los datos de comportamiento a un sistema externo sin estar unidos a otras fuentes de datos archivadas para un usuario determinado.

## Categorías de destino {#categories}

Las conexiones y extensiones del [catálogo de destinos](https://platform.adobe.com/destination/catalog) se agrupan por categoría de destino (**Advertising**, **almacenamiento en la nube**, **plataformas de encuestas**, **marketing por correo electrónico**, etc.), según la acción de marketing que le ayuden a lograr. Para obtener más información sobre cada una de las categorías, así como los destinos incluidos en cada categoría, consulte la [documentación del catálogo de destinos](./catalog/overview.md).

![Categorías de destino resaltadas en la página del catálogo.](./assets/destination-types/destination-categories-menu.png "Categorías de destino resaltadas en la página del catálogo."){zoomable="yes"}
