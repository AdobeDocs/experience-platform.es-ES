---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Información general sobre las etiquetas de uso de datos
topic: labels
description: La Administración de datos de Adobe Experience Platform le permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, y categorizar cada una según las políticas de uso de datos relacionadas. Este documento proporciona información general sobre las etiquetas de uso de datos en Experience Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Información general sobre las etiquetas de uso de datos

Adobe Experience Platform [!DNL Data Governance] permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada uno según las políticas de uso de datos relacionadas.

Este documento proporciona información general sobre las etiquetas de uso de datos de [!DNL Experience Platform]. Antes de leer esta guía, consulte la información general [sobre el Gobierno de](../home.md) datos para obtener una introducción más sólida al marco de administración de datos.

## Explicación de las etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de los datos tan pronto como se ingieran [!DNL Experience Platform]o tan pronto como los datos estén disponibles para su uso en [!DNL Platform].

Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación.

[!DNL Platform] proporciona varias etiquetas de uso de datos &quot;principales&quot; integradas, que abarcan una amplia variedad de restricciones comunes aplicables a la administración de datos. Para obtener más información sobre estas etiquetas y las políticas de uso que representan, consulte la guía sobre las etiquetas [de uso de datos](reference.md)principales.

Además de las etiquetas proporcionadas por Adobe, también puede definir sus propias etiquetas personalizadas para su organización. Consulte la sección sobre [administración de etiquetas](#manage-labels) para obtener más información.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por el servicio [de segmentación de](../../segmentation/home.md) Adobe Experience Platform heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite que las aplicaciones creadas sobre el Experience Platform (por ejemplo, [!DNL Real-time Customer Data Platform]) proporcionen la aplicación automática de la directiva de uso de datos al activar segmentos en destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Según el modo en que la aplicación [!DNL Platform]basada consuma segmentos, es posible especificar qué campos se utilizan, impidiendo así que el segmento herede etiquetas de campos excluidos.

Para obtener más información sobre cómo funciona la aplicación automática en tiempo real de CDP, consulte la información general sobre la administración [de datos en tiempo real de CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).

### Herencia de los controles de exportación de datos de Adobe Audience Manager

[!DNL Experience Platform] tiene la capacidad de compartir segmentos con Adobe Audience Manager. Todos los controles de exportación de datos que se hayan aplicado a segmentos de Audience Manager se traducen a etiquetas y acciones de marketing equivalentes que [!DNL Experience Platform][!DNL Data Governance]reconoce.

Para obtener una referencia sobre cómo los controles de exportación de datos específicos se asignan a las etiquetas de uso de datos en [!DNL Platform], consulte la documentación [del](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.

## Administración de etiquetas de uso de datos en [!DNL Experience Platform] {#manage-labels}

Puede administrar etiquetas de uso de datos mediante [!DNL Experience Platform] API o la interfaz de usuario. Consulte las subsecciones siguientes para obtener más detalles sobre cada una.

### Uso de la interfaz de usuario

El espacio de trabajo **[!UICONTROL Directivas]** de la [!DNL Experience Platform] interfaz de usuario le permite realizar vistas y administrar las etiquetas principales y personalizadas de su organización. El espacio de trabajo permite aplicar etiquetas a conjuntos de datos y campos. **[!DNL Datasets]** For more information, refer to the [labels user guide](user-guide.md).

### Uso de API

El `/labels` punto final de la API [del servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) directivas le permite administrar mediante programación las etiquetas de uso de datos, incluida la creación de etiquetas personalizadas. Consulte la guía [de extremo de](../api/labels.md) etiquetas para obtener más información.

La API [del servicio](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) de dataset se utiliza para administrar etiquetas para conjuntos de datos y campos. Consulte la guía sobre la [administración de etiquetas](./dataset-api.md) de conjuntos de datos para obtener más información.

## Pasos siguientes

Este documento proporcionó una introducción a las etiquetas de uso de datos y su función dentro del marco de administración de datos. Consulte la documentación relacionada en esta guía para obtener más información sobre cómo administrar las etiquetas en [!DNL Experience Platform].