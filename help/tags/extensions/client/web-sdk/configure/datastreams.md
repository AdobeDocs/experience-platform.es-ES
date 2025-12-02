---
title: Ajustes de configuración de flujo de datos
description: Configure la secuencia de datos para enviar datos a mediante la extensión de etiquetas Web SDK.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Ajustes de configuración de flujo de datos

Esta sección de configuración le permite determinar a qué [secuencia de datos](/help/datastreams/overview.md) desea enviar datos. **Se requiere un id. de secuencia de datos para todos los datos enviados a Edge Network.**

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Datastreams]**.

![Imagen que muestra la configuración de secuencia de datos de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas](../assets/web-sdk-ext-datastreams.png)

Al seleccionar flujos de datos, puede hacerlo para cada [entorno](/help/tags/ui/publishing/environments.md) ([!UICONTROL Development], [!UICONTROL Staging] y [!UICONTROL Production]). Estos campos son útiles cuando desea separar los datos enviados entre los entornos de desarrollo, ensayo y producción. Esto permite un flujo de trabajo cómodo en el que no tiene que preocuparse por enviar datos al conjunto de datos incorrecto, siempre y cuando instale el cargador de etiquetas correcto en cada entorno respectivo.

Puede rellenar los ID de flujo de datos mediante uno de los métodos siguientes:

* **[!UICONTROL Choose from list]**: cada entorno contiene dos menús desplegables, que le permiten seleccionar la zona protegida y la secuencia de datos para el entorno seleccionado. Los valores de cada menú desplegable dependen de las [secuencias de datos](/help/datastreams/overview.md) configuradas en cada [zona protegida](/help/sandboxes/ui/overview.md) correspondiente.

* **[!UICONTROL Enter values]**: como alternativa al uso de menús desplegables para seleccionar la secuencia de datos deseada, puede especificar manualmente el ID de secuencia de datos deseado directamente. Cada entorno le permite introducir directamente un ID de secuencia de datos o rellenar este campo con un [elemento de datos](/help/tags/ui/managing-resources/data-elements.md).
