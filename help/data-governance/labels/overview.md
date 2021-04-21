---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas;descripción general de etiquetas de uso de datos
solution: Experience Platform
title: Información general sobre las etiquetas de uso de datos
topic-legacy: labels
description: La administración de datos de Adobe Experience Platform permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada uno según las políticas de uso de datos relacionadas. Este documento proporciona información general sobre las etiquetas de uso de datos en Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Información general sobre las etiquetas de uso de datos

Adobe Experience Platform [!DNL Data Governance] permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada uno según las políticas de uso de datos relacionadas.

Este documento proporciona información general sobre las etiquetas de uso de datos en [!DNL Experience Platform]. Antes de leer esta guía, consulte la [información general sobre el control de datos](../home.md) para obtener una introducción más sólida al marco de control de datos.

## Información sobre las etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. Las prácticas recomendadas recomiendan el etiquetado de datos tan pronto como se incorporan a [!DNL Experience Platform] o tan pronto como los datos estén disponibles para su uso en [!DNL Platform].

Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación.

[!DNL Platform] proporciona varias etiquetas de uso de datos &quot;principales&quot; listas para usar, que abarcan una amplia variedad de restricciones comunes aplicables al control de datos. Para obtener más información sobre estas etiquetas y las políticas de uso que representan, consulte la guía sobre [etiquetas de uso de datos principales](reference.md).

Además de las etiquetas proporcionadas por Adobe, también puede definir sus propias etiquetas personalizadas para su organización. Consulte la sección sobre [administración de etiquetas](#manage-labels) para obtener más información.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite al Experience Platform proporcionar una aplicación automática de la directiva de uso de datos al activar segmentos en destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Por lo tanto, puede identificar con mayor facilidad qué atributos deben excluirse de los segmentos e impedir que hereden etiquetas de campos excluidos.

Para obtener más información sobre cómo funciona la aplicación automática en Platform, consulte la descripción general de [aplicación automática de políticas](../enforcement/auto-enforcement.md).

### Herencia de los controles de exportación de datos de Adobe Audience Manager

[!DNL Experience Platform] tiene la capacidad de compartir segmentos con Adobe Audience Manager. Cualquier control de exportación de datos que se haya aplicado a segmentos de Audience Manager se traduce a etiquetas y acciones de marketing equivalentes reconocidas por [!DNL Experience Platform] [!DNL Data Governance].

Para obtener una referencia sobre cómo los controles de exportación de datos específicos se asignan a las etiquetas de uso de datos en [!DNL Platform], consulte la [documentación del Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Administración de etiquetas de uso de datos en [!DNL Experience Platform] {#manage-labels}

Puede administrar las etiquetas de uso de datos mediante las API [!DNL Experience Platform] o la interfaz de usuario. Consulte las subsecciones siguientes para obtener más información sobre cada una.

### Uso de la interfaz de usuario

El espacio de trabajo **[!UICONTROL Policies]** en la interfaz de usuario [!DNL Experience Platform] le permite ver y administrar las etiquetas principales y personalizadas de su organización. El espacio de trabajo **[!DNL Datasets]** permite aplicar etiquetas a conjuntos de datos y campos. Para obtener más información, consulte la [guía del usuario de etiquetas](user-guide.md).

### Uso de API

El extremo `/labels` de la [API del servicio de directivas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) le permite administrar mediante programación las etiquetas de uso de datos, incluida la creación de etiquetas personalizadas. Consulte la [guía de extremo de etiquetas](../api/labels.md) para obtener más información.

La [API del servicio de conjunto de datos](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) se utiliza para administrar etiquetas para conjuntos de datos y campos. Consulte la guía sobre [administración de etiquetas de conjuntos de datos](./dataset-api.md) para obtener más información.

## Pasos siguientes

Este documento ofrecía una introducción a las etiquetas de uso de datos y su función dentro del marco de control de datos. Consulte la documentación vinculada a través de esta guía para obtener más información sobre cómo administrar las etiquetas en [!DNL Experience Platform].
