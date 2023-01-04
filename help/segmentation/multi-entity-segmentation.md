---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentos;segmentos;segmentos;varias entidades;segmentación multientidad;segmentos multientidad;
solution: Experience Platform
title: Información general sobre la segmentación de varias entidades
topic-legacy: overview
description: La segmentación de varias entidades es la capacidad de ampliar los datos del perfil con datos adicionales basados en productos, tiendas u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema de perfil.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Resumen de segmentación de varias entidades

La segmentación de varias entidades es una función avanzada disponible como parte de Adobe Experience Platform [!DNL Segmentation Service]. Esta función le permite ampliar [!DNL Real-Time Customer Profile] datos con datos &quot;no personas&quot; adicionales (también conocidos como &quot;entidades de dimensión&quot;) que su organización puede definir, como datos relacionados con productos o almacenes. La segmentación de varias entidades proporciona flexibilidad a la hora de definir segmentos de audiencia basados en datos relevantes para sus necesidades comerciales únicas y se puede realizar sin tener experiencia en consultas de bases de datos. Con la segmentación multientidad, puede añadir datos clave a sus segmentos sin tener que realizar cambios costosos en las secuencias de datos ni esperar a una combinación de datos back-end.

## Primeros pasos

La segmentación de varias entidades requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform implicados en la segmentación. Antes de continuar con esta guía, revise la siguiente documentación:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
   * [Protecciones de perfil](../profile/guardrails.md): Prácticas recomendadas para crear modelos de datos compatibles con [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite generar segmentos a partir de [!DNL Real-Time Customer Profile] datos.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../xdm/schema/composition.md#union): Conozca las prácticas recomendadas para componer esquemas para utilizarlos en Experience Platform. Para utilizar mejor la segmentación, asegúrese de que los datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../xdm/schema/best-practices.md).

## Casos de uso

Para ilustrar el valor de la segmentación de varias entidades, considere tres casos de uso de marketing estándar que ilustren los desafíos presentes en la mayoría de las aplicaciones de marketing:

### Combinación de datos de compra en línea y sin conexión

Es posible que un especialista en marketing que crea una campaña de correo electrónico haya intentado crear un segmento para una audiencia objetivo utilizando compras recientes del almacén de clientes en los últimos tres meses. Lo ideal sería que este segmento requiriera tanto el nombre del artículo como el nombre del almacén donde se realizó la compra. Anteriormente, el desafío habría sido capturar el identificador de tienda del evento de compra y asignarlo a un perfil de cliente individual.

### Retargeting de correo electrónico para el abandono del carro de compras

A menudo es complejo crear y clasificar usuarios en segmentos dirigidos al abandono del carro de compras. Saber qué productos incluir en una campaña de retargeting personalizado requiere datos sobre qué productos abandonaron cada individuo. Estos datos están vinculados a eventos de comercio que anteriormente eran un desafío para supervisar y extraer datos de.

## Creación de segmentos de varias entidades

Para crear un segmento de varias entidades, primero debe definir relaciones entre esquemas antes de usar la variable [!DNL Segmentation] API o interfaz de usuario del Generador de segmentos para crear la definición del segmento.

### Definir relaciones

La definición de relaciones dentro de la estructura de los esquemas del Modelo de datos de experiencia (XDM) es una parte integral de la creación de segmentos de varias entidades. Para las relaciones, el campo del destino debe marcarse como la identidad principal de ese esquema. Una identidad solo se puede marcar en cadenas y no en matrices. Además, las relaciones no tienen que ser necesariamente una a una, ya que puede conectar perfiles y eventos de experiencia a varios destinos.

La definición de relaciones se puede realizar mediante la API del Registro de esquemas o el Editor de esquemas. Para ver los pasos detallados que muestran cómo definir una relación entre dos esquemas, elija entre los siguientes tutoriales:

* [Definición de una relación entre dos esquemas mediante la API](../xdm/tutorials/relationship-api.md)
* [Definición de una relación entre dos esquemas mediante la IU del Editor de esquemas](../xdm/tutorials/relationship-ui.md)

### Generar un segmento de varias entidades

Una vez definidas las relaciones XDM necesarias, puede empezar a crear un segmento de varias entidades. Esto se puede hacer mediante la API de segmentación o la interfaz de usuario del Generador de segmentos. Para obtener más información, elija una de las siguientes guías:

* [Creación de un segmento mediante la API de segmentación](./tutorials/create-a-segment.md)
* [Creación de un segmento mediante la interfaz de usuario del Generador de segmentos](./ui/overview.md)

## Evaluar y acceder a segmentos de varias entidades

Después de crear un segmento, puede evaluar los resultados del segmento y acceder a ellos mediante la API de segmentación. Evaluar un segmento de varias entidades es muy similar a evaluar un segmento estándar. Este proceso solo se puede realizar mediante la API de segmentación. Para obtener una guía detallada que muestre cómo utilizar la API para evaluar y acceder a segmentos, lea la [evaluación y acceso a segmentos](./tutorials/evaluate-a-segment.md) tutorial.
