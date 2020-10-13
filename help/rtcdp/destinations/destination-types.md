---
keywords: destinations;destination;destination types
title: Tipos y Categorías de destinos
seo-title: Tipos y Categorías de destinos
description: 'En la plataforma de datos del cliente en tiempo real de Adobe, los destinos de exportación de Perfiles/segmentos capturan datos de evento, los combinan con otras fuentes de datos, aplican segmentación y exportan segmentos y perfiles cualificados a los destinos. Las extensiones de inicio reenvían datos de evento sin procesar a varios tipos de destinos. '
seo-description: En la plataforma de datos del cliente en tiempo real de Adobe, los destinos de exportación de Perfiles/segmentos capturan datos de evento, los combinan con otras fuentes de datos, aplican segmentación y exportan segmentos y perfiles cualificados a los destinos. Las extensiones de inicio reenvían datos de evento sin procesar a varios tipos de destinos.
translation-type: tm+mt
source-git-commit: b510f715133cc3fed98861f977b3ce9a857a5ced
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Tipos y Categorías de destino

Lea esta página para conocer los distintos tipos y categorías de destinos de la Plataforma de datos de clientes en tiempo real de Adobe.

## Tipos de destino

En la plataforma de datos del cliente en tiempo real de Adobe, distinguimos dos tipos de destino: conexiones y extensiones. Existen dos tipos de destinos de conexión: destinos de exportación de Perfil y destinos de exportación de segmentos.

![Tipos de destinos](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Conexiones {#connections}

**[!UICONTROL Los destinos de exportación]** y **[!UICONTROL segmento de perfil Exportar]** en Adobe Plataforma de datos del cliente en tiempo real capturan datos de evento, los combinan con otras fuentes de datos para formar el perfil [del cliente en tiempo](/help/profile/home.md)real, aplicar segmentación y exportar segmentos y perfiles cualificados a los destinos.

<br> 

#### Destinos de exportación de perfil

Los destinos de exportación de perfil generan un archivo que contiene perfiles y/o atributos. Estos destinos utilizan datos sin procesar, a menudo con la dirección de correo electrónico como clave principal. El destino [de almacenamiento en la nube](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 es un ejemplo de destino en el que puede depositar archivos que contengan exportaciones de perfil.

#### Destinos de exportación de segmentos

Los destinos de exportación de segmentos envían los perfiles y los segmentos para los que cumplen los requisitos a las plataformas de destino. Estos destinos utilizan ID de segmento o ID de usuario. Los destinos de publicidad como [[!DNL Google Display & Video 360]](/help/rtcdp/destinations/google-dv360-destination.md) o [[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) son ejemplos de estos tipos de destinos.

#### Destinos de exportación de perfiles y segmentos: descripción general de vídeo

El siguiente vídeo le muestra las particularidades de los dos tipos de destinos:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensiones {#extensions}

CDP en tiempo real de Adobe aprovecha la potencia y flexibilidad del Experience Platform Launch para incluir extensiones de Launch en la interfaz CDP en tiempo real de Adobe.

>[!TIP]
>
>Para obtener información detallada sobre las extensiones de Experience Platform Launch, incluidos los casos de uso y cómo encontrarlos en la interfaz, consulte la descripción general [de extensiones de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Launch.

Las extensiones de inicio reenvían datos de evento sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino de reenvío de **Evento** . Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de evento sin procesar. Algunos ejemplos son la extensión [de personalización de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight o [Confirmar voz de la extensión](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Cliente.

![Extensiones de Experience Platform Launch en comparación con otros destinos](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Cuándo utilizar conexiones y extensiones

Como especialista en mercadotecnia, puede utilizar una combinación de conexiones y extensiones para abordar sus casos de uso.

Las conexiones son útiles cuando es necesario aprovechar un perfil de cliente centralizado completo o un segmento de cliente para la activación. Por ejemplo, utilice conexiones si está uniendo datos de comportamiento de un sistema de análisis con datos CRM cargados para calificar a un usuario para un segmento determinado antes de enviar un mensaje personalizado a ese usuario.

Las extensiones son útiles cuando se utilizan datos de evento para desencadenar una acción o para realizar la segmentación en un entorno externo. Por ejemplo, si los datos de comportamiento deben reenviarse a un sistema externo sin estar unidos a otras fuentes de datos de un archivo para un usuario determinado.

<br> 

## Categorías de destino

Las conexiones y extensiones del catálogo [de](https://platform.adobe.com/destination/catalog) destinos se agrupan por categoría de destino (**Publicidad**, almacenamiento **de** Cloud, plataformas **de** Encuesta, marketing **** por correo electrónico, etc.), según el caso de uso de marketing que le ayuden a conseguir. Para obtener más información sobre cada una de las categorías, así como sobre los destinos incluidos en cada categoría, consulte la documentación [del catálogo de](/help/rtcdp/destinations/destinations-catalog.md)Destinations.

![Categorías de destino](/help/rtcdp/destinations/assets/destination-categories-menu.png)

