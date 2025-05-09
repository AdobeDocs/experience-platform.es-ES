---
keywords: Experience Platform;inicio;temas populares;dule;DULE
solution: Experience Platform
title: Información general sobre políticas de uso de datos
description: Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de Adobe Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 17%

---

# Información general sobre las políticas de uso de datos {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Restringir el uso de datos"
>abstract="El tipo de directiva de uso de datos evalúa las acciones de marketing específicas aplicadas a las etiquetas de gobernanza de datos para restringir el uso de datos para actividades de marketing."

Para que las etiquetas de uso de datos respalden con eficacia el cumplimiento, deben implementarse políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos dentro de [!DNL Experience Platform].

Hay dos tipos de directivas disponibles:

* **[!UICONTROL Política de control de datos]**: Restrinja la activación de datos en función de la acción de marketing que se esté realizando y de las etiquetas de uso de datos que lleven los datos en cuestión.
* **[!UICONTROL Política de consentimiento]**: filtre los perfiles que se pueden activar a [destinos](../../destinations/home.md) según las preferencias o el consentimiento de sus clientes

>[!NOTE]
>
>Las políticas de uso de datos no se deben confundir con las [políticas de control de acceso](../../access-control/abac/end-to-end-guide.md#policy), que determinan si ciertos usuarios de Experience Platform de su organización pueden acceder a ciertos campos de datos y se configuran a través de la pestaña [!UICONTROL Permisos].

Este documento proporciona información general de alto nivel sobre las políticas de uso de datos y proporciona vínculos a documentación adicional para trabajar con políticas en la interfaz de usuario o la API.

## Acciones de marketing {#marketing-actions}

Las acciones de marketing (también denominadas casos de uso de marketing) en el contexto del marco de trabajo de control de datos, son acciones que puede realizar un consumidor de datos de [!DNL Experience Platform] y para las cuales su organización desea restringir el uso de datos. Como tal, una política de uso de datos se define de la siguiente manera:

1. Una acción de marketing específica
2. Condiciones en las que se restringe la realización de esa acción

Un ejemplo de acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una directiva que indica que no se pueden exportar tipos específicos de datos (como Información de identificación personal (PII)) y trata de exportar un conjunto de datos que contiene una etiqueta &quot;I&quot; (Datos de identidad), recibirá una respuesta de [!DNL Policy Service] que le informará de que se ha infringido una directiva de uso de datos.

>[!NOTE]
>
>Las acciones de marketing por sí mismas no restringen el uso de datos. Deben incluirse en las políticas de uso de datos habilitadas para que esas acciones se evalúen en busca de violaciones de políticas.

Cuando el uso de datos se produce en el servicio de su organización, se deben indicar las acciones de marketing relevantes para que se pueda identificar cualquier infracción de política. A continuación, puede usar la [API del servicio de directivas](https://www.adobe.io/experience-platform-apis/references/policy-service/) para comprobar si hay violaciones de directivas en su integración.

>[!NOTE]
>
>Puede configurar casos de uso de marketing en destinos para automatizar la aplicación de políticas. Consulte la [documentación de destinos](../../destinations/home.md) para obtener más información sobre las opciones de configuración de un destino en particular.

Consulte el apéndice de este documento para obtener una lista de [acciones de marketing definidas por Adobe disponibles](#core-actions). También puede definir sus propias acciones de marketing personalizadas mediante la API [!DNL Policy Service] o la interfaz de usuario [!DNL Experience Platform]. En la siguiente sección se proporciona más información sobre cómo trabajar con acciones y políticas de marketing.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Experience Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=es).
-->

## Administración de políticas de uso de datos {#manage}

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden utilizar la API [!DNL Policy Service] o la interfaz de usuario [!DNL Experience Platform] para administrar y evaluar las directivas relacionadas con las acciones de marketing que se realizan en los datos que contienen etiquetas de uso de datos. Puede crear y actualizar directivas, determinar el estado de una directiva y trabajar con acciones de marketing para evaluar si una acción específica infringe una directiva de uso de datos.

>[!IMPORTANT]
>
>Todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas de forma predeterminada. Para que se considere una directiva individual para su aplicación, debe habilitar manualmente esa directiva a través de la API o la interfaz de usuario.

Para obtener instrucciones paso a paso sobre cómo trabajar con acciones de marketing y políticas de uso de datos en la API, consulte el tutorial de [creación y evaluación de políticas de uso de datos](create.md). Para obtener más información sobre las operaciones clave proporcionadas por la API [!DNL Policy Service], consulte la [Guía para desarrolladores de Policy Service](../api/getting-started.md).

Para obtener información sobre cómo trabajar con acciones y directivas de marketing en la interfaz de usuario de [!DNL Experience Platform], consulte la [guía del usuario sobre la directiva de uso de datos](./user-guide.md).

## Pasos siguientes

Este documento proporciona una introducción a las políticas de uso de datos dentro del marco de trabajo de control de datos. Ahora puede seguir leyendo la documentación del proceso vinculada a través de esta guía para obtener más información sobre cómo trabajar con políticas en la API y la IU.

## Apéndice

La siguiente sección proporciona información adicional sobre las políticas de uso de datos.

### Acciones de marketing definidas por Adobe {#core-actions}

En la tabla siguiente se describen las acciones de marketing principales que proporciona Adobe de forma predeterminada.

>[!NOTE]
>
>Las acciones de marketing principales deben considerarse como un punto de partida para ayudarle a identificar qué políticas de uso crear y comprobar violaciones. Las definiciones y la forma en que se interpretan dependen de las necesidades y directivas de su organización.

| Acción de marketing | Descripción |
| --- | --- |
| Analytics  | Una acción que utiliza datos con fines de análisis, como medir, analizar y crear informes sobre el uso que hacen los clientes de los sitios o las aplicaciones de su organización. |
| Combinación con datos directamente identificables | Una acción que combina cualquier información de identificación personal (PII) con datos anónimos. Los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de dichos datos con datos directamente identificables. |
| Segmentación entre sitios | Una acción que utiliza datos para la segmentación de anuncios entre sitios. La combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas, se denomina datos entre sitios. Los datos entre sitios generalmente se recopilan y procesan para hacer deducciones sobre los intereses de los usuarios. |
| Ciencia de datos | Una acción que utiliza datos para flujos de trabajo de ciencia de datos. Algunos contratos incluyen prohibiciones explícitas sobre el uso de datos para la ciencia de datos. A veces se formulan en términos que prohíben el empleo de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado. |
| Exportación de datos | Una acción que exporta datos a cualquier ubicación o destino fuera de los productos y servicios de Adobe. Por ejemplo: descargar datos en el equipo local, copiar datos de la pantalla, programar el envío de datos a una ubicación fuera de Adobe, Proyectos programados de Customer Journey Analytics, Descargar informes, API de informes, etc. |
| Segmentación por correo electrónico | Una acción que utiliza datos en campañas de direccionamiento de correo electrónico. |
| Exportar a terceros | Una acción que exporta datos a procesadores y entidades que no tienen relaciones directas con los clientes. Muchos proveedores de datos tienen condiciones en los contratos que prohíben la exportación de datos desde el lugar donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales suelen restringir la transferencia de los datos que se reciben de ellas. |
| Advertising in situ | Una acción que utiliza datos para anuncios en el sitio, incluida la selección y el envío de anuncios en los sitios web o las aplicaciones de la organización, o para medir el envío y la eficacia de dichos anuncios. |
| Personalization in situ | Una acción que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer deducciones sobre los intereses de los usuarios, y se utiliza para seleccionar qué contenido o anuncios se muestran en función de esas deducciones. |
| Coincidencia de segmento | Una acción que utiliza datos para la coincidencia de segmentos de Adobe Experience Platform, lo que permite a dos o más usuarios de Experience Platform intercambiar datos de audiencia. Al habilitar las directivas que hacen referencia a esta acción, puede restringir qué datos se utilizan para la coincidencia de segmentos. Por ejemplo, si la directiva principal &quot;Restringir el uso compartido de datos&quot; está habilitada, no se podrá usar ningún dato con una etiqueta [C11](../labels/reference.md#c11) para la coincidencia de segmentos. |
| Personalization de identidad única | Una acción que requiere que se utilice una sola identidad con fines de personalización en lugar de vincular identidades de varias fuentes. |
