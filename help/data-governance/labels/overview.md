---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre las etiquetas de uso de datos
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Información general sobre las etiquetas de uso de datos

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo central del control de datos de la plataforma de experiencia de Adobe. Las funciones DULE permiten aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada una según las políticas de uso de datos relacionadas.

Este documento proporciona información general sobre las etiquetas de uso de datos (también conocidas como etiquetas DULE) en la plataforma de experiencia. Antes de leer esta guía, consulte la información general [sobre la gobernanza de](../home.md) datos para obtener una introducción más sólida al marco DULE.

## Explicación de las etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de los datos tan pronto como se incorporan a la plataforma de experiencia o tan pronto como los datos estén disponibles para su uso en la plataforma.

Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación.

Para obtener más información sobre las etiquetas de uso de datos disponibles en la plataforma de experiencia y las políticas de uso que representan, consulte la guía sobre etiquetas [de uso de datos](reference.md)admitidas.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por el servicio [de segmentación de](../../segmentation/home.md) Adobe Experience Platform heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite que las aplicaciones creadas en la parte superior de la plataforma de experiencias (como la plataforma de datos del cliente en tiempo real) proporcionen una aplicación automática de las políticas de uso de datos al activar segmentos en destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Según el modo en que la aplicación basada en plataforma consuma segmentos, puede especificar potencialmente qué campos se utilizan, impidiendo así que el segmento herede etiquetas de campos excluidos.

Para obtener más información sobre cómo funciona la aplicación automática en tiempo real de CDP, consulte la información general [sobre la administración de datos CDP en tiempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.

## Pasos siguientes

Ahora que se le han introducido etiquetas de uso de datos, puede seguir leyendo la guía [del](user-guide.md) usuario para aprender a administrar etiquetas en la interfaz de usuario de la plataforma de experiencia. Para ver los pasos sobre cómo administrar etiquetas mediante API, consulte la sección correspondiente en la guía [para desarrolladores del servicio de](../../catalog/api/labels.md)catálogos.