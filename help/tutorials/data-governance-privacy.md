---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriales sobre administración de datos y privacidad
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Tutoriales sobre administración de datos y privacidad

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo central del control de datos de la plataforma de experiencia de Adobe. Las funciones DULE permiten aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada una según las políticas de uso de datos relacionadas. Antes de comenzar con las etiquetas, consulte la información general [sobre el Gobierno de](../data-governance/home.md) datos para obtener una introducción más sólida al marco de trabajo DULE dentro de la plataforma.

Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario que le permiten coordinar las solicitudes de privacidad y cumplimiento de normas en varias soluciones. Para obtener más información, lea la información general [de](../privacy-service/home.md)Privacy Service.

## Añadir etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de los datos tan pronto como se incorporan a la plataforma de experiencia o tan pronto como los datos estén disponibles para su uso en la plataforma. Las etiquetas de uso de datos que se aplican en el nivel de conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) en un conjunto de datos, sin propagación. Para aprender a aplicar etiquetas de uso de datos a sus datos, visite la información general [de etiquetas de uso de](../data-governance/labels/overview.md)datos.

## Crear directivas de uso de datos

La API del servicio de directivas DULE le permite crear y administrar políticas DULE para determinar qué acciones de marketing se pueden realizar con datos que contengan determinadas etiquetas DULE. Para empezar, lea la descripción general [de las directivas de uso de](../data-governance/policies/overview.md)datos.

## Aplicar directivas de uso de datos

Una vez que haya creado las etiquetas de etiquetado y cumplimiento de uso de datos (DULE) para sus datos y haya creado políticas DULE para acciones de marketing con dichas etiquetas, puede utilizar la API de servicio de directivas DULE para evaluar si una acción de marketing realizada en un conjunto de datos o un grupo arbitrario de etiquetas DULE constituye una infracción de la política. A continuación, puede configurar sus propios protocolos internos para controlar las infracciones de política en función de la respuesta de la API. Para empezar, visite la descripción general [de la aplicación de](../data-governance/enforcement/overview.md)políticas.

## Aplicar la conformidad de uso de datos para un segmento de audiencia

Los segmentos que están habilitados para su uso en el Perfil del cliente en tiempo real contienen un ID de directiva de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre los conjuntos de datos que se deben incluir en el segmento, que a su vez contienen las etiquetas de uso de datos aplicables. Para ver los pasos específicos que abarcan la aplicación de la conformidad con el uso de datos para un segmento de audiencia, siga el tutorial de cumplimiento de la normativa de uso de [datos para segmentos](../segmentation/tutorials/governance.md).

## Introducción a Privacy Service

Privacy Service proporciona una API RESTful y una interfaz de usuario que le permiten administrar los datos personales de los sujetos de datos (clientes) en todas las aplicaciones de Adobe Experience Cloud. Privacy Service también proporciona un mecanismo central de auditoría y registro que le permite acceder al estado y los resultados de los trabajos que involucran aplicaciones de Experience Cloud. Para obtener instrucciones sobre cómo crear y supervisar trabajos de Privacy Service, siga los pasos que se proporcionan en la guía [para desarrolladores de](../privacy-service/api/getting-started.md) Privacy Service o en la guía [para usuarios de](../privacy-service/ui/overview.md)Privacy Service.