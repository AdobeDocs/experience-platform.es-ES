---
keywords: gtag;google tag;google extension;google gtag extension;GTAG
title: Extensión de etiqueta de Google
description: La extensión de etiqueta Google es un destino publicitario en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---

# Extensión de etiqueta de Google {#gtag-advertising-extension}

>[!IMPORTANT]
>
>La extensión de etiqueta de Google descrita aquí ha quedado obsoleta y reemplazada por la función [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) extensión desarrollada por [!DNL Acronym]. Puede encontrar la variable [!DNL Google Global Site Tag (gtag)] dentro de la función [[!UICONTROL Etiquetas]](../../../tags/home.md) en la interfaz de usuario de la recopilación de datos o de la interfaz de usuario del Experience Platform.

## Información general {#overview}

Cargar Google `gtag.js` en el sitio para enviar datos de evento a [!DNL Google Analytics], Google Ads y [!DNL Google Marketing Platform]. Esta extensión solo agrega el código de etiqueta al sitio. Deberá utilizar otras extensiones de Google para agregar eventos y acciones que utilicen gtag.

Google es una extensión publicitaria de Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [información general sobre las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de etiqueta de Google](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] catálogo para todos los clientes que han comprado Platform.

Para utilizar esta extensión, es necesario acceder a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda la **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión de la etiqueta Google:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, le falta la variable **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la [Sección de página Propiedades](../../../tags/ui/administration/companies-and-properties.md#properties-page) de en la documentación de etiquetas.

El flujo de trabajo le guía por los pasos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [Página de etiqueta de Google en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

También puede instalar la extensión directamente en el [Interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Para obtener más información, consulte la sección sobre [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) en la documentación de etiquetas.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas.

Puede configurar reglas para las extensiones instaladas para que envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la [documentación de etiquetas](../../../tags/ui/managing-resources/rules.md).

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario de Platform sigue mostrándose **[!UICONTROL Instalar]** para la extensión de . Inicie el flujo de trabajo de instalación tal como se describe en [Extensión de instalación](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía de la [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
