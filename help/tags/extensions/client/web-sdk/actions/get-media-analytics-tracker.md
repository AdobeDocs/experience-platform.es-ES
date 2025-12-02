---
title: Obtener el rastreador de Media Analytics
description: Exporta la API de medios heredada a un objeto window.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# Obtener rastreador de Media Analytics

La acción **[!UICONTROL Get Media Analytics tracker]** se usa para obtener la API heredada de Media Analytics. Al configurar la acción y proporcionar un nombre de objeto, la API heredada de Media Analytics se exporta a ese objeto de ventana. Esta acción es útil para pasar de Media Analytics heredado a Streaming Media Analytics.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]**, luego establezca [!UICONTROL Action type] en **[!UICONTROL Get Media Analytics tracker]**.

![Imagen de la interfaz de usuario de Experience Platform que muestra el tipo de acción Obtener rastreador de Media Analytics.](../assets/get-media-analytics-tracker.png)

Esta acción contiene un único campo que puede configurar:

* **[!UICONTROL Export the Media Legacy API to this window object]**: selecciona el objeto deseado al que exportar la API heredada de medios. Si no se proporciona ninguno, la acción exporta la API a `window.Media`.
