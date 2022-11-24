---
keywords: extensión del DIL del Audience Manager;audience manager de destino;extensión dil
title: extensión del DIL del Audience Manager
description: La extensión del DIL del Audience Manager es un destino de la plataforma de administración de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# extensión del DIL del Audience Manager {#aam-dil-extension}

## Información general {#overview}

Esta es la extensión de Data Integration Library de Adobe Audience Manager (implementación del lado del cliente). Nota: Esta extensión no está pensada para utilizarse en el reenvío de datos de Adobe Analytics del lado del servidor (SSF). Para SSF, utilice la extensión de Adobe Analytics. Importante: A partir de la versión 8.0, el DIL tiene una gran dependencia de la variable [!DNL Experience Cloud] Servicio de ID, versión 3.3 o superior. Implemente ambas [!DNL Experience Cloud] Servicio de ID y DIL para obtener información completa [!DNL Audience Manager] funciones de integración de datos.

[!DNL Audience Manager] DIL es una extensión de plataforma de gestión de datos (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [página de extensión del Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) en la documentación de etiquetas.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones en Platform, consulte la [información general sobre las extensiones de etiquetas](../launch-extensions/overview.md).

![extensión del DIL del Audience Manager](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] catálogo para todos los clientes que han comprado Platform.

Para utilizar esta extensión, es necesario acceder a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda la **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar el [!DNL Audience Manager] Extensión del DIL:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, le falta la variable **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md#properties-page).

El flujo de trabajo le guía por los pasos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la [página de extensión del Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) en la documentación de etiquetas.

También puede instalar la extensión directamente en el [Interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la interfaz de usuario de la recopilación de datos, puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [reglas](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario sigue mostrándose **[!UICONTROL Instalar]** para la extensión de . Inicie el flujo de trabajo de instalación tal como se describe en [Extensión de instalación](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía de la [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
