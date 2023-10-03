---
keywords: destinos;destino;tipos de destino
title: Tipos y categorías de destino
description: Obtenga información sobre los distintos tipos y categorías de destinos en Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# Tipos y categorías de destino

Lea esta página para comprender los diferentes tipos y categorías de destinos de Adobe Experience Platform.

## Tipos de destino {#destination-types}

En Adobe Experience Platform, distinguimos entre diferentes tipos de destino: conexiones, exportaciones de conjuntos de datos y extensiones. Existen varios tipos de destinos de conexión, que le permiten exportar datos a destinos basados en API, .

Por último, las conexiones también se pueden distinguir entre destinos públicos disponibles en todas las organizaciones del catálogo de destinos y destinos privados que los clientes de Real-Time CDP Ultimate pueden crear para satisfacer sus casos de uso de exportación específicos.

![Diagrama de tipos de destinos.](./assets/destination-types/types-of-destinations-no-highlight.png)

## Conexiones {#connections}

**[!UICONTROL Exportación de perfiles]**, **[!UICONTROL Exportación de audiencia de streaming]**, y **[!DNL Edge Personalization]** destinos en Adobe Experience Platform capture datos de evento, combínelos con otras fuentes de datos para formar el [Perfil del cliente en tiempo real](../profile/home.md), aplique la segmentación y exporte audiencias y perfiles cualificados a destinos.

## Destinos de exportación de perfil {#profile-export}

Los destinos de exportación de perfiles reciben datos sin procesar, a menudo con la dirección de correo electrónico como clave principal. Actualmente, Experience Platform admite dos tipos de destinos de exportación de perfiles:

* [Destinos de exportación de perfiles de streaming (destinos empresariales)](#streaming-profile-export)
* [Destinos por lotes (basados en archivos)](#file-based)

### Destinos de exportación de perfiles de streaming (destinos empresariales) {#streaming-profile-export}

>[!IMPORTANT]
>
>Los destinos empresariales o los destinos de exportación de perfil de flujo continuo están disponibles para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) solo para clientes de.

Utilice los conectores de datos de destino empresariales para ofrecer perfiles de Adobe Real-time Customer Data Platform en tiempo casi real a sistemas internos o a otros sistemas de terceros para la sincronización de datos, el análisis y más casos de uso de enriquecimiento de perfiles.

Estos destinos reciben datos de audiencia y perfil como flujos de datos de Experience Platform.

Los destinos empresariales incluyen:

* [Destino de API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Destinos por lotes (basados en archivos) {#file-based}

Los destinos basados en archivos reciben `.csv` archivos que contienen perfiles o atributos. [Amazon S3](catalog/cloud-storage/amazon-s3.md) es un ejemplo de destino en el que se pueden exportar archivos que contengan exportaciones de perfil.

## Destinos de exportación de audiencia de streaming {#streaming-destinations}

Los destinos de exportación de audiencia reciben datos de audiencia de Experience Platform. Estos destinos utilizan ID de audiencia o ID de usuario. Destinos publicitarios y sociales como [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), o [Facebook](catalog/social/facebook.md) Estos son ejemplos de destinos de este tipo.

## Destinos de personalización de Edge {#edge-personalization-destinations}

Los destinos de personalización de Edge en Experience Platform incluyen [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) y el [Destino de personalización personalizado](/help/destinations/catalog/personalization/custom-personalization.md). Al utilizar estos destinos, puede habilitar casos de uso de personalización de la misma página y de la siguiente página para sus clientes.

Obtenga más información sobre cómo [configuración de destinos de personalización para la personalización de la misma página y de la página siguiente](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Exportación de perfiles y destinos de exportación de audiencias: vídeo introductorio {#video}

El siguiente vídeo le muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Destinos de exportación de conjuntos de datos {#dataset-export-destinations}

Algunos destinos de almacenamiento en la nube del catálogo de destinos admiten exportaciones de conjuntos de datos. Utilice estos destinos para exportar conjuntos de datos sin procesar a ubicaciones de almacenamiento en la nube.

Obtenga más información sobre cómo [exportar conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Extensiones {#extensions}

Platform aprovecha la potencia y flexibilidad de la administración de etiquetas, lo que le permite configurar las extensiones de etiquetas en la interfaz de usuario.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de etiquetas, incluidos los casos de uso y cómo encontrarlas en la interfaz, consulte la [información general sobre extensiones de etiquetas](./catalog/launch-extensions/overview.md).

Las extensiones de etiquetas reenvían datos de evento sin procesar a varios tipos de destinos. Considere las extensiones como una **Reenvío de eventos** tipo de destino. Se trata de un tipo de integración más sencillo con las plataformas de destino, que solo reenvía datos de evento sin procesar. Algunos ejemplos son los siguientes [Extensión de personalización Gainsight](./catalog/personalization/gainsight.md) o el [Confirmar la extensión de Voz del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Extensiones de etiquetas comparadas con otros destinos](./assets/common/launch-and-other-destinations.png)

## Cuándo utilizar conexiones y extensiones {#when-to-use}

Como experto en marketing, puede utilizar una combinación de conexiones y extensiones para tratar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o una audiencia de cliente para la activación. Por ejemplo, utilice conexiones si va a unir datos de comportamiento de un sistema de análisis con datos CRM cargados para clasificar a un usuario para una audiencia determinada antes de enviarle un mensaje personalizado.

Las extensiones son útiles cuando los datos de evento se utilizan para almacenar en déclencheur una acción o para llevar a cabo la segmentación en un entorno externo. Por ejemplo, si es necesario reenviar los datos de comportamiento a un sistema externo sin estar unidos a otras fuentes de datos archivadas para un usuario determinado.

## Categorías de destino {#categories}

Las conexiones y extensiones de la [catálogo de destinos](https://platform.adobe.com/destination/catalog) se agrupan por categoría de destino (**Publicidad**, **Almacenamiento en la nube**, **Plataformas de encuesta**, **Marketing por email**, etc.), según la acción de marketing que le ayuden a lograr. Para obtener más información sobre cada una de las categorías, así como los destinos incluidos en cada categoría, consulte la [Documentación del catálogo de destinos](./catalog/overview.md).

![Categorías de destino resaltadas en la página del catálogo.](./assets/destination-types/destination-categories-menu.png)
