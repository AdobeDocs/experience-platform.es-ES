---
title: Ajustes de anulación de configuración de flujo de datos
description: Modifique las opciones de configuración cuando se cumplan determinadas condiciones.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# Ajustes de anulación de configuración de flujo de datos

Las anulaciones de flujos de datos permiten definir configuraciones adicionales para los flujos de datos, que se pasan a Edge Network a través de Web SDK. Esta función le ayuda a almacenar en déclencheur de forma condicional diferentes comportamientos de flujo de datos sin crear un nuevo flujo de datos ni modificar la configuración existente.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Datastream configuration overrides]**.

La anulación de la configuración de la secuencia de datos es un proceso de dos pasos:

1. En primer lugar, debe definir la anulación de la configuración de la secuencia de datos al [configurar una secuencia de datos](/help/datastreams/configure.md) en la IU de Datastreams. Consulte [Anulaciones de configuración de secuencia de datos](/help/datastreams/overrides.md) en la documentación de flujos de datos para obtener instrucciones sobre cómo configurar las anulaciones.
1. Después de configurar la anulación de la secuencia de datos en la interfaz de usuario de flujos de datos, puede configurar la extensión de etiqueta.

Las anulaciones de flujos de datos deben configurarse por entorno. Los entornos de desarrollo, ensayo y producción tienen invalidaciones independientes. Puede copiar la configuración de anulación entre cualquier entorno deseado:

![Imagen que muestra las anulaciones de configuración de secuencia de datos usando la página de extensión de etiquetas Web SDK.](../assets/datastream-overrides.png)

De forma predeterminada, las invalidaciones de configuración de la secuencia de datos están deshabilitadas. La opción **[!UICONTROL Match datastream configuration]** está seleccionada de manera predeterminada.

![La interfaz de usuario de la extensión de etiquetas Web SDK que muestra la configuración de secuencia de datos invalida la configuración predeterminada.](../assets/datastream-override-default.png)

Para habilitar las anulaciones de secuencia de datos en la extensión de etiqueta, seleccione **[!UICONTROL Enabled]** en el menú desplegable.

![La interfaz de usuario de la extensión de etiquetas Web SDK muestra las anulaciones de configuración de secuencia de datos habilitada.](../assets/datastream-override-enabled.png)

Después de habilitar las invalidaciones de configuración de la secuencia de datos, puede configurar las invalidaciones para cada servicio descrito a continuación. Estos ajustes de anulación de flujos de datos anulan cualquier configuración y regla del flujo de datos del lado del servidor para el entorno seleccionado.

## Adobe Analytics

Anule el enrutamiento de datos al servicio Adobe Analytics.

![Imagen de la interfaz de usuario de la extensión de etiquetas Web SDK que muestra la configuración de anulación de secuencia de datos de Adobe Analytics.](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: habilita o deshabilita el enrutamiento de datos a Adobe Analytics.
* **[!UICONTROL Report suites]**: los identificadores de los grupos de informes de destino en Adobe Analytics. El valor debe ser un grupo de informes de anulación preconfigurado (o una lista de grupos de informes separados por comas) de la configuración del conjunto de datos. Esta configuración anula los grupos de informes principales.
* **[!UICONTROL Add Report Suite]**: seleccione esta opción para agregar grupos de informes adicionales.

## Adobe Audience Manager

Anular el enrutamiento de datos a Adobe Audience Manager.

![Imagen de la interfaz de usuario de la extensión de etiquetas Web SDK que muestra la configuración de anulación de secuencia de datos de Adobe Audience Manager.](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: habilita o deshabilita el enrutamiento de datos a Adobe Audience Manager.
* **[!UICONTROL Third-party ID sync container]**: ID del contenedor de sincronización de ID de terceros de destino en Audience Manager. El valor debe ser un contenedor secundario preconfigurado de la configuración del conjunto de datos y anula el contenedor principal.

## Adobe Experience Platform

Anular el enrutamiento de datos a Adobe Experience Platform.

![Imagen de la interfaz de usuario de la extensión de etiquetas Web SDK que muestra la configuración de anulación de secuencia de datos de Adobe Experience Platform.](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: habilita o deshabilita el enrutamiento de datos a Adobe Experience Platform.
* **[!UICONTROL Event dataset]**: ID del conjunto de datos de evento de destino en Adobe Experience Platform. El valor debe ser un conjunto de datos secundario preconfigurado de la configuración del conjunto de datos.
* **[!UICONTROL Offer Decisioning]**: habilita o deshabilita el enrutamiento de datos al servicio [!DNL Offer Decisioning].
* **[!UICONTROL Edge Segmentation]**: habilita o deshabilita el enrutamiento de datos al servicio [!DNL Edge Segmentation].
* **[!UICONTROL Personalization Destinations]**: habilita o deshabilita el enrutamiento de datos a destinos de personalización.
* **[!UICONTROL Adobe Journey Optimizer]**: habilita o deshabilita el enrutamiento de datos a [!DNL Adobe Journey Optimizer].

## Reenvío de eventos del lado del servidor de Adobe

Omitir el enrutamiento de datos al servicio de reenvío de eventos del lado del servidor de Adobe.

![Imagen de la interfaz de usuario de la extensión de etiquetas Web SDK que muestra la configuración de anulación de secuencia de datos del reenvío de eventos del lado del servidor de Adobe.](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: habilita o deshabilita el enrutamiento de datos al servicio de reenvío de eventos del lado del servidor de Adobe.

## Adobe Target {#target}

Anular el enrutamiento de datos a Adobe Target.

![Imagen de la interfaz de usuario de la extensión de etiquetas Web SDK que muestra la configuración de anulación de secuencia de datos de Adobe Target.](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: habilita o deshabilita el enrutamiento de datos a Adobe Target.
