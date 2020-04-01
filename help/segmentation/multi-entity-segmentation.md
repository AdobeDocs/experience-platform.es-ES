---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentación multientidad
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Segmentación multientidad

La segmentación de varias entidades es la capacidad de ampliar los datos de Perfil con datos adicionales basados en productos, almacenes u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema de Perfil.

Para obtener más información sobre la segmentación multientidad, lea la información general [de](./home.md)segmentación.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que intervienen en el uso de la segmentación. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Perfil](../profile/home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [Servicio](./home.md)de segmentación de la plataforma Adobe Experience: Permite generar segmentos a partir del Perfil del cliente en tiempo real.
- [Modelo de datos de experiencia (XDM)](../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

## Cómo definir relaciones XDM

La definición de relaciones con la estructura de los esquemas del Modelo de datos de experiencia (XDM) es una parte importante e integral de la creación de segmentos.

Este proceso se puede realizar mediante la API del Registro de Esquemas o el Editor de Esquemas. Para obtener una guía detallada sobre el uso de la API para definir una relación entre dos esquemas, lea [el tutorial sobre la definición de una relación entre dos esquemas mediante la API](../xdm/tutorials/relationship-api.md). Para obtener una guía detallada sobre el uso del Editor de Esquemas para definir una relación entre dos esquemas, lea [el tutorial sobre la definición de una relación entre dos esquemas con el Editor](../xdm/tutorials/relationship-ui.md)de Esquemas.

## Cómo utilizar la creación de segmentos que utilicen relaciones XDM

Una vez definidas las relaciones XDM, puede utilizar las API de Perfil del cliente en tiempo real para crear un segmento.

Este proceso se puede realizar mediante la API de Perfil del cliente en tiempo real o el Generador de segmentos. Para obtener una guía detallada sobre el uso de la API para crear un segmento, lea [el tutorial sobre la creación de un segmento mediante la API](./tutorials/create-a-segment.md)de Perfil del cliente en tiempo real. Para obtener una guía detallada sobre el uso del Generador de segmentos para generar un segmento, consulte [la guía](./ui/overview.md)de usuario del Generador de segmentos.

## Cómo evaluar y acceder a segmentos para segmentos de varias entidades

Después de crear un segmento, puede evaluarlo y acceder a los resultados del mismo mediante las API de Perfil del cliente en tiempo real. Evaluar un segmento de varias entidades es muy similar a evaluar un segmento normal.

Este proceso solo se puede realizar mediante la API de Perfil del cliente en tiempo real. Para obtener una guía detallada sobre el uso de la API para evaluar y acceder a segmentos, lea [el tutorial sobre evaluación y acceso a segmentos](./tutorials/evaluate-a-segment.md).