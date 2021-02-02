---
keywords: Experience Platform;inicio;temas populares;programar;DULE
solution: Experience Platform
title: Información general sobre las directivas de uso de datos
topic: policies
description: Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se restringe el rendimiento de los datos dentro de Experience Platform.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# Información general sobre las directivas de uso de datos

Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de mercadotecnia que se le permite o se le restringe la realización de datos dentro de [!DNL Experience Platform].

Este documento proporciona información general de alto nivel sobre las políticas de uso de datos y proporciona vínculos a documentación adicional para trabajar con políticas en la interfaz de usuario o la API.

## Acciones de mercadotecnia {#marketing-actions}

Las acciones de mercadotecnia (también denominadas casos de uso de mercadotecnia) en el contexto del marco de administración de datos, son acciones que puede realizar un [!DNL Experience Platform] consumidor de datos, para las que su organización desea restringir el uso de datos. Como tal, una directiva de uso de datos se define de la siguiente manera:

1. Una acción de mercadotecnia específica
2. Las etiquetas de uso de datos con las que se restringe la acción

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que indica que no se pueden exportar tipos específicos de datos (como Información de identificación personal (PII)) e intenta exportar un conjunto de datos que contiene una etiqueta &quot;I&quot; (Datos de identidad), recibirá una respuesta de [!DNL Policy Service] que le informará de que se ha violado una política de uso de datos.

>[!NOTE]
>
>Las acciones de marketing por sí solas no restringen el uso de datos. Deben incluirse en las directivas de uso de datos habilitadas para que esas acciones se evalúen en caso de infracciones de políticas.

Cuando el uso de datos se produce en el servicio de su organización, se deben indicar las acciones de mercadotecnia relevantes para que se puedan identificar las infracciones de política. A continuación, puede utilizar la [API de servicio de directivas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) para comprobar si hay infracciones de políticas en la integración.

>[!NOTE]
>
>Si utiliza [!DNL Real-time Customer Data Platform], puede configurar casos de uso de mercadotecnia en destinos para automatizar la aplicación de políticas. Consulte el documento sobre [Administración de datos en tiempo real CDP](../../rtcdp/privacy/data-governance-overview.md) para obtener más información.

Consulte el apéndice de este documento para ver una lista de [acciones de mercadotecnia definidas por Adobe](#core-actions) disponibles. También puede definir sus propias acciones de mercadotecnia personalizadas mediante la API [!DNL Policy Service] o la interfaz de usuario [!DNL Experience Platform ]. En la siguiente sección se proporciona más información sobre cómo trabajar con las acciones y políticas de marketing.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Administración de políticas de uso de datos {#manage}

Una vez que se han aplicado las etiquetas de uso de datos, los administradores de datos pueden utilizar la API [!DNL Policy Service] o la interfaz de usuario [!DNL Experience Platform] para administrar y evaluar las políticas relacionadas con las acciones de mercadotecnia que se realizan en datos que contienen etiquetas de uso de datos. Puede crear y actualizar políticas, determinar el estado de una política y trabajar con acciones de marketing para evaluar si una acción específica infringe una política de uso de datos.

>[!IMPORTANT]
>
>Todas las directivas de uso de datos (incluidas las directivas principales proporcionadas por Adobe) están deshabilitadas de forma predeterminada. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Para obtener instrucciones paso a paso sobre cómo trabajar con acciones de marketing y políticas de uso de datos en la API, consulte el tutorial sobre [creación y evaluación de políticas de uso de datos](create.md). Para obtener más información sobre las operaciones clave proporcionadas por la API [!DNL Policy Service], consulte la [Guía para desarrolladores de Policy Service](../api/getting-started.md).

Para obtener información sobre cómo trabajar con las acciones y políticas de mercadotecnia en la [!DNL Platform] interfaz de usuario, consulte la [guía del usuario de la directiva de uso de datos](./user-guide.md).

## Pasos siguientes

Este documento proporcionó una introducción a las políticas de uso de datos dentro del marco [!DNL Data Governance]. Ahora puede seguir leyendo la documentación del proceso a la que se ha vinculado a través de esta guía para obtener más información sobre cómo trabajar con políticas en la API y la interfaz de usuario.

## Apéndice

La siguiente sección proporciona información adicional sobre las políticas de uso de datos.

### Acciones de mercadotecnia definidas por Adobe {#core-actions}

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
