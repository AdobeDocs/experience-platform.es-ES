---
keywords: destinos;destino;tipos de destino
title: Tipos y categorías de destino
seo-title: Tipos y categorías de destino
description: Obtenga información sobre los distintos tipos y categorías de destinos en Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 5a6f14ba65584a6bd61d62c4fb0b46e8f9e8e96d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Tipos y categorías de destino

Lea esta página para comprender los distintos tipos y categorías de destinos de Adobe Experience Platform.

## Tipos de destino

En Adobe Experience Platform, distinguimos entre dos tipos de destino: conexiones y extensiones. Existen dos tipos de destinos de conexión: destinos de exportación de perfil y destinos de exportación de segmento.

![Tipos de destinos](./assets/destination-types/types-of-destinations.png)

## Conexiones {#connections}

**[!UICONTROL Exportación de]** perfiles y  **[!UICONTROL exportación de segmentos de]** flujo continuo en Adobe Experience Platform capturan datos de evento, los combinan con otras fuentes de datos para formar el Perfil del cliente en tiempo  [real](../profile/home.md), aplican segmentación y exportan segmentos y perfiles cualificados a los destinos.

## Destinos de exportación de perfil

Los destinos de exportación de perfil reciben datos sin procesar, a menudo con direcciones de correo electrónico como clave principal. Actualmente, el Experience Platform admite dos tipos de destinos de exportación de perfil:

* [Destinos de exportación de perfiles de transmisión](#streaming-profile-export)
* [Destinos basados en archivos](#file-based)

### Destinos de exportación de perfiles de transmisión {#streaming-profile-export}

Los destinos de exportación de perfiles de flujo continuo reciben datos de segmentos y perfiles como flujos de datos de Experience Platform. [Amazon ](catalog/cloud-storage/amazon-kinesis.md) Kinesiy  [Azure Event ](catalog/cloud-storage/azure-event-hubs.md) Hubsare son ejemplos de estos destinos.

### Destinos basados en archivos {#file-based}

Los destinos basados en archivos reciben `.csv` archivos que contienen perfiles o atributos. [Amazon S3](catalog/cloud-storage/amazon-s3.md) es un ejemplo de destino en el que se pueden depositar archivos que contengan exportaciones de perfiles.

## Destinos de exportación de segmentos de transmisión

Los destinos de exportación de segmentos reciben datos de segmentos del Experience Platform. Estos destinos utilizan ID de segmento o ID de usuario. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md) y  [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) son ejemplos de estos destinos.

## Exportación de perfiles y destinos de exportación de segmentos: información general sobre vídeo

El siguiente vídeo muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensiones {#extensions}

Platform aprovecha la potencia y flexibilidad de la administración de etiquetas, lo que le permite configurar extensiones de etiquetas en la interfaz de usuario de recopilación de datos.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de etiquetas, incluidos los casos de uso y cómo encontrarlos en la interfaz, consulte la [información general sobre las extensiones de etiquetas](./catalog/launch-extensions/overview.md).

Las extensiones de etiqueta reenvían datos de eventos sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino **Event Forwarding**. Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de eventos sin procesar. Algunos ejemplos son la [Gainsight personalization extension](./catalog/personalization/gainsight.md) o la [Confirmit Voice of the Customer extension](./catalog/voice/confirmit-digital-feedback.md).

![Etiquetar extensiones en comparación con otros destinos](./assets/common/launch-and-other-destinations.png)

## Cuándo utilizar conexiones y extensiones

Como especialista en marketing, puede utilizar una combinación de conexiones y extensiones para solucionar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o un segmento de cliente para la activación. Por ejemplo, utilice conexiones si está uniendo datos de comportamiento de un sistema de análisis con datos CRM cargados para calificar a un usuario para un segmento determinado antes de enviar un mensaje personalizado a ese usuario.

Las extensiones son útiles cuando los datos de evento se utilizan para almacenar en déclencheur una acción o para realizar la segmentación en un entorno externo. Por ejemplo, si los datos de comportamiento deben reenviarse a un sistema externo sin unirse a otras fuentes de datos en el archivo para un usuario determinado.

## Categorías de destino

Las conexiones y extensiones del [catálogo de destinos](https://platform.adobe.com/destination/catalog) se agrupan por categoría de destino (**Advertising**, **Cloud storage**, **Survey platform**, **Email marketing**, etc.), según la acción de marketing que le ayuden a realizar. Para obtener más información sobre cada una de las categorías, así como los destinos incluidos en cada categoría, consulte la [Documentación del catálogo de destinos](./catalog/overview.md).

![Categorías de destino](./assets/destination-types/destination-categories-menu.png)
