---
keywords: Experience Platform;home;popular topics;dule;DULE
solution: Experience Platform
title: Información general sobre las directivas de uso de datos
topic: policies
description: Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se restringe el rendimiento de los datos dentro de Experience Platform.
translation-type: tm+mt
source-git-commit: 259c26a9d3b6ef397acd552e255f68ecb25b2dd1
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---


# Información general sobre las directivas de uso de datos

Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se restringe el rendimiento de los datos dentro de [!DNL Experience Platform].

Este documento proporciona información general de alto nivel sobre las políticas de uso de datos y proporciona vínculos a documentación adicional para trabajar con políticas en la interfaz de usuario o la API.

## Acciones de mercadotecnia {#marketing-actions}

Las acciones de mercadotecnia (también denominadas casos de uso de mercadotecnia) en el contexto del marco de administración de datos, son acciones que un consumidor de [!DNL Experience Platform] datos puede realizar, para las que su organización desea restringir el uso de datos. Como tal, una directiva de uso de datos se define de la siguiente manera:

1. Una acción de mercadotecnia específica
2. Las etiquetas de uso de datos con las que se restringe la acción

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que indica que los tipos de datos específicos (como Información de identificación personal (PII)) no se pueden exportar e intenta exportar un conjunto de datos que contiene una etiqueta &quot;I&quot; (Datos de identidad), recibirá una respuesta del usuario que le [!DNL Policy Service] informará de que se ha violado una política de uso de datos.

>[!NOTE]
>
>Las acciones de marketing por sí solas no restringen el uso de datos. Deben incluirse en las directivas de uso de datos habilitadas para que esas acciones se evalúen en caso de infracciones de políticas.

Cuando el uso de datos se produce en el servicio de su organización, se deben indicar las acciones de mercadotecnia relevantes para que se puedan identificar las infracciones de política. A continuación, puede utilizar la API [de servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) directivas para comprobar si hay infracciones de políticas en la integración.

>[!NOTE]
>
>Si utiliza [!DNL Real-time Customer Data Platform], puede configurar casos de uso de mercadotecnia en destinos para automatizar la aplicación de políticas. Consulte el documento sobre Administración de [datos en tiempo real CDP](../../rtcdp/privacy/data-governance-overview.md) para obtener más información.

Consulte el apéndice del presente documento para ver una lista de las acciones [de marketing definidas por el Adobe](#core-actions)disponibles. También puede definir sus propias acciones de marketing personalizadas mediante la [!DNL Policy Service] API o la interfaz de [!DNL Experience Platform ]usuario. En la siguiente sección se proporciona más información sobre cómo trabajar con las acciones y políticas de marketing.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Administración de directivas de uso de datos {#manage}

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden utilizar la [!DNL Policy Service] [!DNL Experience Platform] API o la interfaz de usuario para administrar y evaluar las políticas relacionadas con las acciones de marketing que se están realizando en datos que contienen etiquetas de uso de datos. Puede crear y actualizar políticas, determinar el estado de una política y trabajar con acciones de marketing para evaluar si una acción específica infringe una política de uso de datos.

>[!IMPORTANT]
>
>Todas las directivas de uso de datos (incluidas las directivas principales proporcionadas por Adobe) están deshabilitadas de forma predeterminada. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Para obtener instrucciones paso a paso sobre cómo trabajar con acciones de marketing y políticas de uso de datos en la API, consulte el tutorial sobre la [creación y evaluación de políticas](create.md)de uso de datos. Para obtener más información sobre las operaciones clave proporcionadas por la [!DNL Policy Service] API, consulte la guía [para desarrolladores de](../api/getting-started.md)Policy Service.

Para obtener información sobre cómo trabajar con las acciones y políticas de marketing en la interfaz de usuario, consulte la guía [!DNL Platform] del usuario de la directiva de uso de [](./user-guide.md)datos.

## Pasos siguientes

Este documento proporcionó una introducción a las políticas de uso de datos dentro del [!DNL Data Governance] marco. Ahora puede seguir leyendo la documentación del proceso a la que se ha vinculado a través de esta guía para obtener más información sobre cómo trabajar con políticas en la API y la interfaz de usuario.

## Apéndice

La siguiente sección proporciona información adicional sobre las políticas de uso de datos.

### Acciones de mercadotecnia definidas por Adobes {#core-actions}

En la tabla siguiente se describen las principales acciones de mercadotecnia que el Adobe proporciona de forma predeterminada.

>[!NOTE]
>
>Las acciones de mercadotecnia principales deben considerarse como un punto de partida para ayudarle a identificar qué políticas de uso crear y verificar las infracciones. Las definiciones y cómo se interpretan dependen de las necesidades y políticas de su organización.

| Acción de mercadotecnia | Descripción |
| --- | --- |
| Analytics  | Acción que utiliza datos para fines analíticos, como medir, analizar y sistemas de informes sobre el uso que los clientes hacen de los sitios o aplicaciones de su organización. |
| Combinar con PII | Acción que combina cualquier información de identificación personal (PII) con datos anónimos. Los contratos para datos provenientes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de esos datos con datos directamente identificables. |
| Objetivos entre sitios | Acción que utiliza datos para la segmentación de anuncios entre sitios. La combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas, se denomina datos entre sitios. Los datos entre sitios generalmente se recopilan y procesan para hacer inferencias sobre los intereses de los usuarios. |
| Ciencia de datos | Acción que utiliza datos para flujos de trabajo de ciencia de datos. Algunos contratos incluyen prohibiciones explícitas del uso de datos para la ciencia de datos. A veces se expresan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado. |
| Objetivo de correo electrónico | Acción que utiliza datos en campañas de segmentación de correo electrónico. |
| Exportar a terceros | Acción que exporta datos a procesadores y entidades que no tienen relaciones directas con clientes. Muchos proveedores de datos tienen términos en los contratos que prohíben la exportación de datos desde donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales suelen restringir la transferencia de datos que recibe de ellos. |
| Publicidad en el sitio | Acción que utiliza datos para publicidades en el sitio, incluida la selección y el envío de publicidades en los sitios web o aplicaciones de la organización, o para medir el envío y la efectividad de dichas publicidades. |
| Personalización en el sitio | Acción que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer inferencias sobre los intereses de los usuarios y se utiliza para seleccionar qué contenido o publicidades se ofrecen en base a esas inferencias. |
| Personalización de identidad única | Acción que requiere que una sola identidad se utilice con fines de personalización en lugar de vincular identidades de múltiples fuentes. |
