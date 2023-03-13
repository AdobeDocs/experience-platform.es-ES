---
keywords: TMMData;datos tmm;tmmdata;datos TMM
title: Extensión TMMData
description: La extensión TMMData es un destino de análisis en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
exl-id: 9f4ad50e-d964-41b0-b58e-71611bff3ead
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# [!DNL TMMData] Extensión {#tmmdata-extension}

## Información general {#overview}

[!DNL TMMData's] Foundation Platform para Adobe Marketing Cloud proporciona a los equipos de marketing las herramientas necesarias para acceder a todas sus fuentes de datos esenciales y fusionarlas (incluidos los datos internos/externos y los datos en línea/sin conexión) para obtener un análisis seguro y completo entre canales, con la configuración automatizada de la campaña y la importación directa a Adobe y otras herramientas de análisis e inteligencia empresarial.

[!DNL TMMData] es una extensión de analytics en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión sobre [Intercambio de Adobe](https://exchange.adobe.com/experiencecloud.details.100148.tmmdata-foundation-platform.html).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [información general sobre extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión TMMData](../../assets/catalog/analytics/tmmdata/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] para todos los clientes que han adquirido Platform.

Para utilizar esta extensión, debe tener acceso a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar el [!DNL TMMData] extensión:

En el [Interfaz de plataforma](https://platform.adobe.com/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y luego seleccione **[!UICONTROL Configurar]** en el carril derecho. Si la variable **[!UICONTROL Configurar]** el control está atenuado, falta el **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en [Sección de página Propiedades](../../../tags/ui/administration/companies-and-properties.md#properties-page) de en la documentación de etiquetas.

El flujo de trabajo le guía para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la [Página TMMData en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100148.tmmdata-foundation-platform.html).

También puede instalar la extensión directamente en [IU de recopilación de datos](https://experience.adobe.com/#/data-collection/). Para obtener más información, consulte la sección sobre [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) en la documentación de etiquetas.

## Uso de la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas.

Puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la [documentación de etiquetas](../../../tags/ui/managing-resources/rules.md).

## Configuración, actualización y eliminación de extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la IU de recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario de Platform sigue apareciendo **[!UICONTROL Instalar]** para la extensión de. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para configurar o eliminar la extensión de.

Para actualizar la extensión, consulte la guía de [proceso de actualización de extensiones](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
