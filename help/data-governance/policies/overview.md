---
keywords: Experience Platform;inicio;temas populares;programación;DULE
solution: Experience Platform
title: Información general sobre las políticas de uso de datos
topic-legacy: policies
description: Para que las etiquetas de uso de datos admitan de forma eficaz el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# Información general sobre las políticas de uso de datos

Para que las etiquetas de uso de datos admitan de forma eficaz el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite o se le restringe, realizar en datos dentro de [!DNL Experience Platform].

Este documento proporciona información general de alto nivel sobre las políticas de uso de datos y proporciona vínculos a documentación adicional para trabajar con políticas en la interfaz de usuario o la API.

## Acciones de marketing {#marketing-actions}

Las acciones de marketing (también denominadas casos de uso de marketing) en el contexto del marco de control de datos, son acciones que puede realizar un [!DNL Experience Platform] consumidor de datos, para las que su organización desea restringir el uso de datos. Como tal, una política de uso de datos se define de la siguiente manera:

1. Una acción de marketing específica
2. Etiquetas de uso de datos con las que se restringe la acción

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si hay una política que indica que no se pueden exportar tipos de datos específicos (como Información de identificación personal (PII)) y que intenta exportar un conjunto de datos que contiene una etiqueta &quot;I&quot; (datos de identidad), recibirá una respuesta de [!DNL Policy Service] que le indicará que se ha violado una política de uso de datos.

>[!NOTE]
>
>Las acciones de marketing por sí mismas no restringen el uso de los datos. Deben incluirse en las políticas de uso de datos habilitadas para que esas acciones se evalúen en caso de infracciones de políticas.

Cuando el uso de los datos se produce en el servicio de su organización, se deben indicar las acciones de marketing relevantes para que se puedan identificar todas las infracciones de políticas. A continuación, puede utilizar la [API del servicio de directivas](https://www.adobe.io/experience-platform-apis/references/policy-service/) para comprobar si hay infracciones de directivas en la integración.

>[!NOTE]
>
>Si utiliza [!DNL Real-time Customer Data Platform], puede configurar casos de uso de marketing en destinos para automatizar la aplicación de políticas. Consulte el documento sobre [Control de datos en CDP en tiempo real](../../rtcdp/privacy/data-governance-overview.md) para obtener más información.

Consulte el apéndice de este documento para obtener una lista de las [acciones de marketing definidas por el Adobe](#core-actions) disponibles. También puede definir sus propias acciones de marketing personalizadas mediante la API [!DNL Policy Service] o la interfaz de usuario [!DNL Experience Platform ]. En la siguiente sección se proporciona más información sobre cómo trabajar con acciones y políticas de marketing.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Administración de políticas de uso de datos {#manage}

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden utilizar la API [!DNL Policy Service] o la [!DNL Experience Platform] IU para administrar y evaluar las políticas relacionadas con las acciones de marketing que se realizan en los datos que contienen etiquetas de uso de datos. Puede crear y actualizar directivas, determinar el estado de una directiva y trabajar con acciones de marketing para evaluar si una acción específica infringe una política de uso de datos.

>[!IMPORTANT]
>
>De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Para obtener instrucciones paso a paso sobre cómo trabajar con acciones de marketing y políticas de uso de datos en la API, consulte el tutorial sobre [creación y evaluación de políticas de uso de datos](create.md). Para obtener más información sobre las operaciones clave proporcionadas por la API [!DNL Policy Service], consulte la [Guía para desarrolladores del servicio de políticas](../api/getting-started.md).

Para obtener información sobre cómo trabajar con acciones y políticas de marketing en la interfaz de usuario de [!DNL Platform], consulte la [guía del usuario de directivas de uso de datos](./user-guide.md).

## Pasos siguientes

Este documento proporciona una introducción a las políticas de uso de datos dentro del marco [!DNL Data Governance]. Ahora puede seguir leyendo la documentación del proceso vinculada a esta guía para obtener más información sobre cómo trabajar con políticas en la API y la IU.

## Apéndice

La siguiente sección proporciona información adicional sobre las políticas de uso de datos.

### Acciones de marketing definidas por Adobe {#core-actions}

En la tabla siguiente se describen las principales acciones de marketing que el Adobe proporciona de forma predeterminada.

>[!NOTE]
>
>Las acciones de marketing principales deben verse como un punto de partida para ayudarle a identificar qué políticas de uso crear y comprobar las infracciones. Las definiciones y cómo se interpretan dependen de las necesidades y políticas de la organización.

| Acción de marketing | Descripción |
| --- | --- |
| Analytics  | Acción que utiliza datos para fines analíticos, como medición, análisis e informes sobre el uso que hacen los clientes de los sitios o aplicaciones de su organización. |
| Combinación con datos directamente identificables | Acción que combina cualquier información de identificación personal (PII) con datos anónimos. Los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de dichos datos con datos directamente identificables. |
| Segmentación entre sitios | Acción que utiliza datos para la segmentación de anuncios entre sitios. La combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio, se denomina datos entre sitios. Los datos entre sitios suelen recopilarse y procesarse para hacer inferencias sobre los intereses de los usuarios. |
| Ciencia de datos | Acción que utiliza datos para flujos de trabajo de ciencia de datos. Algunos contratos incluyen prohibiciones explícitas sobre el uso de datos para la ciencia de datos. A veces se expresan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado. |
| Targeting de correo electrónico | Acción que utiliza datos en campañas de segmentación de correo electrónico. |
| Exportar a terceros | Acción que exporta datos a procesadores y entidades que no tienen relaciones directas con clientes. Muchos proveedores de datos tienen cláusulas en los contratos que prohíben la exportación de datos desde donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales a menudo restringen la transferencia de datos que recibe de ellos. |
| Publicidad en el sitio | Acción que usa datos para anuncios en el sitio, incluida la selección y entrega de anuncios en los sitios web o aplicaciones de su organización, o para medir la entrega y efectividad de dichos anuncios. |
| Personalización en el sitio | Acción que utiliza datos para la personalización de contenido en el sitio. La personalización del sitio es cualquier dato que se utiliza para hacer inferencias sobre los intereses de los usuarios y se utiliza para seleccionar qué contenido o anuncios se proporcionan en función de esas inferencias. |
| Coincidencia de segmentos | Acción que utiliza datos para la coincidencia de segmentos de Adobe Experience Platform, lo que permite que dos o más usuarios de Platform intercambien datos de segmentos. Al habilitar las políticas que hacen referencia a esta acción, puede restringir los datos que se usan para la coincidencia de segmentos. Por ejemplo, si la política principal &quot;Restringir el uso compartido de datos&quot; está habilitada, los datos con una etiqueta [C11](../labels/reference.md#c11) no se pueden usar para la coincidencia de segmentos. |
| Personalización de identidad única | Acción que requiere que una sola identidad se utilice con fines de personalización en lugar de vincular identidades de varias fuentes. |
