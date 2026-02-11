---
title: Componentes de compilación personalizados
description: Cree una compilación personalizada de Web SDK que deshabilite las características para reducir el tamaño de compilación.
exl-id: 853e0a6c-0953-4e08-9a7d-334aab022583
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Componentes de compilación personalizados

La biblioteca Web SDK incluye varios módulos para varias funciones, como personalización, identidad, seguimiento de vínculos y mucho más. Según sus casos de uso, es posible que solo necesite funciones específicas en lugar de toda la biblioteca. Deshabilitar los componentes de compilación le permite utilizar solo los módulos que necesita, reducir el tamaño de la biblioteca y mejorar el rendimiento.

Cuando desactiva un componente, ya no puede editar su configuración. Si utiliza varias instancias de Web SDK, los componentes de generación seleccionados se aplican a todas las instancias.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Expanda el acordeón **[!UICONTROL Custom build components]** en la parte superior.

>[!WARNING]
>
>Modificar incorrectamente esta configuración puede causar resultados no deseados, incluida la pérdida de datos. Pruebe exhaustivamente la implementación en un entorno de desarrollo antes de publicar estos cambios en producción.

Adobe ofrece la capacidad de deshabilitar los siguientes componentes de compilación de Web SDK:

| Componente Generar | Descripción | Funciones dependientes |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Permite la recopilación automática de vínculos y el seguimiento de Activity Map. | |
| **[!UICONTROL Advertising]** | Habilita la integración de Adobe Advertising con Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Admite la integración con Adobe Audience Manager, como sincronizaciones de ID. | |
| **[!UICONTROL Brand concierge]** | Habilita la integración con Brand concierge. |
| **[!UICONTROL Consent]** | Permite utilizar funciones de consentimiento. | [[!UICONTROL Set consent]](../actions/set-consent.md) acción |
| **[!UICONTROL Event merge]** | Obsoleto. | [[!UICONTROL Event merge ID]](../data-element-types.md) elemento de datos (obsoleto)<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) acción (obsoleto) |
| **[!UICONTROL Media Analytics bridge]** | Admite la integración con Media Analytics heredados. | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) acción |
| **[!UICONTROL Personalization]** | Admite integraciones con Adobe Target y Adobe Journey Optimizer. | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) acción |
| **[!UICONTROL Push notifications]** | Activa las notificaciones push web para Adobe Journey Optimizer. | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) acción |
| **[!UICONTROL Rules engine]** | Habilita la toma de decisiones mediante Adobe Journey Optimizer. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) acción<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) evento |
| **[!UICONTROL Streaming media]** | Admite la integración con la recopilación de medios de streaming. | [[!UICONTROL Send media event]](../actions/send-media-event.md) acción |
