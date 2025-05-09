---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas;información general sobre etiquetas de uso de datos
solution: Experience Platform
title: Resumen de etiquetas de uso de datos
description: Descubra cómo se utilizan las etiquetas de uso de datos para ayudar a aplicar el cumplimiento de la gobernanza de datos en Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 916eb01ea7878366620b859c1d6a667a88b850c9
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 16%

---

# Información general sobre las etiquetas de uso de datos {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Control de acceso a datos confidenciales y protegidos"
>abstract="<h2>Descripción</h2><p>Controle el acceso a atributos de datos o segmentos específicos, lo que le permite diseñar flujos de trabajo flexibles para las distintas personas y equipos que operan en los casos de uso de Experience Platform.</p>"

Adobe Experience Platform le permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada uno según [políticas de control de datos](../policies/overview.md) y [políticas de control de acceso](../../access-control/abac/ui/policies.md) relacionadas.

Este documento proporciona información general sobre las etiquetas de uso de datos en [!DNL Experience Platform].

## Explicación de las etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de gobernanza que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas recomiendan etiquetar los datos en cuanto se introduzcan en [!DNL Experience Platform] o en cuanto estén disponibles los datos para su uso en [!DNL Experience Platform].

Las etiquetas de uso de datos que se aplican al nivel del conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) de un conjunto de datos, sin propagación.

[!DNL Experience Platform] proporciona varias etiquetas de uso de datos &quot;principales&quot; listas para usarse, que cubren una amplia variedad de restricciones comunes aplicables al control de datos. Para obtener más información sobre estas etiquetas y las políticas de gobernanza que representan, consulte la guía sobre [etiquetas de uso de datos principales](reference.md).

Además de las etiquetas proporcionadas por Adobe, también puede definir sus propias etiquetas personalizadas para su organización. Consulte la sección sobre [administración de etiquetas](#manage-labels) para obtener más información.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite a Experience Platform aplicar directivas automáticamente al activar segmentos en los destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Por lo tanto, puede identificar más fácilmente qué atributos deben excluirse de los segmentos e impedir que hereden etiquetas de campos excluidos.

Para obtener más información sobre cómo funciona la aplicación automática en Experience Platform, consulte la descripción general de [aplicación automática de directivas](../enforcement/auto-enforcement.md).

### Herencia de los controles de exportación de datos de Adobe Audience Manager

[!DNL Experience Platform] tiene la capacidad de compartir segmentos con Adobe Audience Manager. Cualquier control de exportación de datos que se haya aplicado a segmentos de Audience Manager se traduce en etiquetas equivalentes y acciones de marketing reconocidas por el control de datos de [!DNL Experience Platform].

Para obtener información sobre cómo se asignan los controles de exportación de datos a las etiquetas de uso de datos de [!DNL Experience Platform], consulte la [documentación de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Administración de etiquetas de uso de datos en [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instrucciones"
>abstract="<ul><li>Etiquete los campos y segmentos XDM para clasificar aquellos a los que desea restringir el acceso.</li><li>Funciones de etiqueta, añadir etiquetas a una función permite definir aquellas para las que los integrantes deben tener restricciones.</li><li>Crear directivas, una directiva genera una relación entre las etiquetas de los objetos etiquetados como campos XDM y segmentos y las etiquetas de las funciones. Si las etiquetas coinciden, se puede definir un permiso o un acceso restringido.</li></ul>"

Puede administrar las etiquetas de uso de datos mediante las API [!DNL Experience Platform] o la interfaz de usuario. Consulte las subsecciones siguientes para obtener detalles sobre cada una de ellas.

### Uso de la IU

El área de trabajo **[!UICONTROL Políticas]** de la interfaz de usuario de [!DNL Experience Platform] le permite ver y administrar las etiquetas principales y personalizadas de su organización. Puede usar el área de trabajo **[!UICONTROL Esquemas]** para [aplicar etiquetas a sus esquemas XDM (Experience Data Model)](../../xdm/tutorials/labels.md), o aprender a [crear y administrar etiquetas personalizadas en la interfaz de usuario **[!UICONTROL Políticas]**](./user-guide.md) leyendo la guía del usuario de etiquetas de uso de datos en su lugar.

>[!IMPORTANT]
>
>Las etiquetas ya no se pueden aplicar a campos de nivel de conjunto de datos. Este flujo de trabajo ha quedado obsoleto y favorece la aplicación de etiquetas en el nivel de esquema. Cualquier etiqueta aplicada anteriormente en el nivel de objeto del conjunto de datos seguirá siendo compatible mediante la interfaz de usuario de Experience Platform hasta el 31 de mayo de 2024. Para garantizar que las etiquetas sean coherentes en todos los esquemas, cualquier etiqueta adjunta anteriormente a campos de nivel de conjunto de datos debe migrarse al nivel de esquema durante el próximo año. Consulte la sección sobre [migración de etiquetas aplicadas anteriormente](../e2e.md#migrate-labels) para obtener instrucciones sobre cómo hacerlo.

### Uso de API

El extremo `/labels` de la [API del servicio de directivas](https://www.adobe.io/experience-platform-apis/references/policy-service/) le permite administrar mediante programación las etiquetas de uso de datos, incluida la creación de etiquetas personalizadas. Consulte la [guía de extremo de etiquetas](../api/labels.md) para obtener más información.

La [API del servicio de conjunto de datos](https://www.adobe.io/experience-platform-apis/references/dataset-service/) se usa para administrar etiquetas para conjuntos de datos y campos. Consulte la guía sobre [administración de etiquetas de conjuntos de datos](./dataset-api.md) para obtener más información.

## Pasos siguientes

Este documento proporciona una introducción a las etiquetas de uso de datos y su función dentro del marco de trabajo de control de datos. Consulte la documentación vinculada a través de esta guía para obtener más información sobre cómo administrar etiquetas en [!DNL Experience Platform].
