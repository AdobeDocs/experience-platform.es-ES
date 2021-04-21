---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Tutoriales sobre administración de datos y privacidad
topic-legacy: tutorial
type: Tutorial
description: Este documento proporciona información general sobre los distintos tutoriales disponibles relacionados con la administración de datos de Adobe Experience Platform y Adobe Experience Platform Privacy Service.
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# [!DNL Data Governance] y  [!DNL Privacy] Tutorials

La administración de datos de Adobe Experience Platform le permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificar cada uno según las políticas de uso de datos relacionadas y evaluar las infracciones de políticas cuando se realizan ciertas acciones en dichos conjuntos de datos o campos. Antes de comenzar con los tutoriales enumerados en este documento, consulte la [[!DNL Data Governance] descripción general](../data-governance/home.md) para obtener una introducción más sólida al marco.

Adobe Experience Platform [!DNL Privacy Service] proporciona una API y una interfaz de usuario de RESTful que le permiten coordinar las solicitudes de privacidad y cumplimiento de normas entre varias soluciones. Para obtener más información, comience por leer la [información general del Privacy Service](../privacy-service/home.md).

## Añadir etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. Las prácticas recomendadas recomiendan el etiquetado de datos tan pronto como se incorporan a [!DNL Experience Platform] o tan pronto como los datos estén disponibles para su uso en [!DNL Platform]. Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación. Para aprender a aplicar etiquetas de uso de datos a sus datos, visite la [información general sobre etiquetas de uso de datos](../data-governance/labels/overview.md).

## Crear políticas de uso de datos

La API [!DNL Policy Service] le permite crear y administrar políticas de uso de datos para determinar qué acciones de marketing se pueden realizar con datos que contengan ciertas etiquetas de uso. Para empezar, lea la [información general sobre las directivas de uso de datos](../data-governance/policies/overview.md).

## Aplicar políticas de uso de datos

Una vez que haya agregado etiquetas de uso para sus datos y haya creado políticas para acciones de marketing con esas etiquetas, puede utilizar [!DNL Policy Service API] para evaluar si una acción de marketing constituye una infracción de directiva cuando se realiza en un conjunto de datos o en un grupo arbitrario de etiquetas de uso. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de API. Para empezar, visite la [descripción general del cumplimiento de políticas](../data-governance/enforcement/overview.md).

## Aplicar el cumplimiento de uso de datos a un segmento de audiencia

Los segmentos que están habilitados para su uso en [!DNL Real-time Customer Profile] contienen un ID de política de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre qué conjuntos de datos se incluyen en el segmento, que a su vez contienen cualquier etiqueta de uso de datos aplicable. Para ver los pasos específicos que abarcan la aplicación del cumplimiento de las normas de uso de datos para un segmento de audiencia, siga el [tutorial de cumplimiento del uso de datos para segmentos](../segmentation/tutorials/governance.md).

## Introducción a [!DNL Privacy Service]

[!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario que le permiten administrar los datos personales de sus interesados (clientes) en todas las aplicaciones de Adobe Experience Cloud. [!DNL Privacy Service] también proporciona un mecanismo central de auditoría y registro que le permite acceder al estado y los resultados de los trabajos que implican  [!DNL Experience Cloud] aplicaciones. Para obtener instrucciones sobre cómo crear y monitorizar trabajos [!DNL Privacy Service], siga los pasos que se proporcionan en la [guía para desarrolladores de Privacy Service](../privacy-service/api/getting-started.md) o en la [guía de usuario de Privacy Service](../privacy-service/ui/overview.md).
