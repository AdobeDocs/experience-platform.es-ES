---
keywords: extensión de DIL de Audience Manager;audience manager de destino;extensión dil
title: Extensión de DIL de Audience Manager
description: La extensión de DIL de Audience Manager es un destino de Data Management Platform (DMP) en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Extensión de DIL de Audience Manager {#aam-dil-extension}

## Información general {#overview}

Extensión de la Data Integration Library de Adobe Audience Manager (implementación del lado del cliente). Nota: Esta extensión no está pensada para utilizarse en el reenvío de datos de Adobe Analytics del lado del servidor (SSF). Para el reenvío del lado del servidor, utilice la extensión Adobe Analytics. Importante: A partir de la versión 8.0, DIL depende en gran medida de [!DNL Experience Cloud] Servicio de ID, versión 3.3 o superior. Implemente ambos [!DNL Experience Cloud] Servicio de ID y DIL para [!DNL Audience Manager] funciones de integración de datos.

[!DNL Audience Manager] DIL es una extensión de Data Management Platform (DMP) de Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [Página de extensión de Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) en la documentación de etiquetas.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones en Platform, consulte la [información general sobre extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de DIL de Audience Manager](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] para todos los clientes que han adquirido Platform.

Para utilizar esta extensión, debe tener acceso a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar el [!DNL Audience Manager] Extensión de DIL:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y luego seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, falta el **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md#properties-page).

El flujo de trabajo le guía para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la [Página de extensión de Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) en la documentación de etiquetas.

También puede instalar la extensión directamente en [IU de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Uso de la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la IU de recopilación de datos, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la información general sobre [reglas](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configuración, actualización y eliminación de extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la IU de recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario se seguirá mostrando **[!UICONTROL Instalar]** para la extensión de. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para configurar o eliminar la extensión de.

Para actualizar la extensión, consulte la guía de [proceso de actualización de extensiones](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
