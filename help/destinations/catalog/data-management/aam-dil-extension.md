---
keywords: extensión de Audience Manager DIL;audience manager de destino;extensión dil
title: Extensión de Audience Manager DIL
description: La extensión de Audience Manager DIL es un destino de Data Management Platform (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Extensión de Audience Manager DIL {#aam-dil-extension}

## Información general {#overview}

Extensión de Adobe Audience Manager Data Integration Library (implementación del lado del cliente). Nota: Esta extensión no está pensada para utilizarse en el reenvío de datos de Adobe Analytics del lado del servidor (SSF). Para el reenvío del lado del servidor, utilice la extensión Adobe Analytics. Importante: A partir de la versión 8.0, DIL depende en gran medida del servicio de ID [!DNL Experience Cloud], versión 3.3 o superior. Implemente el servicio de ID [!DNL Experience Cloud] y DIL para disfrutar de todas las funcionalidades de integración de datos de [!DNL Audience Manager].

[!DNL Audience Manager] DIL es una extensión de Data Management Platform (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [página de extensión de Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) en la documentación de etiquetas.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones en Experience Platform, consulte [descripción general de las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que hayan adquirido Experience Platform.

Para utilizar esta extensión, debe tener acceso a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar la extensión de DIL [!DNL Audience Manager]:

En la [interfaz de Experience Platform](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** está deshabilitado, no tendrá el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información acerca de las propiedades en la [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md#properties-page).

El flujo de trabajo le guía para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la [página de extensión de Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) en la documentación de etiquetas.

También puede instalar la extensión directamente en la [IU de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Uso de la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la IU de recopilación de datos, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [rules](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configuración, actualización y eliminación de extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la IU de recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario seguirá mostrando **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía sobre el [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
