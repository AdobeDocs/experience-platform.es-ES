---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Tutoriales de segmentación
topic-legacy: tutorial
type: Tutorial
description: El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite crear segmentos y generar audiencias a partir de los datos del perfil del cliente en tiempo real. Estos segmentos están configurados y mantenidos de forma centralizada en Platform y son fácilmente accesibles para cualquier solución de Adobe.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
source-git-commit: 36f64b3a1e75c9badaee29e28408504eabac64fe
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Tutoriales de segmentación

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permite crear segmentos y generar audiencias a partir de sus datos [!DNL Real-time Customer Profile]. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform] y son fácilmente accesibles para cualquier solución de Adobe. Para obtener más información sobre la segmentación, comience por leer la [información general del Servicio de segmentación](../segmentation/home.md).

## Crear una definición de segmento

Una definición de segmento es el conjunto de reglas que se utiliza para describir características clave o el comportamiento de una audiencia de destino. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia cualificados para un segmento. El desarrollo, la prueba, la previsualización y el guardado de una definición de segmento se pueden realizar utilizando la interfaz de usuario o las API [!DNL Platform]. Para crear una definición de segmento, siga el [tutorial de creación de una API de segmento](../segmentation/tutorials/create-a-segment.md) o la [guía del usuario del Generador de segmentos](../segmentation/ui/overview.md).

## Evaluar un segmento y acceder a los resultados

Una vez que haya desarrollado, probado y guardado su definición de segmento, puede evaluar el segmento mediante una evaluación programada o una evaluación bajo demanda. La evaluación programada (también conocida como &quot;segmentación programada&quot;) le permite crear una programación recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que la evaluación bajo demanda implica crear un trabajo de segmento para crear la audiencia inmediatamente. Para obtener más información, visite el tutorial para [evaluar y acceder a los resultados del segmento](../segmentation/tutorials/evaluate-a-segment.md).

## Exportación de datos de segmentos

La exportación de segmentos que contienen [!DNL Profile] datos requiere primero [crear un conjunto de datos en el que se exportarán los datos](../segmentation/tutorials/create-dataset-export-segment.md) y, a continuación, iniciar un nuevo trabajo de exportación. Los pasos para generar un trabajo de exportación se encuentran en el tutorial sobre la [evaluación de un segmento](../segmentation/tutorials/evaluate-a-segment.md).

## Configuración de directivas de combinación

Adobe Experience Platform le permite agrupar los datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para obtener más información sobre las políticas de combinación y la función que desempeñan en el Experience Platform, lea en primer lugar la [información general sobre las políticas de combinación](../profile/merge-policies/overview.md).

## Aplicar el cumplimiento de uso de datos para los segmentos

Los segmentos que están habilitados para su uso en [!DNL Real-time Customer Profile] contienen un ID de política de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre qué conjuntos de datos se incluyen en el segmento, que a su vez contienen cualquier etiqueta de uso de datos aplicable. Para ver los pasos específicos que abarcan la aplicación del cumplimiento de las normas de uso de datos para un segmento de audiencia, siga el [tutorial de cumplimiento del uso de datos para segmentos](../segmentation/tutorials/governance.md).

## Segmentación por transmisión

La segmentación por transmisión es la capacidad de evaluar instantáneamente a un cliente en cuanto un evento entra en un grupo de segmentos determinado. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a Adobe Experience Platform, lo que significa que la pertenencia a los segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados. Para obtener más información, visite [descripción general de la segmentación de flujo continuo](../segmentation/api/streaming-segmentation.md).

## Segmentación de varias entidades

La segmentación de varias entidades es la capacidad de ampliar [!DNL Profile] datos con datos adicionales basados en productos, tiendas u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema [!DNL Profile]. Para aprender a mover, consulte la [documentación de segmentación de varias entidades](../segmentation/multi-entity-segmentation.md).
