---
title: Ajustes de configuración de identidad
description: Defina cómo la extensión de etiqueta identifica a los visitantes.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# Ajustes de configuración de identidad

Esta sección de configuración le permite definir el comportamiento de Web SDK cuando se trata de gestionar la identificación del usuario.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Identity]**.

![Imagen que muestra la configuración de identidad de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas](../assets/web-sdk-ext-identity.png)

Las opciones disponibles son las siguientes:

## [!UICONTROL Migrate ECID from VisitorAPI]

Casilla de verificación que permite que Web SDK lea las cookies `AMCV` y `s_ecid` y establezca la cookie `AMCV` que usa `Visitor.js`. Esta característica es importante al migrar de bibliotecas que usan `VisitorAPI.js` a Web SDK, ya que algunas páginas podrían seguir usando `Visitor.js`. Esta opción permite que SDK siga utilizando el mismo ECID para que los usuarios no se identifiquen como dos usuarios independientes. La biblioteca JavaScript equivalente a esta casilla es [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## [!UICONTROL Use third-party cookies]

Cuando esta opción está habilitada, Web SDK intenta almacenar un identificador de usuario en una cookie de terceros. Si se realiza correctamente, el usuario se identifica como un solo usuario a medida que navega por varios dominios, en lugar de identificarse como un usuario independiente en cada dominio. Si esta opción está habilitada, es posible que SDK aún no pueda almacenar el identificador de usuario en una cookie de terceros si el explorador no admite cookies de terceros o si el usuario lo ha configurado para no permitir cookies de terceros. En este caso, SDK solo almacena el identificador en el dominio de origen. La biblioteca JavaScript equivalente a esta casilla es [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md).

>[!IMPORTANT]
>
>Las cookies de terceros no son compatibles con la funcionalidad [ID de dispositivo de origen](/help/collection/use-cases/identity/first-party-device-ids.md) en Web SDK. Puede usar ID de dispositivos de origen o cookies de terceros; no puede usar ambas funciones simultáneamente.
