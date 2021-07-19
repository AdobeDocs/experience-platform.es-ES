---
keywords: Encuestas de Intersección de QuestionPro;Encuestas de Intercept de cuestionpro;PreguntasPro;PreguntasPro
title: Extensión de los estudios de interceptación de QuestionPro
description: La extensión de Encuestas interceptadas de QuestionPro es un destino de encuesta en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de la extensión en Adobe Exchange.
exl-id: a0d6d46b-caac-48ae-94bc-4ebf24f9c94a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 3%

---

# [!DNL QuestionPro Intercept Surveys] Extensión {#questionpro-extension}

## Información general {#overview}

[!DNL QuestionPro Intercept Surveys] es una plataforma para implementar encuestas y recopilar datos de actitud en el punto de transacción o cuando los usuarios entran o salen del sitio web.

[!DNL QuestionPro Intercept Surveys] es una extensión de encuesta en Adobe Experience Platform. Para obtener más información sobre la funcionalidad de la extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.90096.questionpro-surveys.html).

Este destino es una extensión de Adobe Experience Platform Launch. Para obtener más información sobre cómo funcionan las extensiones de Platform launch en Platform, consulte [Información general sobre las extensiones de Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Extensión de encuestas de interceptación de QuestionPro](../../assets/catalog/survey/web-intercept-surveys/catalog.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo [!DNL Destinations] para todos los clientes que han comprado Platform.

Para utilizar esta extensión, necesita acceder a Adobe Experience Platform Launch. El platform launch se ofrece a los clientes de Adobe Experience Cloud como una función incluida que añade valor. Póngase en contacto con el administrador de su organización para obtener acceso a Platform launch y pídale que le conceda el permiso **[!UICONTROL manage_properties]** para poder instalar extensiones.

## Extensión de instalación {#install-extension}

Para instalar la extensión [!DNL QuestionPro Intercept Surveys]:

En la [Platform interface](http://platform.adobe.com/), vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleccione la extensión del catálogo o utilice la barra de búsqueda.

Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Configurar]** en el carril derecho. Si el control **[!UICONTROL Configure]** aparece atenuado, le falta el permiso **[!UICONTROL manage_properties]**. Consulte [Requisitos previos](#prerequisites).

En la ventana **[!UICONTROL Select available Platform launch property]**, seleccione la propiedad de Platform launch en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en Platform launch. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [Properties page](../../../tags/ui/administration/companies-and-properties.md#properties-page) de la documentación de Platform launch.

El flujo de trabajo le lleva al Platform launch para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la página [Encuestas de interceptación de QuestionPro en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.90096.questionpro-surveys.html).

También puede instalar la extensión directamente en la [interfaz de Adobe Experience Platform Launch](https://launch.adobe.com/). Consulte [Añadir una nueva extensión](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) en la documentación de Platform launch.

## Cómo utilizar la extensión {#how-to-use}

Una vez instalada la extensión, puede empezar a configurar las reglas para ella directamente en el Platform launch.

En Platform launch, puede configurar reglas para las extensiones instaladas para que envíen datos de evento al destino de la extensión solo en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte [Documentación de reglas](../../../tags/ui/managing-resources/rules.md).

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de Platform launch.

>[!TIP]
>
>Si la extensión ya está instalada en una de las propiedades, la interfaz de usuario de Platform sigue mostrando **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación tal como se describe en [Install extension](#install-extension) para llegar al Platform launch y configurar o eliminar la extensión.

Para actualizar la extensión, consulte [Extension upgrade](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) en la documentación de Platform launch.
