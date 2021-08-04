---
keywords: extensión del DIL del Audience Manager;audience manager de destino;extensión dil
title: extensión del DIL del Audience Manager
description: La extensión del DIL del Audience Manager es un destino de la plataforma de administración de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# extensión del DIL del Audience Manager {#aam-dil-extension}

## Información general {#overview}

Esta es la extensión de Data Integration Library de Adobe Audience Manager (implementación del lado del cliente). Nota: Esta extensión no está pensada para utilizarse en el reenvío de datos de Adobe Analytics del lado del servidor (SSF). Para SSF, utilice la extensión de Adobe Analytics. Importante: A partir de la versión 8.0, DIL tiene una gran dependencia del [!DNL Experience Cloud] servicio de ID, versión 3.3 o superior. Implemente tanto el [!DNL Experience Cloud] servicio de ID como el DIL para las [!DNL Audience Manager] funcionalidades completas de integración de datos.

[!DNL Audience Manager] DIL es una extensión de plataforma de gestión de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [página de la extensión del Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) en la documentación de las etiquetas.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones en Platform, consulte la [descripción general de las extensiones de etiquetas](../launch-extensions/overview.md).

![extensión del DIL del Audience Manager](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, es necesario acceder a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión del DIL [!DNL Audience Manager]:

En la [Platform interface](https://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** aparece atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la documentación de etiquetas [](../../../tags/ui/administration/companies-and-properties.md#properties-page).

El flujo de trabajo le guía por los pasos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la [página de extensión del Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) en la documentación de etiquetas.

También puede instalar la extensión directamente en la [interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía [adding a new extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la interfaz de usuario de la recopilación de datos, puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [rules](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de seguirá mostrando **[!UICONTROL Install]** para la extensión de . Inicie el flujo de trabajo de instalación tal como se describe en [Install extension](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía del [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
