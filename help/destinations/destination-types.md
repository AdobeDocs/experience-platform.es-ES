---
keywords: destinos;destino;tipos de destino
title: Tipos y categorías de destino
seo-title: Destination types and categories
description: Obtenga información sobre los distintos tipos y categorías de destinos en Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 08c6c2716b88180b1eb290663117e6da2d8641f0
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Tipos y categorías de destino

Lea esta página para comprender los distintos tipos y categorías de destinos de Adobe Experience Platform.

## Tipos de destino

En Adobe Experience Platform, distinguimos entre dos tipos de destino: conexiones y extensiones. Existen dos tipos de destinos de conexión: destinos de exportación de perfil y destinos de exportación de segmento.

![Tipos de destinos](./assets/destination-types/types-of-destinations.png)

## Conexiones {#connections}

**[!UICONTROL Exportación de perfiles]** y **[!UICONTROL Exportación de segmentos de transmisión]** los destinos en Adobe Experience Platform capturan datos de evento y los combinan con otras fuentes de datos para formar la variable [Perfil del cliente en tiempo real](../profile/home.md), aplique la segmentación y exporte segmentos y perfiles cualificados a los destinos.

## Destinos de exportación de perfil

Los destinos de exportación de perfil reciben datos sin procesar, a menudo con direcciones de correo electrónico como clave principal. Actualmente, el Experience Platform admite dos tipos de destinos de exportación de perfil:

* [Destinos de exportación de perfiles de transmisión](#streaming-profile-export)
* [Destinos por lotes (basados en archivos)](#file-based)

### Destinos de exportación de perfiles de transmisión {#streaming-profile-export}

Los destinos de exportación de perfiles de flujo continuo reciben datos de segmentos y perfiles como flujos de datos de Experience Platform. [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md) y [Centros de eventos de Azure](catalog/cloud-storage/azure-event-hubs.md) son ejemplos de estos destinos.

### Destinos por lotes (basados en archivos) {#file-based}

Los destinos basados en archivos reciben `.csv` archivos que contienen perfiles o atributos. [Amazon S3](catalog/cloud-storage/amazon-s3.md) es un ejemplo de destino en el que puede exportar archivos que contengan exportaciones de perfiles.

## Destinos de exportación de segmentos de transmisión {#streaming-destinations}

Los destinos de exportación de segmentos reciben datos de segmentos del Experience Platform. Estos destinos utilizan ID de segmento o ID de usuario. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), y son ejemplos de estos destinos.

## Exportación de perfiles y destinos de exportación de segmentos: información general sobre vídeo {#video}

El siguiente vídeo muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensiones {#extensions}

Platform aprovecha la potencia y flexibilidad de la administración de etiquetas, lo que le permite configurar extensiones de etiquetas en la interfaz de usuario de recopilación de datos.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de etiquetas, incluidos los casos de uso y cómo encontrarlos en la interfaz, consulte la [información general sobre las extensiones de etiquetas](./catalog/launch-extensions/overview.md).

Las extensiones de etiqueta reenvían datos de eventos sin procesar a varios tipos de destinos. Considere las extensiones como un **Reenvío de eventos** tipo de destino. Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de eventos sin procesar. Algunos ejemplos de estos son los [Extensión de personalización de Gainsight](./catalog/personalization/gainsight.md) o [Confirmar la extensión de voz del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Etiquetar extensiones en comparación con otros destinos](./assets/common/launch-and-other-destinations.png)

## Cuándo utilizar conexiones y extensiones {#when-to-use}

Como especialista en marketing, puede utilizar una combinación de conexiones y extensiones para solucionar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o un segmento de cliente para la activación. Por ejemplo, utilice conexiones si está uniendo datos de comportamiento de un sistema de análisis con datos CRM cargados para calificar a un usuario para un segmento determinado antes de enviar un mensaje personalizado a ese usuario.

Las extensiones son útiles cuando los datos de evento se utilizan para almacenar en déclencheur una acción o para realizar la segmentación en un entorno externo. Por ejemplo, si los datos de comportamiento deben reenviarse a un sistema externo sin unirse a otras fuentes de datos en el archivo para un usuario determinado.

## Categorías de destino {#categories}

Las conexiones y extensiones en la variable [catálogo de destinos](https://platform.adobe.com/destination/catalog) se agrupan por categoría de destino (**Publicidad**, **Almacenamiento en la nube**, **Plataformas de encuesta**, **Marketing por correo electrónico**, etc.), según la acción de marketing que le ayuden a lograr. Para obtener más información sobre cada una de las categorías, así como los destinos incluidos en cada categoría, consulte la [Documentación del catálogo de destinos](./catalog/overview.md).

![Categorías de destino](./assets/destination-types/destination-categories-menu.png)
