---
keywords: Extensión de etiqueta de conversión del anunciante de Awin;etiqueta de conversión;Awin;awin;AWIN
title: Extensión de la etiqueta de conversión del anunciante de Awin
description: La extensión Awin Advertiser Conversion Tag es un destino publicitario en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---

# Extensión de la etiqueta de conversión del anunciante de Awin {#awin-conversiontag-extension}

## Información general {#overview}

La etiqueta de conversión es la declaración del objeto JavaScript AWIN.Tracking.Sale , que se realiza en la página de confirmación para indicar a la etiqueta maestra que se ha producido una conversión. A continuación, realizará las solicitudes de seguimiento necesarias.

La etiqueta de conversión del anunciante de Awin es una extensión de publicidad en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [información general sobre las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de Awin Advertiser Conversiontag en la interfaz de usuario](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo de destinos para todos los clientes que hayan comprado Platform.

Para utilizar esta extensión, necesita acceder a las etiquetas en Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a la interfaz de usuario de recopilación de datos y pídale que le conceda la variable **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar el [!DNL Awin Advertiser Conversion Tag] extensión:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, le falta la variable **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad tag en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md).

El flujo de trabajo le lleva a la interfaz de usuario de recopilación de datos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [Página de etiquetas de conversión del anunciante de Awin en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

También puede instalar la extensión directamente en el [Interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.


## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la interfaz de usuario de la recopilación de datos, puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [reglas](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario sigue mostrándose **[!UICONTROL Instalar]** para la extensión de . Inicie el flujo de trabajo de instalación tal como se describe en [Extensión de instalación](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía de la [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
