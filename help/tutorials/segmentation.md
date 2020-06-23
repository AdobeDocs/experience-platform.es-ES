---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriales de segmentación
topic: tutorial
translation-type: tm+mt
source-git-commit: 636fae71f9c826ce9715bd96a974e5f6afbffb42
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Tutoriales de segmentación

El servicio de segmentación por Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite crear segmentos y generar audiencias a partir de los datos de Perfil del cliente en tiempo real. Estos segmentos están configurados y mantenidos de forma centralizada en Platform y son fácilmente accesibles para cualquier solución de Adobe. Para obtener más información sobre la segmentación, lea la información general [del servicio](../segmentation/home.md)de segmentación.

## Crear una definición de segmento

Una definición de segmento es el conjunto de reglas utilizado para describir las características clave o el comportamiento de una audiencia de destinatario. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia que cumplen los requisitos para un segmento. El desarrollo, la prueba, la vista previa y el guardado de una definición de segmento se pueden realizar mediante la interfaz de usuario o las API de Platform. Para crear una definición de segmento, siga el tutorial [de](../segmentation/tutorials/create-a-segment.md) creación de una API de segmento o la guía [de usuario de la interfaz de usuario del Generador de](../segmentation/ui/overview.md)segmentos.

## Evaluar un segmento y acceder a los resultados

Una vez desarrollada, probada y guardada la definición del segmento, puede evaluar el segmento mediante una evaluación programada o una evaluación a petición. La evaluación programada (también conocida como &#39;segmentación programada&#39;) le permite crear una programación recurrente para ejecutar un trabajo de exportación a una hora específica, mientras que la evaluación a petición implica crear un trabajo de segmento para generar la audiencia inmediatamente. Para obtener más información, visite el tutorial para [evaluar y acceder a los resultados](../segmentation/tutorials/evaluate-a-segment.md)de los segmentos.

## Exportar datos de segmentos

La exportación de segmentos que contengan datos de Perfil requiere primero [crear un conjunto de datos en el que se exportarán](../segmentation/tutorials/create-dataset-export-segment.md)los datos y, a continuación, iniciar un nuevo trabajo de exportación. Los pasos para generar un trabajo de exportación se encuentran en el tutorial [de la API de](../segmentation/tutorials/export-data.md)exportación.

## Configurar directivas de combinación

Adobe Experience Platform le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para trabajar con políticas de combinación en la interfaz de usuario de Platform, visite la guía [del usuario de directivas de](../profile/ui/merge-policies.md)combinación. Para trabajar con políticas de combinación mediante la API de Perfil del cliente en tiempo real, consulte la guía [para desarrolladores de políticas de](../profile/api/merge-policies.md)combinación.

## Aplicar la conformidad de uso de datos para segmentos

Los segmentos que están habilitados para su uso en el Perfil del cliente en tiempo real contienen un ID de directiva de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre los conjuntos de datos que se deben incluir en el segmento, que a su vez contienen las etiquetas de uso de datos aplicables. Para ver los pasos específicos que abarcan la aplicación de la conformidad con el uso de datos para un segmento de audiencia, siga el tutorial de cumplimiento de la normativa de uso de [datos para segmentos](../segmentation/tutorials/governance.md).

## (Beta) Segmentación por flujo continuo

>[!NOTE]
>La segmentación por flujo continuo está en fase beta y estará disponible bajo petición. Las funciones y la documentación están sujetas a cambios.

La segmentación por flujo continuo es la capacidad de evaluar instantáneamente a un cliente tan pronto como un evento entra en un grupo de segmentos en particular. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a Adobe Experience Platform, lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados. Para obtener más información, visite la descripción general [de la segmentación de](../segmentation/api/streaming-segmentation.md)flujo.

## Segmentación multientidad

La segmentación de varias entidades es la capacidad de ampliar los datos de Perfil con datos adicionales basados en productos, almacenes u otras clases que no sean de perfil. Una vez conectados, los datos de clases adicionales estarán disponibles como si fueran nativos del esquema de Perfil. Para aprender a mover, consulte la documentación [de segmentación de](../segmentation/multi-entity-segmentation.md)varias entidades.