---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre las etiquetas de uso de datos
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Información general sobre las etiquetas de uso de datos

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo central del Adobe Experience Platform [!DNL Data Governance]. Las funciones DULE permiten aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada una según las políticas de uso de datos relacionadas.

Este documento proporciona información general sobre las etiquetas de uso de datos (también conocidas como etiquetas DULE) en [!DNL Experience Platform]. Antes de leer esta guía, consulte la información general [sobre la gobernanza de](../home.md) datos para obtener una introducción más sólida al marco DULE.

## Explicación de las etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de los datos tan pronto como se ingieran [!DNL Experience Platform]o tan pronto como los datos estén disponibles para su uso en [!DNL Platform].

Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación.

[!DNL Platform] proporciona varias etiquetas de uso de datos &quot;principales&quot; integradas, que abarcan una amplia variedad de restricciones comunes aplicables a la administración de datos. Para obtener más información sobre estas etiquetas y las políticas de uso que representan, consulte la guía sobre las etiquetas [de uso de datos](reference.md)principales.

Además de las etiquetas proporcionadas por Adobe, también puede definir sus propias etiquetas personalizadas. Para ver los pasos sobre cómo hacerlo en la interfaz de usuario, consulte la guía [del usuario de etiquetas de uso de](./user-guide.md)datos. Para ver los pasos para realizar esto mediante llamadas de API, consulte la guía [de la API de etiquetas de uso de](./api.md)datos.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por el servicio [de segmentación de](../../segmentation/home.md) Adobes Experience Platform heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite que las aplicaciones creadas sobre [!DNL Experience Platform] (por ejemplo, [!DNL Real-time Customer Data Platform]) proporcionen una aplicación automática de la directiva de uso de datos al activar segmentos en destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Según el modo en que la aplicación [!DNL Platform]basada consuma segmentos, es posible especificar qué campos se utilizan, impidiendo así que el segmento herede etiquetas de campos excluidos.

Para obtener más información sobre el funcionamiento de la aplicación automática en tiempo real de CDP, consulte la información general [sobre la administración de datos CDP en tiempo real de](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe.

### Herencia de los controles de exportación de datos de Adobe Audience Manager

[!DNL Experience Platform] tiene la capacidad de compartir segmentos con Adobe Audience Manager. Todos los controles de exportación de datos que se hayan aplicado a segmentos de Audience Manager se traducen a etiquetas y acciones de marketing equivalentes que [!DNL Experience Platform][!DNL Data Governance]reconoce.

Para obtener una referencia sobre cómo los controles de exportación de datos específicos se asignan a las etiquetas de uso de datos en [!DNL Platform], consulte la documentación [del](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.


## Pasos siguientes

Ahora que se le han introducido etiquetas de uso de datos, puede seguir leyendo la guía [del](user-guide.md) usuario para aprender a administrar etiquetas en la [!DNL Experience Platform] interfaz de usuario. Para ver los pasos sobre cómo administrar etiquetas mediante API, consulte la guía [de API de etiquetas de](./api.md)uso.