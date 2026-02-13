---
title: Opciones de configuración avanzadas
description: Configure las opciones avanzadas de la extensión de etiquetas Web SDK.
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Opciones de configuración avanzadas {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="Configuración avanzada"
>abstract="Opciones de configuración avanzadas. Adobe recomienda dejar estas opciones tal cual para la mayoría de las implementaciones."

Esta sección de configuración le permite modificar la configuración avanzada. Adobe recomienda dejar estas opciones tal cual para la mayoría de las implementaciones.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Advanced Settings]**.

![Imagen que muestra la configuración avanzada mediante la página de extensión de etiquetas de Web SDK](../assets/advanced-settings.png)

Actualmente, hay una opción disponible.

## [!UICONTROL Edge base path]

Utilice este campo para cambiar la ruta base que se utiliza para interactuar con Edge Network. Adobe podría solicitarle que cambie este campo si participa en ciertas pruebas alfa o beta; de lo contrario, Adobe recomienda dejarlo en el valor predeterminado de `ee`.

Este campo es el equivalente de etiqueta de [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) al configurar la biblioteca de JavaScript.
