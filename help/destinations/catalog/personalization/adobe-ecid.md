---
Keywords: ECID;ecid
title: Extensión de Experience Cloud ID Service
description: La extensión del Servicio de ID de Experience Cloud es un destino de personalización en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# [!DNL Experience Cloud] Extensión del servicio de ID {#adobe-ecid-extension}

## Información general {#overview}

Esta extensión implementa las [!DNL Experience Cloud] Servicio de ID, que identifica a los visitantes en todas las [!DNL Experience Cloud] soluciones.

[!DNL Experience Cloud] El servicio de ID es una extensión de personalización en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la [Página de extensión del servicio de ID de Experience Cloud](../../../tags/extensions/client/id-service/overview.md) en la documentación de etiquetas.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [información general sobre extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión ECID de Adobe](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo de destinos para todos los clientes que han adquirido Platform.

Para utilizar esta extensión, debe acceder a las etiquetas en Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a la IU de recopilación de datos y pídale que le conceda el **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar el [!DNL Experience Cloud] Extensión del servicio de ID:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y luego seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, falta el **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad de etiqueta en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en [documentación de etiquetas](../../../tags/ui/administration/companies-and-properties.md).

El flujo de trabajo le lleva a la IU de recopilación de datos para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [Página de extensión del servicio de ID de Experience Cloud](../../../tags/extensions/client/id-service/overview.md) en la documentación de etiquetas.

También puede instalar la extensión directamente en [IU de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía de [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Uso de la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la IU de recopilación de datos, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la información general sobre [reglas](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configuración, actualización y eliminación de extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la IU de recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario se seguirá mostrando **[!UICONTROL Instalar]** para la extensión de. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para configurar o eliminar la extensión de.

Para actualizar la extensión, consulte la guía de [proceso de actualización de extensiones](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
