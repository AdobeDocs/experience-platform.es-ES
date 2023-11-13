---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas;información general sobre etiquetas de uso de datos
solution: Experience Platform
title: Resumen de etiquetas de uso de datos
description: Descubra cómo se utilizan las etiquetas de uso de datos para ayudar a aplicar el cumplimiento de la gobernanza de datos en Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 15%

---

# Información general sobre las etiquetas de uso de datos {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Control de acceso a datos confidenciales y protegidos"
>abstract="<h2>Descripción</h2><p>Controle el acceso a atributos de datos o segmentos específicos, lo que le permite diseñar flujos de trabajo flexibles para las distintas personas y equipos que operan en los casos de uso de Experience Platform.</p>"

Adobe Experience Platform le permite aplicar etiquetas de uso de datos a conjuntos de datos y campos, clasificando cada uno según los campos relacionados [políticas de gobernanza de datos](../policies/overview.md) y [directivas de control de acceso](../../access-control/abac/ui/policies.md).

Este documento proporciona información general sobre las etiquetas de uso de datos en [!DNL Experience Platform].

## Descripción de etiquetas de uso de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de gobernanza que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas recomiendan etiquetar los datos en cuanto se incorporen en [!DNL Experience Platform]o en cuanto los datos estén disponibles para su uso en [!DNL Platform].

Las etiquetas de uso de datos que se aplican al nivel del conjunto de datos se propagan a todos los campos dentro del conjunto de datos. Las etiquetas también se pueden aplicar directamente a campos individuales (encabezados de columna) de un conjunto de datos, sin propagación.

[!DNL Platform] proporciona varias etiquetas de uso de datos &quot;principales&quot; listas para usarse, que abarcan una amplia variedad de restricciones comunes aplicables al control de datos. Para obtener más información sobre estas etiquetas y las políticas de gobernanza que representan, consulte la guía sobre [etiquetas de uso de datos principales](reference.md).

Además de las etiquetas proporcionadas por Adobe, también puede definir sus propias etiquetas personalizadas para su organización. Consulte la sección sobre [administración de etiquetas](#manage-labels) para obtener más información.

## Herencia de etiquetas para segmentos de audiencia

Todos los segmentos de audiencia creados por [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md) heredan las etiquetas de uso de sus conjuntos de datos correspondientes. Esto permite al Experience Platform aplicar directivas automáticamente al activar segmentos en los destinos.

Además de heredar etiquetas de nivel de conjunto de datos, los segmentos heredan todas las etiquetas de nivel de campo de sus conjuntos de datos asociados de forma predeterminada. Por lo tanto, puede identificar más fácilmente qué atributos deben excluirse de los segmentos e impedir que hereden etiquetas de campos excluidos.

Para obtener más información sobre cómo funciona la aplicación automática en Platform, consulte la información general sobre [aplicación automática de políticas](../enforcement/auto-enforcement.md).

### Herencia de los controles de exportación de datos de Adobe Audience Manager

[!DNL Experience Platform] tiene la capacidad de compartir segmentos con Adobe Audience Manager. Los controles de exportación de datos que se hayan aplicado a los segmentos del Audience Manager se traducen en etiquetas y acciones de marketing equivalentes que reconoce [!DNL Experience Platform] Gobernanza de datos.

Para obtener una referencia sobre cómo los controles de exportación de datos específicos se asignan a las etiquetas de uso de datos en [!DNL Platform], consulte la [Documentación del Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Administración de etiquetas de uso de datos en [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instrucciones"
>abstract="<ul><li>Etiquete los campos y segmentos XDM para clasificar aquellos a los que desea restringir el acceso.</li><li>Funciones de etiqueta, añadir etiquetas a una función permite definir aquellas para las que los integrantes deben tener restricciones.</li><li>Crear directivas, una directiva genera una relación entre las etiquetas de los objetos etiquetados como campos XDM y segmentos y las etiquetas de las funciones. Si las etiquetas coinciden, se puede definir un permiso o un acceso restringido.</li></ul>"

Puede administrar las etiquetas de uso de datos mediante [!DNL Experience Platform] API para la interfaz de usuario de. Consulte las subsecciones siguientes para obtener detalles sobre cada una de ellas.

### Uso de la IU

El **[!UICONTROL Políticas]** workspace en [!DNL Experience Platform] La interfaz de usuario de le permite ver y administrar las etiquetas principales y personalizadas de su organización. Puede usar el complemento **[!UICONTROL Esquemas]** espacio de trabajo a [aplicar etiquetas a los esquemas XDM (Experience Data Model)](../../xdm/tutorials/labels.md)o aprenda a hacer lo siguiente [crear y administrar etiquetas personalizadas en el **[!UICONTROL Políticas] IU](./user-guide.md) leyendo la guía del usuario sobre etiquetas de uso de datos en su lugar.

>[!IMPORTANT]
>
>Las etiquetas ya no se pueden aplicar a campos de nivel de conjunto de datos. Este flujo de trabajo ha quedado obsoleto y favorece la aplicación de etiquetas en el nivel de esquema. Cualquier etiqueta aplicada anteriormente en el nivel de objeto del conjunto de datos seguirá siendo compatible mediante la IU de Platform hasta el 31 de mayo de 2024. Para garantizar que las etiquetas sean coherentes en todos los esquemas, cualquier etiqueta adjunta anteriormente a campos de nivel de conjunto de datos debe migrarse al nivel de esquema durante el próximo año. Consulte la sección sobre [migración de etiquetas aplicadas anteriormente](../e2e.md#migrate-labels) para obtener instrucciones sobre cómo hacerlo.

### Uso de API

El `/labels` punto final en la [API del servicio de directivas](https://www.adobe.io/experience-platform-apis/references/policy-service/) permite administrar etiquetas de uso de datos mediante programación, incluida la creación de etiquetas personalizadas. Consulte la [guía de extremo de etiquetas](../api/labels.md) para obtener más información.

El [API del servicio de conjunto de datos](https://www.adobe.io/experience-platform-apis/references/dataset-service/) se utiliza para administrar etiquetas para conjuntos de datos y campos. Consulte la guía de [administrar etiquetas de conjuntos de datos](./dataset-api.md) para obtener más información.

## Pasos siguientes

Este documento proporciona una introducción a las etiquetas de uso de datos y su función dentro del marco de trabajo de control de datos. Consulte la documentación relacionada con esta guía para obtener más información sobre cómo administrar etiquetas en [!DNL Experience Platform].
