---
keywords: Advertising Cloud;extensión de advertising cloud; destino de advertising cloud
title: Extensión de Adobe Advertising Cloud
description: La extensión de Adobe Advertising Cloud es un destino publicitario en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---

# Extensión de Adobe Advertising Cloud {#adobe-advertising-cloud-extension}

## Información general {#overview}

Esta es la [!DNL Advertising Cloud] extensión para la implementación [!DNL Advertising Cloud] etiquetas de conversión y segmento tanto para la DSP como para la búsqueda (actualmente no se admite DCO).

Adobe Advertising Cloud es una extensión publicitaria de Adobe Experience Platform.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [información general sobre las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de Adobe Advertising Cloud](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo de destinos para todos los clientes que hayan comprado Platform.

Para utilizar esta extensión, necesita acceder a las etiquetas en Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las funciones de recopilación de datos en la interfaz de usuario de y pídale que le conceda la variable **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión de Adobe Advertising Cloud:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, le falta la variable **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad tag en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md).

El flujo de trabajo le lleva a la interfaz de usuario de recopilación de datos para completar la instalación.

También puede instalar la extensión directamente en el [Interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la interfaz de usuario de la recopilación de datos, puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [reglas](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario sigue mostrándose **[!UICONTROL Instalar]** para la extensión de . Inicie el flujo de trabajo de instalación tal como se describe en [Extensión de instalación](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía de la [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
