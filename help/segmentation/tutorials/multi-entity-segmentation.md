---
solution: Experience Platform
title: Resumen de segmentación de varias entidades
description: La segmentación de varias entidades es la capacidad de ampliar datos de perfil con datos adicionales basados en productos, tiendas u otras clases que no sean de perfil. Una vez conectado, los datos de las clases adicionales están disponibles como si fueran nativos del esquema Profile.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 630041a7ef82993038ef4510dd08d3bc67bfce41
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Resumen de segmentación de varias entidades

La segmentación de varias entidades es una característica avanzada disponible como parte de Adobe Experience Platform [!DNL Segmentation Service]. Esta característica le permite ampliar datos de [!DNL Real-Time Customer Profile] con datos adicionales de &quot;no personas&quot; (también conocidos como &quot;entidades de dimensión&quot;) que su organización puede definir, como datos relacionados con productos o tiendas. La segmentación de varias entidades proporciona flexibilidad al definir definiciones de segmentos basadas en datos relevantes para sus necesidades comerciales únicas y se puede realizar sin tener experiencia en la consulta de bases de datos. Con la segmentación de varias entidades, puede añadir datos clave a las definiciones de segmentos sin tener que realizar cambios costosos en las secuencias de datos o esperar a una combinación de datos back-end.

## Introducción

La segmentación de varias entidades requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform que intervienen en la segmentación. Antes de continuar con esta guía, revise la siguiente documentación:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado en tiempo real, basado en los datos agregados de varias fuentes.
   * [Protecciones de perfil](../../profile/guardrails.md): prácticas recomendadas para crear modelos de datos compatibles con [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite crear audiencias a partir de los datos de [!DNL Real-Time Customer Profile].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../xdm/schema/composition.md#union): Conozca las prácticas recomendadas para componer esquemas para utilizarlos en Experience Platform. Para utilizar la segmentación de la mejor manera posible, asegúrate de que tus datos se incorporen como perfiles y eventos según las [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).

## Casos de uso

Para ilustrar el valor de la segmentación de varias entidades, considere tres casos de uso de marketing estándar que ilustran los desafíos presentes en la mayoría de las aplicaciones de marketing:

### Combinación de datos de compra en línea y sin conexión

Un experto en marketing que crea una campaña de correo electrónico puede haber intentado crear una audiencia utilizando compras recientes de tiendas de clientes en los últimos tres meses. Lo ideal es que esta audiencia requiera el nombre del elemento y el nombre de la tienda en la que se realizó la compra. Anteriormente, el desafío habría sido capturar el identificador de tienda desde el evento de compra y asignarlo a un perfil de cliente individual.

### Retargeting de correo electrónico para abandono del carro

La creación y calificación de usuarios en definiciones de segmentos dirigidas al abandono del carro de compras es compleja. Saber qué productos incluir en una campaña de resegmentación personalizada requiere datos sobre qué productos abandonó cada individuo. Estos datos están vinculados a eventos de comercio que anteriormente eran difíciles de monitorizar y extraer de.

## Creación de definiciones de segmentos de varias entidades

La creación de una definición de segmento de varias entidades primero requiere la definición de relaciones entre esquemas antes de utilizar la API [!DNL Segmentation] o la interfaz de usuario del Generador de segmentos para generar la definición del segmento.

### Definición de relaciones

La definición de relaciones dentro de la estructura de los esquemas XDM (Experience Data Model) es una parte integral de la creación de segmentos de varias entidades. Para las relaciones, el campo del destino debe marcarse como la identidad principal de ese esquema. Una identidad solo se puede marcar en cadenas y no en matrices. Además, las relaciones no necesariamente tienen que ser una a una, ya que puede conectar perfiles y eventos de experiencia a varios destinos.

La definición de relaciones se puede realizar mediante la API del Registro de esquemas o el Editor de esquemas. Para ver los pasos detallados que muestran cómo definir una relación entre dos esquemas, elija entre los siguientes tutoriales:

* [Definición de una relación entre dos esquemas mediante la API](../../xdm/tutorials/relationship-api.md)
* [Definición de una relación entre dos esquemas mediante la IU del Editor de Esquemas](../../xdm/tutorials/relationship-ui.md)

### Creación de una definición de segmento de varias entidades

Una vez que haya definido las relaciones XDM necesarias, puede empezar a crear una definición de segmento de varias entidades. Esto se puede hacer mediante la API de segmentación o la interfaz de usuario del Generador de segmentos. Para obtener más información, elija una de las siguientes guías:

* [Creación de una definición de segmento mediante la API de segmentación](./create-a-segment.md)
* [Creación de una definición de segmento mediante la interfaz de usuario del Generador de segmentos](../ui/overview.md)

## Evaluación y acceso a definiciones de segmentos de varias entidades

Después de crear una definición de segmento, puede evaluar los resultados y acceder a ellos mediante la API de segmentación. La evaluación de una definición de segmento de varias entidades es muy similar a la evaluación de una definición de segmento estándar. Este proceso solo se puede realizar mediante la API de segmentación. Para obtener una guía detallada que muestra cómo usar la API para evaluar y acceder a las definiciones de segmentos, lea el tutorial [evaluación y acceso a las definiciones de segmentos](./evaluate-a-segment.md).
