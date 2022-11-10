---
keywords: Experience Platform;inicio;temas populares;programación;DULE
solution: Experience Platform
title: Información general sobre las políticas de uso de datos
topic-legacy: policies
description: Para que las etiquetas de uso de datos admitan de forma eficaz el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 4%

---

# Información general sobre las políticas de uso de datos {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Restringir el uso de datos"
>abstract="El tipo de directiva de uso de datos evalúa las acciones de marketing específicas aplicadas a las etiquetas de control de datos para restringir el uso de datos para actividades de marketing."

Para que las etiquetas de uso de datos admitan de forma eficaz el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de [!DNL Experience Platform].

Hay dos tipos de políticas disponibles:

* **[!UICONTROL Política de control de datos]**: Restringir la activación de datos en función de la acción de marketing que se realice y las etiquetas de uso de datos que lleven los datos en cuestión.
* **[!UICONTROL Política de consentimiento]**: Filtre los perfiles que se pueden activar en [destinos](../../destinations/home.md) en función del consentimiento o las preferencias de sus clientes

>[!NOTE]
>
>Las políticas de uso de datos no deben confundirse con [directivas de control de acceso](../../access-control/abac/end-to-end-guide.md#policy), que determinan si determinados usuarios de Platform de su organización pueden acceder a ciertos campos de datos y se configuran mediante la variable [!UICONTROL Permisos] pestaña .

Este documento proporciona información general de alto nivel sobre las políticas de uso de datos y proporciona vínculos a documentación adicional para trabajar con políticas en la interfaz de usuario o la API.

## Acciones de marketing {#marketing-actions}

Las acciones de marketing (también denominadas casos de uso de marketing) en el contexto del marco de control de datos, son acciones que [!DNL Experience Platform] Los consumidores de datos pueden tomarlos, para lo cual su organización desea restringir el uso de datos. Como tal, una política de uso de datos se define de la siguiente manera:

1. Una acción de marketing específica
2. Condiciones en las que se restringe la realización de esa acción

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si hay una directiva que indica que no se pueden exportar tipos de datos específicos (como Información de identificación personal (PII)) y que intenta exportar un conjunto de datos que contiene una etiqueta &quot;I&quot; (datos de identidad), recibirá una respuesta de la [!DNL Policy Service] que indica que se ha infringido una directiva de uso de datos.

>[!NOTE]
>
>Las acciones de marketing por sí mismas no restringen el uso de los datos. Deben incluirse en las políticas de uso de datos habilitadas para que esas acciones se evalúen en caso de infracciones de políticas.

Cuando el uso de los datos se produce en el servicio de su organización, se deben indicar las acciones de marketing relevantes para que se puedan identificar todas las infracciones de políticas. A continuación, puede usar la variable [API del servicio de directivas](https://www.adobe.io/experience-platform-apis/references/policy-service/) para comprobar las infracciones de directiva en su integración.

>[!NOTE]
>
>Puede configurar casos de uso de marketing en destinos para automatizar la aplicación de políticas. Consulte la [documentación de destinos](../../destinations/home.md) para obtener más información sobre las opciones de configuración de su destino específico.

Para obtener una lista de [acciones de marketing definidas por el Adobe disponibles](#core-actions). También puede definir sus propias acciones de marketing personalizadas mediante la variable [!DNL Policy Service] API o [!DNL Experience Platform] interfaz de usuario. En la siguiente sección se proporciona más información sobre cómo trabajar con acciones y políticas de marketing.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Administración de políticas de uso de datos {#manage}

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden utilizar la variable [!DNL Policy Service] API o [!DNL Experience Platform] IU para administrar y evaluar políticas relacionadas con las acciones de marketing que se realizan en datos que contienen etiquetas de uso de datos. Puede crear y actualizar directivas, determinar el estado de una directiva y trabajar con acciones de marketing para evaluar si una acción específica infringe una política de uso de datos.

>[!IMPORTANT]
>
>De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Para obtener instrucciones paso a paso sobre cómo trabajar con acciones de marketing y políticas de uso de datos en la API, consulte el tutorial sobre [creación y evaluación de políticas de uso de datos](create.md). Para obtener más información, consulte las operaciones clave proporcionadas por la variable [!DNL Policy Service] API, consulte la [Guía para desarrolladores de Policy Service](../api/getting-started.md).

Para obtener información sobre cómo trabajar con acciones y políticas de marketing en la variable [!DNL Platform] La interfaz de usuario de puede consultar la [guía del usuario de la directiva de uso de datos](./user-guide.md).

## Pasos siguientes

Este documento ofrecía una introducción a las políticas de uso de datos dentro del marco de control de datos. Ahora puede seguir leyendo la documentación del proceso vinculada a esta guía para obtener más información sobre cómo trabajar con políticas en la API y la IU.

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
| Coincidencia de segmentos | Acción que utiliza datos para la coincidencia de segmentos de Adobe Experience Platform, lo que permite que dos o más usuarios de Platform intercambien datos de segmentos. Al habilitar las políticas que hacen referencia a esta acción, puede restringir los datos que se usan para la coincidencia de segmentos. Por ejemplo, si la política principal &quot;Restringir el uso compartido de datos&quot; está activada, cualquier dato con un [Etiqueta C11](../labels/reference.md#c11) no se puede usar para la coincidencia de segmentos. |
| Personalización de identidad única | Acción que requiere que una sola identidad se utilice con fines de personalización en lugar de vincular identidades de varias fuentes. |
