---
keywords: Personalización web de Marketo;personalización web de marketing;extensión de personalización web de Marketo;extensión de personalización web de marketing;marketing;Marketo
title: Extensión de personalización web de Marketo
description: La extensión Marketo Web Personalization es un destino de personalización en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 3%

---

# [!DNL Marketo Web Personalization] Extensión {#marketo-web-personalization-extension}

## Información general {#overview}

Esta extensión implementa el script para las aplicaciones [!DNL Marketo’s] Web Personalization y ContentAI. [!DNL Marketo] La personalización web identifica y personaliza de forma exclusiva el contenido según las características de los visitantes web, como las firmografías para visitantes anónimos y una amplia gama de atributos de comportamiento dentro de la plataforma de  [!DNL Marketo] compromiso para visitantes conocidos. [!DNL Marketo] ContentAI contiene funciones para recomendaciones y personalización con tecnología de IA para campañas web y de correo electrónico únicas para clientes B2B.

[!DNL Marketo Web Personalization] es una extensión de personalización en Adobe Experience Platform. Para obtener más información sobre la personalización web y el contenidoAI en Marketo, lea [Información general sobre la personalización web](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html?lang=en).

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [descripción general de las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión de personalización web de Marketo](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, es necesario acceder a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones. y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para que pueda instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión [!DNL Marketo Web Personalization]:

En la [Platform interface](https://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

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
