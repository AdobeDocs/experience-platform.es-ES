---
title: Extensión de Adobe Media Analytics for Audio and Video
seo-title: Extensión de Adobe Media Analytics for Audio and Video
description: La extensión Adobe Media Analytics para audio y vídeo es un destino de análisis en Adobe Real-time Customer Data Platform. Para obtener más información sobre la funcionalidad de extensión, consulte la página de extensión en Adobe Exchange.
seo-description: La extensión Adobe Media Analytics para vídeo es un destino de análisis en Adobe Real-time Customer Data Platform. Para obtener más información sobre la funcionalidad de extensión, consulte la página de extensión en Adobe Exchange.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 11%

---


# Extensión de Adobe Media Analytics for Audio and Video {#adobe-analytics-for-video-extension}

## Información general {#overview}

Adobe Media Analytics para audio y vídeo es un complemento de la oferta básica de Analytics que proporciona a los clientes una medición sólida para vídeo, audio y anuncios.

Adobe Media Analytics para audio y vídeo es una extensión de análisis en Adobe Real-time Customer Data Platform. Para obtener más información sobre la funcionalidad de extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100157.html).

Este destino es una [!DNL Experience Platform Launch] extensión. Para obtener más información sobre cómo funcionan [!DNL Launch] las extensiones en tiempo real de CDP de Adobe, consulte Información general [sobre las extensiones de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Extensión de Adobe Media Analytics for Audio and Video](/help/rtcdp/destinations/assets/adobe-analytics-extension.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] catálogo para todos los clientes que han adquirido CDP en tiempo real de Adobe.

Para utilizar esta extensión, necesita acceder a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida. Póngase en contacto con el administrador de su organización para obtener acceso a [!DNL Launch] y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar la extensión Adobe Analytics for Video:

1. En la interfaz [CDP en tiempo real de](http://platform.adobe.com/)Adobe, vaya a **[!UICONTROL Destinos > Catálogo]**.
2. Seleccione la extensión del catálogo o utilice la barra de búsqueda.
3. Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Instalar extensión]** en el carril derecho. Si el control **[!UICONTROL Instalar extensión]** está atenuado, le falta el permiso **[!UICONTROL manage_properties]** . Consulte [Requisitos previos](#prerequisites).
4. En la ventana **[!UICONTROL Seleccionar la propiedad]** Launch disponible, seleccione la [!DNL Launch] propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en [!DNL Launch]. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [de la página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propiedades de la [!DNL Launch] documentación.
5. El flujo de trabajo le lleva a [!DNL Launch] completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la página [de extensión](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html) Adobe Media Analytics para audio y vídeo en la [!DNL Experience Launch] documentación.

También puede instalar la extensión directamente en la interfaz del [Experience Platform Launch](https://launch.adobe.com/). Consulte [Añadir una nueva extensión](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) en la [!DNL Launch] documentación.


## Cómo usar la extensión {#how-to-use}

Una vez instalada la extensión, puede configurar inicios directamente en [!DNL Launch].

En [!DNL Launch], puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión únicamente en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la documentación [](https://docs.adobe.com/help/es-ES/launch/using/reference/manage-resources/rules.html)Reglas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la [!DNL Launch] interfaz.

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de CDP en tiempo real de Adobe seguirá mostrando **[!UICONTROL Instalar]** para la extensión. Inicie el flujo de trabajo de instalación tal como se describe en [Instalar extensión](#install-extension) para obtener [!DNL Launch] y configurar o eliminar la extensión.

Para actualizar la extensión, consulte Actualización [de](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) Extension en la [!DNL Launch] documentación.



