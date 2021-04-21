---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de API del servicio de directivas
topic-legacy: developer guide
description: La API del servicio de directivas permite a los desarrolladores administrar las etiquetas y políticas de uso de datos en Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# [!DNL Policy Service] Guía de API

Adobe Experience Platform [!DNL Data Governance] le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de uso de los datos y el control del uso de los datos para las acciones de marketing.

La API [!DNL Policy Service] proporciona varios puntos finales que le permiten administrar mediante programación las etiquetas y políticas de uso de datos, así como evaluar las acciones de marketing en caso de infracciones de políticas. Estos extremos se describen a continuación. Visite las guías de puntos finales individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y todas las operaciones de CRUD, visite el [[!DNL Policy Service] Intercambio de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etiquetas

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. Las prácticas recomendadas recomiendan el etiquetado de datos tan pronto como se incorporan a [!DNL Experience Platform] o tan pronto como los datos estén disponibles para su uso en [!DNL Platform]. Puede crear, ver, editar y eliminar etiquetas utilizando el extremo `/labels` . Para aprender a utilizar este extremo, visite la [guía de extremo de etiquetas](./labels.md).

## Acciones de marketing

Las acciones de marketing (también denominadas casos de uso de marketing), en el contexto del marco [!DNL Data Governance], son acciones que puede realizar un [!DNL Experience Platform] consumidor de datos, para las que su organización desea restringir el uso de datos. Para obtener información detallada sobre cómo trabajar con acciones de marketing, consulte la [guía de extremo de acciones de marketing](./marketing-actions.md).

## Políticas

Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se le restringe, realizar en datos dentro de [!DNL Experience Platform]. Una política se define de la siguiente manera:

1. Una acción de marketing específica
1. Etiquetas de uso de datos con las que se restringe la acción

Para obtener información sobre cómo administrar directivas en la API, consulte la [guía de extremo de directivas](./policies.md)

## Evaluación

Una vez que las etiquetas de uso de datos se han aplicado a los conjuntos de datos [!DNL Platform] y se han definido políticas de uso de datos para acciones de marketing frente a esas etiquetas, las funcionalidades de control de datos permiten aplicar esas políticas y evitar operaciones de datos que constituyan infracciones de políticas.

La API [!DNL Policy Service] proporciona extremos que le permiten probar acciones de marketing con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se produce alguna infracción de directiva. En función de la respuesta de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente la política de uso de datos. Consulte la [guía de extremos de evaluación](./evaluation.md) para obtener más información.

## Pasos siguientes

Para empezar a realizar llamadas con la API [!DNL Policy Service], lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos. Para trabajar con etiquetas y políticas usando la interfaz de usuario [!DNL Experience Platform], consulte la [guía del usuario de etiquetas](../labels/user-guide.md) y la [guía del usuario de directivas](../policies/user-guide.md), respectivamente.
