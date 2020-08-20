---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments
solution: Experience Platform
title: Segmentación multientidad
topic: overview
description: La segmentación de varias entidades es la capacidad de ampliar los datos de Perfil con datos adicionales basados en productos, almacenes u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema de Perfil.
translation-type: tm+mt
source-git-commit: cb5df9b44486bda84f08805f1077d6097e3666e2
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Segmentación multientidad

La segmentación de varias entidades es la capacidad de ampliar [!DNL Profile] datos con datos adicionales basados en productos, almacenes u otras clases que no son de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del [!DNL Profile] esquema.

Para obtener más información sobre la segmentación multientidad, siga leyendo la documentación y complementando su aprendizaje, vea el siguiente vídeo o explore la información general [de la](./home.md)segmentación.

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que intervienen en el uso de la segmentación. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [!DNL Real-time Customer Profile](../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [Servicio](./home.md)de segmentación de Adobe Experience Platform: Permite generar segmentos a partir del Perfil del cliente en tiempo real.
- [!DNL Experience Data Model (XDM)](../xdm/home.md):: El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

## Cómo definir relaciones XDM

La definición de relaciones con la estructura de sus esquemas [!DNL Experience Data Model] (XDM) es una parte importante e integral de la creación de segmentos.

Este proceso puede realizarse mediante la [!DNL Schema Registry] API o la [!DNL Schema Editor]. Para obtener una guía detallada sobre el uso de la API para definir una relación entre dos esquemas, lea [el tutorial sobre la definición de una relación entre dos esquemas mediante la API](../xdm/tutorials/relationship-api.md). Para obtener una guía detallada sobre el uso de [!DNL Schema Editor] para definir una relación entre dos esquemas, lea [el tutorial sobre la definición de una relación entre dos esquemas con el Editor](../xdm/tutorials/relationship-ui.md)de Esquemas.

## Cómo crear segmentos que utilicen relaciones XDM

Una vez definidas las relaciones XDM, puede utilizar la [!DNL Segmentation Service] API para crear un segmento.

Este proceso se puede realizar mediante la [!DNL Segmentation] API o la interfaz [!DNL Segment Builder] de usuario. Para obtener una guía detallada sobre el uso de la API para crear un segmento, lea [el tutorial sobre la creación de un segmento mediante la API](./tutorials/create-a-segment.md)de segmentación. Para obtener una guía detallada sobre el uso del Generador de segmentos para generar un segmento, consulte [la guía](./ui/overview.md)de usuario del Generador de segmentos.

## Cómo evaluar y acceder a segmentos para segmentos de varias entidades

Después de crear un segmento, puede evaluar los resultados del mismo y acceder a ellos mediante la [!DNL Segmentation Service] API. Evaluar un segmento de varias entidades es muy similar a evaluar un segmento normal.

Este proceso solo se puede realizar mediante la [!DNL Segmentation Service] API. Para obtener una guía detallada sobre el uso de la API para evaluar y acceder a segmentos, lea el tutorial sobre [evaluación y acceso a segmentos](./tutorials/evaluate-a-segment.md).