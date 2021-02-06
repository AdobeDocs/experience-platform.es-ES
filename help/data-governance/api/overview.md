---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de API de servicio de directivas
topic: developer guide
description: La API de servicio de directivas permite a los desarrolladores administrar las etiquetas y políticas de uso de datos en Experience Platform. Siga esta guía para aprender a realizar operaciones clave mediante la API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# [!DNL Policy Service] Guía de API

Adobe Experience Platform [!DNL Data Governance] le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en diversos niveles, incluso la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de uso de datos y el control del uso de datos para acciones de mercadotecnia.

La API [!DNL Policy Service] proporciona varios extremos que le permiten administrar mediante programación las directivas y etiquetas de uso de datos, como así también evaluar las acciones de mercadotecnia en caso de infracciones de políticas. Estos extremos se describen a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados requeridos, leer llamadas de API de muestra y mucho más.

Para realizar la vista de todos los extremos y las operaciones de CRUD disponibles, visite el [[!DNL Policy Service] swagger de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etiquetas

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. Las prácticas recomendadas alientan el etiquetado de datos tan pronto como se ingesta en [!DNL Experience Platform] o tan pronto como los datos estén disponibles para su uso en [!DNL Platform]. Puede crear, vista, editar y eliminar etiquetas mediante el extremo `/labels`. Para aprender a usar este extremo, visite la [guía de extremo de etiquetas](./labels.md).

## Acciones de mercadotecnia

Las acciones de mercadotecnia (también denominadas casos de uso de mercadotecnia), en el contexto del [!DNL Data Governance] marco de trabajo, son acciones que un [!DNL Experience Platform] consumidor de datos puede realizar, para las cuales su organización desea restringir el uso de datos. Para obtener información detallada sobre cómo trabajar con acciones de mercadotecnia, consulte la [guía del extremo de acciones de mercadotecnia](./marketing-actions.md).

## Políticas

Las políticas de uso de datos son reglas que describen los tipos de acciones de mercadotecnia que se le permite o se le restringe la realización de datos dentro de [!DNL Experience Platform]. Una directiva se define de la siguiente manera:

1. Una acción de mercadotecnia específica
1. Las etiquetas de uso de datos con las que se restringe la acción

Para obtener información sobre cómo administrar las políticas en la API, consulte la [guía de extremo de directivas](./policies.md)

## Evaluación

Una vez que las etiquetas de uso de datos se han aplicado a [!DNL Platform] datasets y se han definido políticas de uso de datos para las acciones de mercadotecnia en relación con dichas etiquetas, las capacidades de administración de datos le permiten aplicar esas políticas y evitar operaciones de datos que constituyan violaciones de políticas.

La API [!DNL Policy Service] proporciona extremos que le permiten probar acciones de mercadotecnia con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para verificar si se producen violaciones de políticas. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la política de uso de datos. Consulte la [guía de extremos de evaluación](./evaluation.md) para obtener más información.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Policy Service], lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos. Para trabajar con etiquetas y políticas mediante la [!DNL Experience Platform] interfaz de usuario, consulte la [guía del usuario de etiquetas](../labels/user-guide.md) y la [guía del usuario de directivas](../policies/user-guide.md), respectivamente.