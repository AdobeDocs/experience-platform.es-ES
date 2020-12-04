---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de API de servicios de directivas
topic: developer guide
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# [!DNL Policy Service] Guía para desarrolladores de API

Adobe Experience Platform [!DNL Data Governance] le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] varios niveles, incluyendo la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de uso de datos y el control del uso de datos para acciones de mercadotecnia.

La [!DNL Policy Service] API proporciona varios extremos que le permiten administrar mediante programación las directivas y etiquetas de uso de datos, así como evaluar las acciones de marketing para infracciones de políticas. Estos extremos se describen a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la guía [de](./getting-started.md) introducción para obtener información importante sobre los encabezados requeridos, la lectura de llamadas de API de muestra y mucho más.

Para vista de todos los extremos disponibles y las operaciones de CRUD, visite el [[!DNL Policy Service] intercambiador](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)de API.

## Etiquetas

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de los datos tan pronto como se ingieran [!DNL Experience Platform]o tan pronto como los datos estén disponibles para su uso en [!DNL Platform]. Puede crear, vista, editar y eliminar etiquetas mediante el `/labels` punto final. Para aprender a utilizar este extremo, visite la guía de extremo de [etiquetas](./labels.md).

## Acciones de mercadotecnia

Las acciones de mercadotecnia (también denominadas casos de uso de mercadotecnia), en el contexto del [!DNL Data Governance] marco de trabajo, son acciones que un consumidor de [!DNL Experience Platform] datos puede realizar, para las que su organización desea restringir el uso de datos. Para obtener información detallada sobre cómo trabajar con acciones de marketing, consulte la guía de objetivos de acciones de [marketing](./marketing-actions.md).

## Políticas

Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se restringe el rendimiento de los datos dentro de [!DNL Experience Platform]. Una directiva se define de la siguiente manera:

1. Una acción de mercadotecnia específica
1. Las etiquetas de uso de datos con las que se restringe la acción

Para obtener información sobre cómo administrar las directivas en la API, consulte la guía de extremo de [directivas](./policies.md)

## Evaluación

Una vez que se han aplicado las etiquetas de uso de datos a los conjuntos de datos y se han definido las políticas de uso de datos para las acciones de marketing en relación con dichas etiquetas, las capacidades de administración de datos le permiten aplicar dichas directivas y evitar operaciones de datos que constituyan violaciones de políticas. [!DNL Platform]

La [!DNL Policy Service] API proporciona puntos finales que le permiten probar acciones de mercadotecnia con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se producen violaciones de políticas. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la política de uso de datos. See the [evaluation endpoints guide](./evaluation.md) for more information.

## Pasos siguientes

Para empezar a realizar llamadas mediante la [!DNL Policy Service] API, lea la guía [de](./getting-started.md) introducción y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos. Para trabajar con etiquetas y políticas mediante la [!DNL Experience Platform] interfaz de usuario, consulte la guía [del usuario de](../labels/user-guide.md) etiquetas y la guía [del usuario de](../policies/user-guide.md)políticas, respectivamente.