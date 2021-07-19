---
keywords: extensión del DIL del Audience Manager;audience manager de destino;extensión dil
title: extensión del DIL del Audience Manager
description: La extensión del DIL del Audience Manager es un destino de la plataforma de administración de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# extensión del DIL del Audience Manager {#aam-dil-extension}

## Información general {#overview}

Esta es la extensión de Data Integration Library de Adobe Audience Manager (implementación del lado del cliente). Nota: Esta extensión no está pensada para utilizarse en el reenvío de datos de Adobe Analytics del lado del servidor (SSF). Para SSF, utilice la extensión de Adobe Analytics. Importante: A partir de la versión 8.0, DIL tiene una gran dependencia del [!DNL Experience Cloud] servicio de ID, versión 3.3 o superior. Implemente tanto el [!DNL Experience Cloud] servicio de ID como el DIL para las [!DNL Audience Manager] funcionalidades completas de integración de datos.

[!DNL Audience Manager] DIL es una extensión de plataforma de gestión de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [página de la extensión del Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) en la documentación del Experience Platform Launch.

Este destino es una extensión [!DNL Experience Platform Launch]. Para obtener más información sobre cómo funcionan las extensiones de Launch en Platform, consulte [información general sobre las extensiones de Experience Platform Launch](../launch-extensions/overview.md).

![extensión del DIL del Audience Manager](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, necesita acceder a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] se ofrece a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a [!DNL Platform Launch] y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión del DIL [!DNL Audience Manager]:

En la [Platform interface](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** aparece atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

En la ventana **[!UICONTROL Select available Launch property]**, seleccione la propiedad [!DNL Launch] en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en Launch. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [Properties page](../../../tags/ui/administration/companies-and-properties.md#properties-page) de la documentación [!DNL Launch].

El flujo de trabajo le lleva a [!DNL Launch] para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la [página de extensión del Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) en la documentación de [!DNL Experience Launch].

También puede instalar la extensión directamente en la [interfaz de Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Añadir una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) en la documentación de [!DNL Platform Launch].

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar las reglas para ella directamente en [!DNL Platform Launch].

En [!DNL Platform Launch], puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte [Documentación de reglas](../../../tags/ui/managing-resources/rules.md).

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz [!DNL Platform Launch].

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario de Platform sigue mostrando **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación tal como se describe en [Install extension](#install-extension) para llegar a [!DNL Platform Launch] y configurar o eliminar la extensión.

Para actualizar la extensión, consulte [Extension upgrade](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de [!DNL Platform Launch].
