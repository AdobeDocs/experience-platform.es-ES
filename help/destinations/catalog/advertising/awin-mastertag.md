---
keywords: Awin Advertiser, extensión de la etiqueta maestra;etiqueta maestra;Awin;awin;AWIN
title: Destino de la extensión Mastertag de Awin Advertiser
description: La extensión Mastertag de Awin Advertiser es un destino publicitario en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 3%

---


# [!DNL Awin Advertiser Mastertag] Extensión {#awin-mastertag-extension}

La [!DNL MasterTag] es una biblioteca JavaScript que contiene todas las funciones necesarias para la solución de seguimiento de Awin y debe agregarse incondicionalmente a todas las páginas del sitio, incluida la página de confirmación, pero excluyendo cualquier página que muestre o procese información de pago.

[!DNL Awin Advertiser Mastertag] es una extensión de publicidad en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Este destino es una extensión [!DNL Experience Platform Launch]. Para obtener más información sobre cómo funcionan las extensiones de Launch en Platform, consulte [información general sobre extensiones de Experience Platform Launch](../launch-extensions/overview.md).

![Awin Advertiser Mastertag extension en la interfaz de usuario](../../assets/catalog/advertising/awin-mastertag/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han adquirido Platform.

Para utilizar esta extensión, necesita acceder a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida. Póngase en contacto con el administrador de su organización para obtener acceso a [!DNL Platform Launch] y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión [!DNL Awin Advertiser Mastertag]:

En la interfaz [Plataforma](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configurar]** está atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

En la ventana **[!UICONTROL Seleccione la propiedad Lanzamiento de plataforma disponible]**, seleccione la propiedad [!DNL Platform Launch] en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en [!DNL Platform Launch]. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [Página Propiedades](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentación de [!DNL Launch].

El flujo de trabajo le lleva a [!DNL Platform Launch] para completar la instalación.

Para obtener más información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [página Mastertag de Awin Advertiser en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

También puede instalar la extensión directamente en la [interfaz de Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Añada una nueva extensión](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) en la documentación de [!DNL Platform Launch].


## Cómo usar la extensión {#how-to-use}

Una vez instalada la extensión, puede configurar inicios para ella directamente en [!DNL Platform Launch].

En [!DNL Platform Launch], puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión únicamente en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte [Documentación de reglas](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurar, actualizar y eliminar la extensión {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz [!DNL Platform Launch].

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de la plataforma aún muestra **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para llegar a [!DNL Platform Launch] y configurar o eliminar la extensión.

Para actualizar la extensión, consulte [Actualización de extensión](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) en la documentación de [!DNL Platform Launch].
