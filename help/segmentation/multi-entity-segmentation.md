---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentos;segmentos;segmentos;varias entidades;segmentación de varias entidades;segmentos de varias entidades;
solution: Experience Platform
title: Resumen de segmentación de varias entidades
description: La segmentación de varias entidades es la capacidad de ampliar datos de perfil con datos adicionales basados en productos, tiendas u otras clases que no sean de perfil. Una vez conectado, los datos de las clases adicionales están disponibles como si fueran nativos del esquema Profile.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Resumen de segmentación de varias entidades

La segmentación de varias entidades es una función avanzada disponible como parte de Adobe Experience Platform [!DNL Segmentation Service]. Esta función le permite ampliar [!DNL Real-Time Customer Profile] datos con datos adicionales de &quot;no personas&quot; (también conocidos como &quot;entidades de dimensión&quot;) que su organización puede definir, como datos relacionados con productos o tiendas. La segmentación de varias entidades proporciona flexibilidad al definir segmentos de audiencia basados en datos relevantes para sus necesidades comerciales únicas y se puede realizar sin tener experiencia en la consulta de bases de datos. Con la segmentación de varias entidades, puede añadir datos clave a sus segmentos sin tener que realizar cambios costosos en las secuencias de datos o esperar a una combinación de datos back-end.

## Primeros pasos

La segmentación de varias entidades requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform que intervienen en la segmentación. Antes de continuar con esta guía, revise la siguiente documentación:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real, basado en los datos agregados de varias fuentes.
   * [Protecciones de perfil](../profile/guardrails.md): Prácticas recomendadas para crear modelos de datos compatibles con [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): le permite generar segmentos desde [!DNL Real-Time Customer Profile] datos.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../xdm/schema/composition.md#union): Conozca las prácticas recomendadas para componer esquemas para utilizarlos en Experience Platform. Para utilizar mejor la segmentación, asegúrese de que sus datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../xdm/schema/best-practices.md).

## Casos de uso

Para ilustrar el valor de la segmentación de varias entidades, considere tres casos de uso de marketing estándar que ilustran los desafíos presentes en la mayoría de las aplicaciones de marketing:

### Combinación de datos de compra en línea y sin conexión

Un experto en marketing que crea una campaña de correo electrónico puede haber intentado crear un segmento para una audiencia objetivo utilizando compras recientes de tiendas de clientes en los últimos tres meses. Lo ideal es que este segmento requiera el nombre del elemento y el nombre de la tienda en la que se realizó la compra. Anteriormente, el desafío habría sido capturar el identificador de tienda desde el evento de compra y asignarlo a un perfil de cliente individual.

### Retargeting de correo electrónico para abandono del carro

A menudo es complejo crear y clasificar usuarios en segmentos dirigidos al abandono del carro de compras. Saber qué productos incluir en una campaña de resegmentación personalizada requiere datos sobre qué productos abandonó cada individuo. Estos datos están vinculados a eventos de comercio que anteriormente eran difíciles de monitorizar y extraer de.

## Creación de segmentos de varias entidades

La creación de un segmento de varias entidades primero requiere la definición de relaciones entre esquemas antes de utilizar [!DNL Segmentation] API o IU del Generador de segmentos para crear la definición del segmento.

### Definición de relaciones

La definición de relaciones dentro de la estructura de los esquemas XDM (Experience Data Model) es una parte integral de la creación de segmentos de varias entidades. Para las relaciones, el campo del destino debe marcarse como la identidad principal de ese esquema. Una identidad solo se puede marcar en cadenas y no en matrices. Además, las relaciones no necesariamente tienen que ser una a una, ya que puede conectar perfiles y eventos de experiencia a varios destinos.

La definición de relaciones se puede realizar mediante la API del Registro de esquemas o el Editor de esquemas. Para ver los pasos detallados que muestran cómo definir una relación entre dos esquemas, elija entre los siguientes tutoriales:

* [Definición de una relación entre dos esquemas mediante la API](../xdm/tutorials/relationship-api.md)
* [Definición de una relación entre dos esquemas mediante la IU del Editor de Esquemas](../xdm/tutorials/relationship-ui.md)

### Creación de un segmento de varias entidades

Una vez que haya definido las relaciones XDM necesarias, puede empezar a crear un segmento de varias entidades. Esto se puede hacer mediante la API de segmentación o la interfaz de usuario del Generador de segmentos. Para obtener más información, elija una de las siguientes guías:

* [Creación de un segmento mediante la API de segmentación](./tutorials/create-a-segment.md)
* [Creación de un segmento mediante la interfaz de usuario del Generador de segmentos](./ui/overview.md)

## Evaluación y acceso a segmentos de varias entidades

Después de crear un segmento, puede evaluar y acceder a los resultados del mismo mediante la API de segmentación. La evaluación de un segmento de varias entidades es muy similar a la evaluación de un segmento estándar. Este proceso solo se puede realizar mediante la API de segmentación. Para obtener una guía detallada que muestra cómo utilizar la API para evaluar segmentos y acceder a ellos, lea la [evaluación y acceso a segmentos](./tutorials/evaluate-a-segment.md) tutorial.
