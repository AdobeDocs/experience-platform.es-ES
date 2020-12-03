---
keywords: target extension;target
title: Extensión de Adobe Target
seo-title: Extensión de Adobe Target
description: La extensión Adobe Target es un destino de personalización en la plataforma de datos del cliente en tiempo real. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
seo-description: La extensión Adobe Target es un destino de personalización en la plataforma de datos del cliente en tiempo real. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en Adobe Exchange.
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 12%

---


# Extensión de Adobe Target {#adobe-target-extension}

## Información general {#overview}

Adobe Target es la solución de Adobe Experience Cloud que proporciona todo lo necesario para adaptar y personalizar la experiencia de sus clientes con el objetivo de maximizar los ingresos en sus sitios web y móviles, aplicaciones, medios sociales y otros canales digitales.

Adobe Target es una extensión de personalización en la plataforma de datos del cliente en tiempo real. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100162.html).

Este destino es una [!DNL Adobe Experience Platform Launch] extensión. Para obtener más información sobre cómo funcionan [!DNL Platform Launch] las extensiones en tiempo real CDP, consulte Visión general [de las extensiones de](../launch-extensions/overview.md)Experience Platform Launch.

![Extensión de Adobe Target](../../assets/catalog/personalization/adobe-target/catalog.png)

## Requisitos previos  {#prerequisites}

Esta extensión está disponible en el [!DNL Destinations] catálogo para todos los clientes que han adquirido CDP en tiempo real.

Para utilizar esta extensión, necesita acceder a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida. Póngase en contacto con el administrador de su organización para obtener acceso a [!DNL Platform Launch] y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Instalar extensión {#install-extension}

Para instalar la extensión de Adobe Target:

En la interfaz [CDP en tiempo](http://platform.adobe.com/)real, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configurar]** está atenuado, le falta el permiso **[!UICONTROL manage_properties]** . Consulte [Requisitos previos](#prerequisites).

En la ventana **[!UICONTROL Seleccionar la propiedad]** Launch de plataforma disponible, seleccione la [!DNL Platform Launch] propiedad en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en [!DNL Platform Launch]. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [de la página](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Propiedades de la [!DNL Launch] documentación.

El flujo de trabajo le lleva a [!DNL Platform Launch] completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión, consulte la página [de la extensión de](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/target-extension/overview.html) Adobe Target en la documentación de Experience [!DNL Launch] .

También puede instalar la extensión directamente en la interfaz [de](https://launch.adobe.com/)Adobe Experience Platform Launch. Consulte [Añadir una nueva extensión](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) en la [!DNL Platform Launch] documentación.

## Cómo usar la extensión {#how-to-use}

Una vez instalada la extensión, puede configurar inicios directamente en [!DNL Platform Launch].

En [!DNL Platform Launch], puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión únicamente en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la documentación [](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)Reglas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la [!DNL Platform Launch] interfaz.

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de CDP en tiempo real aún muestra **[!UICONTROL Instalar]** para la extensión. Inicie el flujo de trabajo de instalación tal como se describe en [Instalar extensión](#install-extension) para obtener [!DNL Platform Launch] y configurar o eliminar la extensión.

Para actualizar la extensión, consulte Actualización [de](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) Extension en la [!DNL Platform Launch] documentación.
