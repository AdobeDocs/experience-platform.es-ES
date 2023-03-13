---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de API del servicio de directivas
description: La API del servicio de directivas permite a los desarrolladores administrar las etiquetas y directivas de uso de datos en Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# Guía de la API de [!DNL Policy Service]

Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado de uso de datos, las políticas de uso de datos y el control del uso de datos para acciones de marketing.

El [!DNL Policy Service] La API proporciona varios extremos que le permiten administrar mediante programación las etiquetas y directivas de uso de datos, así como evaluar las acciones de marketing por infracciones de directivas. Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [[!DNL Policy Service] Swagger de API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etiquetas

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas recomiendan etiquetar los datos en cuanto se incorporen en [!DNL Experience Platform]o en cuanto los datos estén disponibles para su uso en [!DNL Platform]. Puede crear, ver, editar y eliminar etiquetas utilizando `/labels` punto final. Para aprender a utilizar este punto de conexión, visite la [guía de extremo de etiquetas](./labels.md).

## Acciones de marketing

Las acciones de marketing (también denominadas casos de uso de marketing), en el contexto del marco de trabajo de gobernanza de datos, son acciones que pueden [!DNL Experience Platform] que el consumidor de datos puede tomar, para lo cual su organización desea restringir el uso de datos. Para obtener información detallada sobre cómo trabajar con acciones de marketing, consulte la [guía de extremo de acciones de marketing](./marketing-actions.md).

## Políticas

Las políticas de gobernanza de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de [!DNL Experience Platform].

>[!NOTE]
>
>Las políticas de gobernanza de datos no se deben confundir con las políticas de control de acceso, que determinan los atributos de datos específicos a los que pueden acceder determinados usuarios de Platform en su organización. Consulte la guía de [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener más información.

Una política de gobernanza de datos se define de la siguiente manera:

1. Una acción de marketing específica
1. Las etiquetas de uso de datos contra las que está restringida esa acción

Para obtener información sobre cómo administrar directivas en la API, consulte la [guía de extremo de directivas](./policies.md)

## Evaluación

Una vez aplicadas las etiquetas de uso de datos a [!DNL Platform] Se han definido conjuntos de datos y políticas de uso de datos para acciones de marketing contra esas etiquetas. Las capacidades de control de datos le permiten aplicar esas políticas y evitar operaciones de datos que constituyan violaciones de políticas.

El [!DNL Policy Service] La API proporciona puntos finales que le permiten probar acciones de marketing contra conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se produce alguna infracción de directiva. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la política de uso de datos. Consulte la [guía de extremos de evaluación](./evaluation.md) para obtener más información.

## Pasos siguientes

Para empezar a realizar llamadas utilizando [!DNL Policy Service] API, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos. Para trabajar con etiquetas y directivas utilizando [!DNL Experience Platform] Interfaz de usuario, consulte la [guía del usuario de etiquetas](../labels/user-guide.md) y [guía del usuario de directivas](../policies/user-guide.md), respectivamente.
