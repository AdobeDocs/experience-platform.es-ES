---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de API del servicio de directivas
topic-legacy: developer guide
description: La API del servicio de directivas permite a los desarrolladores administrar las etiquetas y políticas de uso de datos en Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# Guía de la API de [!DNL Policy Service]

La administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de uso de datos y el control del uso de datos para las acciones de marketing.

La variable [!DNL Policy Service] La API de proporciona varios puntos de conexión que le permiten administrar mediante programación las etiquetas y políticas de uso de datos, así como evaluar las acciones de marketing en caso de infracciones de políticas. Estos extremos se describen a continuación. Visite las guías de puntos de conexión individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [[!DNL Policy Service] Intercambio de API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etiquetas

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. Las prácticas recomendadas alientan el etiquetado de datos en cuanto se incorpora en [!DNL Experience Platform]o en cuanto los datos estén disponibles para su uso en [!DNL Platform]. Puede crear, ver, editar y eliminar etiquetas utilizando la variable `/labels` punto final. Para aprender a utilizar este extremo, visite la [guía de extremo de etiquetas](./labels.md).

## Acciones de marketing

Las acciones de marketing (también denominadas casos de uso de marketing), en el contexto del marco de control de datos, son acciones que [!DNL Experience Platform] Los consumidores de datos pueden tomarlos, para lo cual su organización desea restringir el uso de datos. Para obtener información detallada sobre cómo trabajar con acciones de marketing, consulte la [guía de extremo de acciones de marketing](./marketing-actions.md).

## Políticas

Las políticas de control de datos son reglas que describen los tipos de acciones de marketing que puede realizar o de las que se le restringe el uso de datos dentro de [!DNL Experience Platform].

>[!NOTE]
>
>Las políticas de control de datos no deben confundirse con las políticas de control de acceso, que determinan los atributos de datos específicos a los que pueden acceder ciertos usuarios de Platform de su organización. Consulte la guía de [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener más información.

Una política de control de datos se define de la siguiente manera:

1. Una acción de marketing específica
1. Etiquetas de uso de datos con las que se restringe la acción

Para obtener información sobre cómo administrar directivas en la API, consulte la [guía de extremo de directivas](./policies.md)

## Evaluación

Una vez aplicadas las etiquetas de uso de datos [!DNL Platform] Los conjuntos de datos de y las políticas de uso de datos se han definido para acciones de marketing con esas etiquetas, las capacidades de control de datos permiten aplicar esas políticas y evitar operaciones de datos que constituyan violaciones de políticas.

La variable [!DNL Policy Service] La API proporciona extremos que le permiten probar acciones de marketing con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se produce alguna violación de la política. En función de la respuesta de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente la política de uso de datos. Consulte la [guía de extremos de evaluación](./evaluation.md) para obtener más información.

## Pasos siguientes

Para empezar a realizar llamadas con [!DNL Policy Service] API, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos. Para trabajar con etiquetas y directivas mediante el uso de [!DNL Experience Platform] Interfaz de usuario, consulte [guía del usuario de etiquetas](../labels/user-guide.md) y [guía del usuario sobre directivas](../policies/user-guide.md), respectivamente.
