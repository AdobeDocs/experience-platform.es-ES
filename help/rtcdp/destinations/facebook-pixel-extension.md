---
keywords: facebook pixel extensions;facebook pixel extension;facebook pixel destinations;facebook pixel
title: Extensión de píxeles de Facebook
seo-title: Extensión de píxeles de Facebook
description: La extensión Pixel de Facebook es un destino publicitario en la plataforma de datos del cliente en tiempo real de Adobe. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
seo-description: null
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 5%

---


# [!DNL Facebook Pixel] Extensión {#facebook-pixel-extension}

## Información general {#overview}

La [!DNL Facebook Pixel] es una herramienta de análisis que le permite medir la eficacia de la publicidad mediante la comprensión de las acciones que las personas realizan en el sitio web.

[!DNL Facebook Pixel] es una extensión de publicidad en la plataforma de datos del cliente en tiempo real de Adobe. Para obtener más información sobre la funcionalidad de extensión, consulte el sitio web [Facebook Pixel](https://developers.facebook.com/docs/facebook-pixel/).

Este destino es una extensión de Experience Platform Launch. Para obtener más información sobre cómo funcionan las extensiones de Launch en Adobe Real-time CDP, consulte Visión general [de las extensiones de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Extensión de píxeles de Facebook](assets/facebook-pixel-extension.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] catálogo para todos los clientes que han adquirido CDP en tiempo real de Adobe.

Para utilizar esta extensión, necesita acceder al Experience Platform Launch. Experience Platform Launch se ofrece a los clientes de Adobe Experience Cloud como una función incluida de valor añadido. Póngase en contacto con el administrador de su organización para obtener acceso a Launch y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar la [!DNL Facebook Pixel] extensión:

1. En la interfaz [CDP en tiempo real de](http://platform.adobe.com/)Adobe, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
2. Seleccione la extensión del catálogo o utilice la barra de búsqueda.
3. Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configurar]** está atenuado, le falta el permiso **[!UICONTROL manage_properties]** . Consulte [Requisitos previos](#prerequisites).
4. En la ventana **[!UICONTROL Seleccionar la propiedad]** Launch disponible, seleccione la propiedad Launch en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en Launch. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [de la página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propiedades de la documentación de Launch.
5. El flujo de trabajo le lleva a Iniciar para completar la instalación.

También puede instalar la extensión directamente en la interfaz del [Experience Platform Launch](https://launch.adobe.com/). Consulte [Añadir una nueva extensión](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) en la documentación de Launch.


## Cómo usar la extensión {#how-to-use}

Una vez instalada la extensión, puede configurar inicios para ella directamente en Launch.

En Launch, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión únicamente en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la documentación [](https://docs.adobe.com/help/es-ES/launch/using/reference/manage-resources/rules.html)Reglas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de Launch.

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de CDP en tiempo real de Adobe seguirá mostrando **[!UICONTROL Instalar]** para la extensión. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para llegar a Iniciar y configurar o eliminar la extensión.

Para actualizar la extensión, consulte Actualización [de](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) Extension en la documentación de Launch.
