---
keywords: bing;seguimiento de eventos de bing ads;seguimiento de eventos bing;UET;extensión de UET
title: Extensión de seguimiento universal de eventos (UET) de Bing Ads
description: La extensión de seguimiento universal de eventos (UET) de Bing Ads es un destino de publicidad en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
exl-id: f2fc4d1f-01b0-4813-902c-9a3c30a8fa78
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 4%

---

# [!DNL Bing Ads Universal Event Tracking] Extensión (UET) {#bing-ads-extension}

## Información general {#overview}

El [!DNL Bing Ads Universal Event Tracking] La extensión de etiquetas (UET) es una forma útil de rastrear lo que sucede después de que alguien haya hecho clic en su anuncio de búsqueda. Con una sola etiqueta UET para registrar lo que hacen los clientes en su sitio web, puede aprovechar esos datos, lo que le permite rastrear conversiones o audiencias de destino mediante listas de remarketing.

[!DNL Bing Ads Universal Event Tracking] (UET) es una extensión publicitaria de Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión sobre [Intercambio de Adobe](https://exchange.adobe.com/experiencecloud.details.100154.html).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [información general sobre extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de Bing Ads](../../assets/catalog/advertising/bing-ads/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] para todos los clientes que han adquirido Platform.

Para utilizar esta extensión, debe tener acceso a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar el [!DNL Bing Ads Universal Event Tracking] Extensión (UET):

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y luego seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, falta el **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad de etiqueta en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md).

El flujo de trabajo le lleva a la IU de recopilación de datos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [Página de seguimiento universal de eventos (UET) de Bing Ads en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

También puede instalar la extensión directamente en [IU de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.


## Uso de la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la IU de recopilación de datos, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la información general sobre [reglas](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configuración, actualización y eliminación de extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la IU de recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario se seguirá mostrando **[!UICONTROL Instalar]** para la extensión de. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para configurar o eliminar la extensión de.

Para actualizar la extensión, consulte la guía de [proceso de actualización de extensiones](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
