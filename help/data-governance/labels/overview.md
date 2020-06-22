---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre las etiquetas de uso de datos
topic: labels
translation-type: tm+mt
source-git-commit: e3c69589e0d4f8224b74a663b23f67e6731ddec4
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Información general sobre las etiquetas de uso de datos

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo central del gobierno de datos de Adobe Experience Platform. Las funciones DULE permiten aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada una según las políticas de uso de datos relacionadas.

Este documento proporciona información general sobre las etiquetas de uso de datos (también conocidas como etiquetas DULE) en Experience Platform. Antes de leer esta guía, consulte la información general [sobre la gobernanza de](../home.md) datos para obtener una introducción más sólida al marco DULE.

## Explicación de las etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de datos tan pronto como se ingesta en el Experience Platform o tan pronto como los datos estén disponibles para su uso en Platform.

Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación.

Para obtener más información sobre las etiquetas de uso de datos disponibles en Experience Platform y las políticas de uso que representan, consulte la guía sobre las etiquetas [de uso de datos](reference.md)admitidas.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por el servicio [de segmentación de](../../segmentation/home.md) Adobes Experience Platform heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite que las aplicaciones creadas sobre el Experience Platform (por ejemplo, Platform de datos del cliente en tiempo real) proporcionen una aplicación automática de la política de uso de datos al activar segmentos en destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Según el modo en que la aplicación basada en Platform consuma segmentos, puede especificar potencialmente qué campos se utilizan, impidiendo así que el segmento herede etiquetas de campos excluidos.

Para obtener más información sobre cómo funciona la aplicación automática en tiempo real de CDP, consulte la información general [sobre la administración de datos CDP en tiempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Pasos siguientes

Ahora que ya ha introducido las etiquetas de uso de datos, puede seguir leyendo la guía [del](user-guide.md) usuario para aprender a administrar las etiquetas en la interfaz de usuario del Experience Platform. Para ver los pasos sobre cómo administrar etiquetas mediante API, consulte la sección correspondiente en la guía [para desarrolladores del servicio de](../../catalog/api/labels.md)catálogos.