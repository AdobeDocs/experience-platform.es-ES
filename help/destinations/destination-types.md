---
keywords: destinos;destino;tipos de destino
title: Tipos y categorías de destino
seo-title: Tipos y categorías de destino
description: Obtenga información sobre los distintos tipos y categorías de destinos en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Tipos y categorías de destino

Lea esta página para comprender los distintos tipos y categorías de destinos de Adobe Experience Platform.

## Tipos de destino

En Adobe Experience Platform, distinguimos entre dos tipos de destino: conexiones y extensiones. Existen dos tipos de destinos de conexión: destinos de exportación de perfil y destinos de exportación de segmento.

![Tipos de destinos](./assets/destination-types/types-of-destinations.png)

## Conexiones {#connections}

**[!UICONTROL Profile Export]** y los  **[!UICONTROL Segment Export]** destinos de Adobe Experience Platform capturan datos de eventos, los combinan con otras fuentes de datos para formar el Perfil del cliente en tiempo  [real](../profile/home.md), aplican segmentación y exportan segmentos y perfiles cualificados a los destinos.

## Destinos de exportación de perfil

Los destinos de exportación de perfil generan un archivo que contiene perfiles o atributos. Estos destinos utilizan datos sin procesar, a menudo con la dirección de correo electrónico como clave principal. El [destino de almacenamiento en la nube de Amazon S3](./catalog/cloud-storage/amazon-s3.md) es un ejemplo de destino en el que puede depositar archivos que contengan exportaciones de perfiles.

## Destinos de exportación de segmentos

Los destinos de exportación de segmentos envían los perfiles y los segmentos para los que cumplen los requisitos a las plataformas de destino. Estos destinos utilizan ID de segmento o ID de usuario. Los destinos publicitarios como [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) o [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) son ejemplos de este tipo de destinos.

## Exportación de perfiles y destinos de exportación de segmentos: información general sobre el vídeo

El siguiente vídeo muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensiones {#extensions}

Platform aprovecha la potencia y flexibilidad de Adobe Experience Platform Launch para incluir extensiones de Platform launch en la interfaz de Platform.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de Adobe Experience Platform Launch, incluidos los casos de uso y cómo encontrarlos en la interfaz, consulte la [información general sobre las extensiones de Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md).

Las extensiones de platform launch reenvían datos de eventos sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino **Event Forwarding**. Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de eventos sin procesar. Algunos ejemplos son la [Gainsight personalization extension](./catalog/personalization/gainsight.md) o la [Confirmit Voice of the Customer extension](./catalog/voice/confirmit-digital-feedback.md).

![Extensiones de Experience Platform Launch en comparación con otros destinos](./assets/common/launch-and-other-destinations.png)

## Cuándo utilizar conexiones y extensiones

Como especialista en marketing, puede utilizar una combinación de conexiones y extensiones para solucionar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o un segmento de cliente para la activación. Por ejemplo, utilice conexiones si está uniendo datos de comportamiento de un sistema de análisis con datos CRM cargados para calificar a un usuario para un segmento determinado antes de enviar un mensaje personalizado a ese usuario.

Las extensiones son útiles cuando los datos de evento se utilizan para almacenar en déclencheur una acción o para realizar la segmentación en un entorno externo. Por ejemplo, si los datos de comportamiento deben reenviarse a un sistema externo sin unirse a otras fuentes de datos en el archivo para un usuario determinado.

## Categorías de destino

Las conexiones y extensiones del [catálogo de destinos](https://platform.adobe.com/destination/catalog) se agrupan por categoría de destino (**Advertising**, **Cloud storage**, **Survey platform**, **Email marketing**, etc.), según la acción de marketing que le ayuden a realizar. Para obtener más información sobre cada una de las categorías, así como los destinos incluidos en cada categoría, consulte la [Documentación del catálogo de destinos](./catalog/overview.md).

![Categorías de destino](./assets/destination-types/destination-categories-menu.png)

