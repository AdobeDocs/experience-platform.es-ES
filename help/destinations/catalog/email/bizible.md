---
keywords: bizible;extensión bizible;destino bizible
title: Extensión Bizible
description: La extensión Bizible es un destino de correo electrónico en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: 9e45416d-b951-411c-a59f-34f84529f721
source-git-commit: 967a287852ce4f479f658900593aed1f1f2bc0ad
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 3%

---

# [!DNL Bizible] Extensión {#bizible-extension}

## Información general {#overview}

[!DNL Bizible] es la solución de atribución B2B líder del sector que le proporciona una visibilidad inigualable de sus datos, de modo que pueda tomar decisiones inteligentes que impulsen el crecimiento.

[!DNL Bizible] es una extensión de correo electrónico en Adobe Experience Platform. Para obtener más información sobre Bizible, lea [Atribución de marketing](https://experienceleague.adobe.com/docs/bizible/using/introduction-to-bizible/overview-resources/marketing-attribution.html?lang=en) en los recursos de información general de Bizible.

Este destino es una extensión de etiqueta. Para obtener más información sobre cómo funcionan las extensiones de etiquetas en Platform, consulte la [descripción general de las extensiones de etiquetas](../launch-extensions/overview.md).

![Extensión Bizible](../../assets/catalog/email/bizible/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, es necesario acceder a las etiquetas en Adobe Experience Platform. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a las etiquetas y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión [!DNL Bizible]:

En la [Platform interface](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** aparece atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

Seleccione la propiedad tag en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la documentación de etiquetas [](../../../tags/ui/administration/companies-and-properties.md).

El flujo de trabajo le lleva a la interfaz de usuario de recopilación de datos para completar la instalación.

También puede instalar la extensión directamente en la [interfaz de usuario de recopilación de datos](https://experience.adobe.com/#/data-collection/). Consulte la guía [adding a new extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obtener más información.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar reglas. En la interfaz de usuario de la recopilación de datos, puede configurar reglas para que las extensiones instaladas envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la descripción general de [rules](../../../tags/ui/managing-resources/rules.md) en la documentación de etiquetas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de usuario de la recopilación de datos.

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de seguirá mostrando **[!UICONTROL Install]** para la extensión de . Inicie el flujo de trabajo de instalación tal como se describe en [Install extension](#install-extension) para configurar o eliminar la extensión.

Para actualizar la extensión, consulte la guía del [proceso de actualización de la extensión](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de etiquetas.
