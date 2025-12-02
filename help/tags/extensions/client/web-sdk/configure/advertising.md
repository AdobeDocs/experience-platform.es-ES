---
title: Ajustes de configuración de Adobe Advertising
description: Habilitar o deshabilitar la funcionalidad de la plataforma del lado de la demanda.
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Ajustes de configuración de Adobe Advertising

>[!AVAILABILITY]
>
>Adobe Advertising para Web SDK se encuentra actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

La sección **[!UICONTROL Adobe Advertising]** le permite habilitar o deshabilitar la funcionalidad de la plataforma del lado de la demanda (DSP) si se utiliza en la implementación. Solo debe definir este campo si la implementación utiliza un DSP.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Adobe Advertising]**.

Actualmente, hay una opción disponible.

## [!UICONTROL Adobe Advertising DSP]

Menú desplegable que habilita o deshabilita la funcionalidad de DSP para Adobe Advertising.

* **[!UICONTROL Enabled]**: habilita el seguimiento de visualizaciones.
* **[!UICONTROL Disabled]**: deshabilita el seguimiento de visualizaciones.

Cuando está habilitada, están disponibles las siguientes configuraciones:

* **[!UICONTROL Advertisers]**: anunciantes para los que se va a habilitar el seguimiento de visualizaciones.
* **[!UICONTROL ID5 partner ID]**: Opcional. ID de socio ID5 de su organización. Esta configuración permite que Web SDK recopile ID5 universales.
* **[!UICONTROL RampID JavaScript path]**: Opcional. Ruta de acceso al código JavaScript [!DNL LiveRamp RampID] de su organización (`ats.js`).  Esta configuración permite que Web SDK recopile [!DNL RampID] ID universales.
