---
title: Extensión PebblePost
seo-title: Extensión PebblePost
description: La extensión PebblePost es un destino de correo electrónico en la plataforma de datos del cliente en tiempo real de Adobe. Para obtener más información sobre la funcionalidad de extensión, consulte la página de extensión en Adobe Exchange.
seo-description: La extensión PebblePost es un destino de correo electrónico en la plataforma de datos del cliente en tiempo real de Adobe. Para obtener más información sobre la funcionalidad de extensión, consulte la página de extensión en Adobe Exchange.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# PebblePost Extension {#pebblepost-extension}

## Información general {#overview}

La solución Correo postal® programático de PebblePost ayuda a los especialistas en mercadotecnia digital a conectar el interés y la intención en línea con medios tangibles y sin conexión que convierten. Los especialistas en marketing pueden aprovechar los segmentos de datos personalizados que han creado en Adobe para ahora destinatario a los consumidores con una impresión de medios local relevante, de más largo plazo. Analice el rendimiento en tiempo real según la actividad de rutas de respuesta y las conversiones en el sitio.

PebblePost es una extensión de correo electrónico en la plataforma de datos del cliente en tiempo real de Adobe. Para obtener más información sobre la funcionalidad de extensión, consulte la página de extensión en [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100315.programmatic-direct-mail.html).

Este destino es una extensión de Experience Platform Launch. Para obtener más información sobre cómo funcionan las extensiones de Launch en Adobe Real-time CDP, consulte Descripción general [de las extensiones de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![PebblePost Extension](assets/pebblepost-extension.png)

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo de destinos para todos los clientes que hayan adquirido CDP en tiempo real de Adobe.

Para utilizar esta extensión, necesita acceder al Experience Platform Launch. Experience Platform Launch se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida. Póngase en contacto con el administrador de su organización para obtener acceso a Launch y pídale que le conceda el permiso para poder instalar extensiones. **[!UICONTROL manage_properties]**

## Instalar extensión {#install-extension}

Para instalar la extensión PebblePost:

1. En la interfaz [CDP en tiempo real de](http://platform.adobe.com/)Adobe, vaya a **[!UICONTROL Destinations > Catalog]**.
2. Seleccione la extensión del catálogo o utilice la barra de búsqueda.
3. Haga clic en el destino para resaltarlo y, a continuación, seleccione **[!UICONTROL Install Extension]** en el carril derecho. Si el **[!UICONTROL Install Extension]** control está atenuado, le falta el **[!UICONTROL manage_properties]** permiso. Consulte [Requisitos previos](#prerequisites).
4. En la **[!UICONTROL Select available Launch property]** ventana, seleccione la propiedad Launch en la que desea instalar la extensión. También tiene la opción de crear una nueva propiedad en Launch. Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Obtenga información sobre las propiedades en la sección [de la página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propiedades de la documentación de Launch.
5. El flujo de trabajo le lleva a Iniciar para completar la instalación.

Para obtener información sobre las opciones de configuración de la extensión y la compatibilidad con la instalación, consulte la página [PebblePost en Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100315.programmatic-direct-mail.html).

También puede instalar la extensión directamente en la interfaz del [Experience Platform Launch](https://launch.adobe.com/). Consulte [Añadir una nueva extensión](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) en la documentación de Launch.

## Cómo usar la extensión {#how-to-use}

Una vez instalada la extensión, puede configurar inicios para ella directamente en Launch.

En Launch, puede configurar reglas para las extensiones instaladas a fin de enviar datos de evento al destino de la extensión únicamente en determinadas situaciones. Para obtener más información sobre la configuración de reglas para las extensiones, consulte la documentación [](https://docs.adobe.com/help/es-ES/launch/using/reference/manage-resources/rules.html)Reglas.

## Configurar, actualizar y eliminar extensiones {#configure-upgrade-delete}

Puede configurar, actualizar y eliminar extensiones en la interfaz de Launch.

>[!TIP]
>
>Si la extensión ya está instalada en una de sus propiedades, la interfaz de usuario de CDP en tiempo real de Adobe seguirá mostrándose **[!UICONTROL Install]** para la extensión. Inicie el flujo de trabajo de instalación como se describe en [Instalar extensión](#install-extension) para llegar a Iniciar y configurar o eliminar la extensión.

Para actualizar la extensión, consulte Actualización [de](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) Extension en la documentación de Launch.