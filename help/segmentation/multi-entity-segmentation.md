---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: Segmentación multientidad
topic: overview
description: La segmentación de varias entidades es la capacidad de ampliar los datos de Perfil con datos adicionales basados en productos, almacenes u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema de Perfil.
translation-type: tm+mt
source-git-commit: 4dd5a91146b116953ba180e3f39d24b4e1ec289e
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# Segmentación multientidad

La segmentación multientidad es una función avanzada disponible como parte de Adobe Experience Platform [!DNL Segmentation Service]. Esta función le permite ampliar [!DNL Real-time Customer Profile] los datos con datos &quot;no personales&quot; adicionales (también conocidos como &quot;entidades de dimensión&quot;) que su organización puede definir, como datos relacionados con productos o almacenes. La segmentación multientidad proporciona flexibilidad al definir segmentos de audiencia en función de datos relevantes para sus necesidades comerciales únicas y se puede realizar sin tener experiencia en consultar bases de datos. Con la segmentación multientidad, puede agregar datos clave a los segmentos sin tener que realizar cambios costosos en los flujos de datos ni esperar a una combinación de datos back-end.

## Primeros pasos

La segmentación de varias entidades requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform implicados en la segmentación. Antes de continuar con esta guía, consulte la siguiente documentación:

* [[!Perfil del cliente en tiempo real de DNL]](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
   * [Guardias](../profile/guardrails.md)de perfil: Prácticas recomendadas para crear modelos de datos compatibles con [!DNL Profile].
* [[!Servicio de segmentación de Adobe Experience Platform DNL]](./home.md): Permite generar segmentos a partir de [!DNL Real-time Customer Profile] datos.
* [[!Modelo de datos de experiencia DNL (XDM)]](../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../xdm/schema/composition.md#union)de esquemas: Conozca las prácticas recomendadas para la composición de esquemas que se utilizarán en Experience Platform.

## Casos de uso

Para ilustrar el valor de la segmentación de varias entidades, considere tres casos de uso de mercadotecnia estándar que ilustran los desafíos presentes en la mayoría de las aplicaciones de mercadotecnia:

### Combinación de datos de compras en línea y sin conexión

Es posible que un especialista en mercadotecnia que crea una campaña de correo electrónico haya intentado crear un segmento para una audiencia de destinatario mediante el uso de compras recientes del almacén de clientes en los últimos tres meses. Lo ideal sería que este segmento requiriera tanto el nombre del artículo como el nombre del almacén donde se realizó la compra. Anteriormente, el desafío habría sido capturar el identificador de tienda del evento de compra y asignarlo a un perfil de cliente individual.

### Redireccionamiento por correo electrónico para abandono del carro de compras

A menudo es complejo crear y clasificar usuarios en segmentos que tengan como objetivo el abandono del carro de compras. El saber qué productos incluir en una campaña de redireccionamiento personalizada requiere datos sobre qué productos abandonó cada individuo. Estos datos están ligados a eventos comerciales que antes eran difíciles de monitorear y extraer datos.

## Creación de segmentos de varias entidades

La creación de un segmento de varias entidades primero requiere definir las relaciones entre esquemas antes de utilizar la interfaz de usuario de la API o del Generador de segmentos para generar la definición del segmento. [!DNL Segmentation]

### Definir relaciones

La definición de relaciones dentro de la estructura de los esquemas del Modelo de datos de experiencia (XDM) es una parte integral de la creación de segmentos de varias entidades. Para las relaciones, el campo del destino debe marcarse como la identidad principal de ese esquema. Una identidad solo se puede marcar en cadenas y no en matrices. Además, las relaciones no necesariamente tienen que ser una a una, ya que puede conectar perfiles y eventos de experiencia a varios destinos.

La definición de relaciones se puede realizar mediante la API del Registro de Esquemas o el Editor de Esquemas. Para ver los pasos detallados que muestran cómo definir una relación entre dos esquemas, elija uno de los siguientes tutoriales:

* [Definición de una relación entre dos esquemas mediante la API](../xdm/tutorials/relationship-api.md)
* [Definición de una relación entre dos esquemas mediante la interfaz de usuario del Editor de Esquemas](../xdm/tutorials/relationship-ui.md)

### Crear un segmento de varias entidades

Una vez definidas las relaciones XDM necesarias, puede empezar a crear un segmento de varias entidades. Esto se puede hacer mediante la API de segmentación o la interfaz de usuario del Generador de segmentos. Para obtener más información, elija una de las siguientes guías:

* [Creación de un segmento mediante la API de segmentación](./tutorials/create-a-segment.md)
* [Creación de un segmento mediante la interfaz de usuario del Generador de segmentos](./ui/overview.md)

## Evaluar y acceder a segmentos de varias entidades

Después de crear un segmento, puede evaluar los resultados del mismo y acceder a ellos mediante la API de segmentación. Evaluar un segmento de varias entidades es muy similar a evaluar un segmento estándar. Este proceso solo se puede realizar mediante la API de segmentación. Para obtener una guía detallada que muestre cómo utilizar la API para evaluar y acceder a segmentos, lea el tutorial de [evaluación y acceso a segmentos](./tutorials/evaluate-a-segment.md) .
