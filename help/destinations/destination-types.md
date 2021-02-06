---
keywords: destinos;destino;tipos de destino
title: Tipos y Categorías de destinos
seo-title: Tipos y Categorías de destinos
description: Obtenga información sobre los distintos tipos y categorías de destinos en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Tipos y categorías de destino

Lea esta página para conocer los distintos tipos y categorías de destinos de Adobe Experience Platform.

## Tipos de destino

En Adobe Experience Platform, distinguimos dos tipos de destino: conexiones y extensiones. Existen dos tipos de destinos de conexión: destinos de exportación de Perfil y destinos de exportación de segmentos.

![Tipos de destinos](./assets/destination-types/types-of-destinations.png)

### Conexiones {#connections}

**[!UICONTROL Los destinos]** de exportación y  **[!UICONTROL segmento de perfil]** Exportaciones en Adobe Experience Platform capturan datos de evento, los combinan con otras fuentes de datos para formar el Perfil [ del cliente en tiempo ](../profile/home.md)real, aplicar segmentación y exportar segmentos y perfiles cualificados a destinos.

#### Destinos de exportación de perfil

Los destinos de exportación de perfil generan un archivo que contiene perfiles y/o atributos. Estos destinos utilizan datos sin procesar, a menudo con la dirección de correo electrónico como clave principal. El [destino del almacenamiento en la nube Amazon S3](./catalog/cloud-storage/amazon-s3.md) es un ejemplo de destino en el que puede depositar archivos que contengan exportaciones de perfil.

#### Destinos de exportación de segmentos

Los destinos de exportación de segmentos envían los perfiles y los segmentos para los que cumplen los requisitos a las plataformas de destino. Estos destinos utilizan ID de segmento o ID de usuario. Los destinos de publicidad como [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) o [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) son ejemplos de estos tipos de destinos.

#### Destinos de exportación de perfiles y segmentos: descripción general de vídeo

El siguiente vídeo le muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Extensiones {#extensions}

La plataforma aprovecha la potencia y flexibilidad de Adobe Experience Platform Launch para incluir extensiones de Launch en la interfaz de la plataforma.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de Adobe Experience Platform Launch, incluidos los casos de uso y cómo encontrarlos en la interfaz, consulte la [información general sobre extensiones de Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md).

Las extensiones de Launch de plataforma reenvían datos de evento sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino de **reenvío de Evento**. Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de evento sin procesar. Algunos ejemplos son la [extensión de personalización de Gainsight](./catalog/personalization/gainsight.md) o la [voz de confirmación de la extensión del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Extensiones de Experience Platform Launch en comparación con otros destinos](./assets/common/launch-and-other-destinations.png)

### Cuándo utilizar conexiones y extensiones

Como especialista en mercadotecnia, puede utilizar una combinación de conexiones y extensiones para abordar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o un segmento de cliente para la activación. Por ejemplo, utilice conexiones si está uniendo datos de comportamiento de un sistema de análisis con datos CRM cargados para calificar a un usuario para un segmento determinado antes de enviar un mensaje personalizado a ese usuario.

Las extensiones son útiles cuando los datos de evento se utilizan para realizar déclencheur de una acción o para realizar la segmentación en un entorno externo. Por ejemplo, si los datos de comportamiento deben reenviarse a un sistema externo sin estar unidos a otras fuentes de datos de un archivo para un usuario determinado.

## Categorías de destino

Las conexiones y extensiones del [catálogo de destinos](https://platform.adobe.com/destination/catalog) se agrupan por categoría de destino (**Publicidad**, **almacenamiento de nube**, **plataformas de Encuesta**, **Marketing por correo electrónico**, etc.), según el caso de uso de mercadotecnia que le ayuden a lograr. Para obtener más información sobre cada una de las categorías, así como sobre los destinos incluidos en cada categoría, consulte la [documentación del catálogo de destinos](./catalog/overview.md).

![Categorías de destino](./assets/destination-types/destination-categories-menu.png)

