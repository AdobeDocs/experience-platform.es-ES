---
title: Ajustes de configuración de consentimiento
description: Configure los ajustes predeterminados de consentimiento y privacidad para la extensión de etiqueta.
exl-id: 93913a8b-0351-409d-b26a-8dc2ac0296c5
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Ajustes de configuración de consentimiento {#consent}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_consent"
>title="Consentimiento"
>abstract="Selecciona el nivel de consentimiento predeterminado que se asume si no se proporciona ninguna otra preferencia de consentimiento explícita."

La sección **[!UICONTROL Consent]** le permite seleccionar el nivel de consentimiento predeterminado que se asume si no se proporciona ninguna otra preferencia de consentimiento explícita. El nivel de consentimiento predeterminado no se guarda en los perfiles de usuario.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Consent]**.

![Imagen que muestra la configuración de privacidad de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas](../assets/web-sdk-ext-privacy.png)

Esta sección contiene un único conjunto de botones de opción que determinan el nivel de consentimiento predeterminado:

* **[!UICONTROL In]**: recopile eventos que se produzcan antes de que el usuario proporcione preferencias de consentimiento.
* **[!UICONTROL Out]**: coloque eventos que se produzcan antes de que el usuario proporcione preferencias de consentimiento.
* **[!UICONTROL Pending]**: eventos de cola que se producen antes de que el usuario proporcione preferencias de consentimiento. Cuando se concede el consentimiento, los eventos en cola se envían a Adobe. Cuando se deniega el consentimiento, se descartan los eventos en cola.
* **[!UICONTROL Provide a data element]**: seleccione un elemento de datos que determine una de las opciones de configuración anteriores. Los valores válidos incluyen las cadenas `"in"`, `"out"` o `"pending"`.

Si su organización requiere el consentimiento explícito del usuario para recopilar datos, Adobe recomienda establecer el consentimiento predeterminado en **[!UICONTROL Out]** o **[!UICONTROL Pending]**.
