---
title: Ajustes de configuración de Adobe Advertising
description: Habilitar o deshabilitar la funcionalidad de la plataforma del lado de la demanda.
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# Ajustes de configuración de Adobe Advertising {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising para Web SDK se encuentra actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Configure las opciones de las integraciones de Adobe Advertising. Tenga en cuenta que no es necesaria ninguna configuración de publicidad para habilitar la medición de clics. Los clientes de Search, Social y Commerce no tienen que realizar más acciones; sin embargo, los usuarios de Demand-side Platform (DSP) deben configurar anunciantes en esta sección para medir las conversiones de visualización."

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
