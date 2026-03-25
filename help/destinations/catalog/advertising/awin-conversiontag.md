---
keywords: Awin Advertiser Conversion Tag extension;etiqueta de conversión;Awin;awin;AWIN
title: Extensión de etiqueta de conversión del anunciante Awin
description: La extensión de etiqueta de conversión del anunciante de Awin es un destino de publicidad en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 3%

---

# Extensión de etiqueta de conversión del anunciante Awin {#awin-conversiontag-extension}

## Información general {#overview}

La etiqueta de conversión es la declaración del objeto de JavaScript AWIN.Tracking.Sale, que se realiza en la página de confirmación para indicar a la etiqueta maestra que se ha realizado una conversión. Posteriormente, realizará las solicitudes de seguimiento necesarias.

La etiqueta de conversión del anunciante de Awin es una extensión publicitaria en [!DNL Adobe Experience Platform]. Para obtener más información acerca de la funcionalidad de la extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Experience Platform, consulte [descripción general de las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión Awin Advertiser Conversiontag en la interfaz de usuario](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo de destinos para todos los clientes que han adquirido Experience Platform.

Para utilizar esta extensión, debe tener acceso a las etiquetas en Experience Platform. Las etiquetas se ofrecen a [!DNL Adobe Experience Cloud] clientes como una característica incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las funciones de recopilación de datos en la interfaz de usuario y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para que pueda instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar la extensión [!DNL Awin Advertiser Conversion Tag]:

En la [interfaz de Experience Platform](https://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Seleccione el destino y, a continuación, seleccione **[!UICONTROL Configure]** en el carril derecho. Si el control **[!UICONTROL Configure]** está deshabilitado, no tiene el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad de etiqueta en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información acerca de las propiedades en la [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md).

El flujo de trabajo le lleva a la IU de recopilación de datos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [página Etiqueta de conversión del anunciante de Awin en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

También puede instalar la extensión directamente en la [IU de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.


## Uso de la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la IU de recopilación de datos, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [rules](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configuración, actualización y eliminación de extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la IU de recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario seguirá mostrando **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía sobre el [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
