---
keywords: extensión de DIL de Audience Manager;administrador de audiencias de destino;extensión de dil
title: extensión del DIL del Audience Manager
description: La extensión del DIL Audience Manager es un destino de la Plataforma de Gestión de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 3%

---


# Extensión de DIL de Audience Manager {#aam-dil-extension}

Es la extensión de Data Integration Library de Adobe Audience Manager (implementación en el lado del cliente). Nota: Esta extensión no está pensada para utilizarse para el reenvío de datos de Adobe Analytics por parte del servidor (SSF). Para SSF, utilice la extensión Adobe Analytics. Importante: A partir de la versión 8.0, DIL tiene una dependencia sólida del [!DNL Experience Cloud] servicio de ID, versión 3.3 o superior. Implemente tanto el [!DNL Experience Cloud] servicio de ID como el DIL para las [!DNL Audience Manager] capacidades completas de integración de datos.

[!DNL Audience Manager] DIL es una extensión de plataforma de Gestión de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [página de extensión del Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) en la documentación del Experience Platform Launch.

Este destino es una extensión [!DNL Experience Platform Launch]. Para obtener más información sobre cómo funcionan las extensiones de Launch en Platform, consulte [información general sobre extensiones de Experience Platform Launch](../launch-extensions/overview.md).

![extensión del DIL del Audience Manager](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han adquirido Platform.

Para utilizar esta extensión, necesita acceder a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida. Póngase en contacto con el administrador de su organización para obtener acceso a [!DNL Platform Launch] y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión de DIL [!DNL Audience Manager]:

En la interfaz [Plataforma](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configurar]** está atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

En la ventana **[!UICONTROL Seleccione la propiedad Launch disponible]**, seleccione la propiedad [!DNL Launch] en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en Launch. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [Página Propiedades](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentación de [!DNL Launch].

El flujo de trabajo le lleva a [!DNL Launch] para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la [página de extensión del Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) en la documentación de [!DNL Experience Launch].

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



