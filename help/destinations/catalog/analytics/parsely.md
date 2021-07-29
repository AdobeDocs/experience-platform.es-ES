---
keywords: Analice. ly;parsón;parse.ly;Parse.ly
title: Extensión de Analytics de Parse.ly
description: La extensión de Analytics Parse.ly es un destino de análisis en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 84d98e74-3e34-406c-9b80-81100c766dc8
source-git-commit: 6bbccf6751240637c861c2962b64e5247d8abb43
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 3%

---

# [!DNL Parse.ly Analytics] Extensión {#parsely-analytics-extension}

## Información general {#overview}

[!DNL Parse.ly Analytics] ayuda a más de 2.500 empresas a usar datos para comprender su audiencia en línea. Esta extensión instala un fragmento de JavaScript que rastrea la forma en que los visitantes interactúan con el contenido del sitio.

Parse.ly es una extensión de análisis en Adobe Experience Platform. Para obtener más información acerca de la funcionalidad de la extensión, consulte [Parse.ly Analytics](https://www.parse.ly/).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [descripción general de las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de Analytics de Parse.ly](../../assets/catalog/analytics/parsely/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, es necesario acceder a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones. y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para que pueda instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión [!DNL Parse.ly]:

En la [Platform interface](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** aparece atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [Properties page](../../../tags/ui/administration/companies-and-properties.md#properties-page) de la documentación de etiquetas.

El flujo de trabajo le guía por los pasos para completar la instalación.

También puede instalar la extensión directamente en la [interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Para obtener más información, consulte la sección sobre [adición de una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) en la documentación de etiquetas.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas.

Puede configurar reglas para las extensiones instaladas para que envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la [documentación de etiquetas](../../../tags/ui/managing-resources/rules.md).

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario de Platform sigue mostrando **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación tal como se describe en [Install extension](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía del [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
