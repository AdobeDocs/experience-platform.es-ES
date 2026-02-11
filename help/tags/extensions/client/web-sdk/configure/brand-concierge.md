---
title: Ajustes de configuración de Brand Concierge
description: Configure la persistencia de la sesión y los tiempos de espera del flujo para el chat de Brand Concierge.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 4%

---

# Ajustes de configuración de Brand Concierge

>[!AVAILABILITY]
>
>Brand Concierge para Web SDK se encuentra actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

La sección **[!UICONTROL Brand Concierge]** permite controlar el comportamiento de las sesiones de chat de Brand Concierge en la extensión de etiquetas de Web SDK.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Brand Concierge]**.

Las opciones disponibles son las siguientes:

## [!UICONTROL Sticky conversation session]

Casilla de verificación que mantiene las sesiones de Brand Concierge en todas las páginas al cargar mediante una cookie de sesión. Esta opción está desactivada de forma predeterminada. Consulte [`conversation`](/help/collection/js/commands/configure/conversation.md) en la documentación de la biblioteca de JavaScript para obtener instrucciones sobre cómo establecer este valor.

## [!UICONTROL Stream timeout (seconds)]

Cantidad máxima de tiempo, en segundos, que se debe esperar a los fragmentos del flujo de conversación antes de activar un error de tiempo de espera. El valor predeterminado es `10` segundos.
