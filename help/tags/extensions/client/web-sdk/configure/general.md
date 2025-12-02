---
title: Ajustes de configuración de instancia de SDK
description: Configure las opciones generales de la instancia de Web SDK.
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# Ajustes de configuración de instancia de SDK

Esta sección de configuración rige el nombre de la instancia de Web SDK, la organización de IMS a la que se aplica y la ubicación a la que desea enviar datos. De manera predeterminada, una instancia se denomina `alloy`.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Busque el nombre de instancia justo debajo del acordeón [!UICONTROL SDK instances] expandido.

![Imagen que muestra la configuración general de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas](../assets/web-sdk-ext-general.png)

Las opciones disponibles son las siguientes:

## [!UICONTROL Name]

La extensión de etiquetas Adobe Experience Platform Web SDK admite varias instancias en la página. El nombre se utiliza para enviar datos a varias organizaciones sin requerir bibliotecas de etiquetas de Web SDK duplicadas. Puede cambiar el nombre de la instancia a cualquier nombre de objeto de JavaScript válido.

## [!UICONTROL IMS organization ID]

El ID de la organización a la que desea que se envíen los datos en Adobe. La mayoría de las veces, utilice el valor predeterminado que se rellena automáticamente. Cuando tenga varias instancias en la página, rellene este campo con el valor de la segunda organización a la que desee enviar datos.

## [!UICONTROL Edge domain]

Dominio desde el cual la extensión envía y recibe datos. Aunque el valor predeterminado de `edge.adobedc.net` funciona, Adobe recomienda usar un dominio de origen en la mayoría de los casos. Consulte el [programa de certificados administrados por Adobe](https://experienceleague.adobe.com/es/docs/core-services/interface/data-collection/adobe-managed-cert) para obtener instrucciones sobre cómo configurar un dominio de origen adecuado para la recopilación de datos. Consulte también [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) en la documentación de la biblioteca de JavaScript para obtener instrucciones sobre cómo establecer este valor.
