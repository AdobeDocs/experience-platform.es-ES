---
keywords: livefyre;extensión livefyre
title: Extensión de Adobe Livefyre
description: La extensión Adobe Livefyre es un destino social en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: a134c144-e7b8-4d48-8c90-5999e5ceb8a0
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 5%

---

# Extensión de Adobe Livefyre {#adobe-livefyre-extension}

## Información general {#overview}

Adobe Livefyre le permite descubrir, organizar y publicar un flujo constante de contenido generado por el usuario en su sitio web para crear experiencias auténticas y altamente personalizadas.

Adobe Livefyre es una extensión social de Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100464.html).

Este destino es una extensión [!DNL Adobe Experience Platform Launch]. Para obtener más información sobre cómo funcionan las [!DNL Platform Launch] extensiones en Platform, consulte [información general sobre las extensiones de Experience Platform Launch](../launch-extensions/overview.md).

![Extensión de Adobe Livefyre](../../assets/catalog/social/adobe-livefyre/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, necesita acceder a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] se ofrece a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a [!DNL Platform Launch] y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión de Adobe Livefyre:

En la [Platform interface](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** aparece atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

En la ventana **[!UICONTROL Select available Platform launch property]**, seleccione la propiedad [!DNL Platform Launch] en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en [!DNL Platform Launch]. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [Properties page](../../../tags/ui/administration/companies-and-properties.md#properties-page) de la documentación [!DNL Launch].

El flujo de trabajo le lleva a [!DNL Platform Launch] para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la página [Adobe Livefyre en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100464.html).

También puede instalar la extensión directamente en la [interfaz de Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Añadir una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) en la documentación de [!DNL Platform Launch].


## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar las reglas para ella directamente en [!DNL Platform Launch].

En [!DNL Platform Launch], puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte [Documentación de reglas](../../../tags/ui/managing-resources/rules.md).

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz [!DNL Platform Launch].

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario de Platform sigue mostrando **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación tal como se describe en [Install extension](#install-extension) para llegar a [!DNL Platform Launch] y configurar o eliminar la extensión.

Para actualizar la extensión, consulte [Extension upgrade](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de [!DNL Platform Launch].
