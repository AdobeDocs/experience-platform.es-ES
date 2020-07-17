---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentación multientidad
topic: overview
translation-type: tm+mt
source-git-commit: f44e42a4faa3b10f147dbaf929048054ce0bec42
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Segmentación multientidad

La segmentación de varias entidades es la capacidad de ampliar los datos de Perfil con datos adicionales basados en productos, almacenes u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema de Perfil.

Para obtener más información sobre la segmentación multientidad, siga leyendo la documentación y complementando su aprendizaje, vea el siguiente vídeo o explorando la descripción general [de la](./home.md)segmentación.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que implican el uso de la segmentación. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Perfil](../profile/home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [Servicio](./home.md)de segmentación de Adobes Experience Platform: Permite generar segmentos a partir del Perfil del cliente en tiempo real.
- [Modelo de datos de experiencia (XDM)](../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

## Cómo definir relaciones XDM

La definición de relaciones con la estructura de los esquemas del Modelo de datos de experiencia (XDM) es una parte importante e integral de la creación de segmentos.

Este proceso se puede realizar mediante la API del Registro de Esquemas o el Editor de Esquemas. Para obtener una guía detallada sobre el uso de la API para definir una relación entre dos esquemas, lea [el tutorial sobre la definición de una relación entre dos esquemas mediante la API](../xdm/tutorials/relationship-api.md). Para obtener una guía detallada sobre el uso del Editor de Esquemas para definir una relación entre dos esquemas, lea [el tutorial sobre la definición de una relación entre dos esquemas con el Editor](../xdm/tutorials/relationship-ui.md)de Esquemas.

## Cómo crear segmentos que utilicen relaciones XDM

Una vez definidas las relaciones XDM, puede utilizar la API de servicio de segmentación para crear un segmento.

Este proceso se puede realizar mediante la API de segmentación o la interfaz de usuario del Generador de segmentos. Para obtener una guía detallada sobre el uso de la API para crear un segmento, lea [el tutorial sobre la creación de un segmento mediante la API](./tutorials/create-a-segment.md)de segmentación. Para obtener una guía detallada sobre el uso del Generador de segmentos para generar un segmento, consulte [la guía](./ui/overview.md)de usuario del Generador de segmentos.

## Cómo evaluar y acceder a segmentos para segmentos de varias entidades

Después de crear un segmento, puede evaluar los resultados del mismo y acceder a ellos mediante la [!DNL Segmentation Service] API. Evaluar un segmento de varias entidades es muy similar a evaluar un segmento normal.

Este proceso solo se puede realizar mediante la [!DNL Segmentation Service] API. Para obtener una guía detallada sobre el uso de la API para evaluar y acceder a segmentos, lea el tutorial sobre [evaluación y acceso a segmentos](./tutorials/evaluate-a-segment.md).