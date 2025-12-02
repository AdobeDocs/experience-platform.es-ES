---
title: Configuración de notificaciones push
description: Configure las notificaciones push para la extensión de etiquetas Web SDK.
source-git-commit: 0b3f4ec51cac182b637c79b9fcb883e5f8f78d02
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Configuración de notificaciones push

>[!AVAILABILITY]
>
>Las notificaciones push para Web SDK se encuentran actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

Esta sección de configuración le permite establecer una clave pública VAPID para la autenticación de notificaciones push.

>[!NOTE]
>
>Esta característica debe habilitarse primero mediante [componentes de compilación personalizados](custom-build-components.md); está deshabilitada de manera predeterminada.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y luego haga clic en **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Expanda **[!UICONTROL Custom build components]** y después habilite **[!UICONTROL Push notifications]**.
1. En [!UICONTROL SDK instances], desplácese hacia abajo para localizar la sección [!UICONTROL Push Notifications].
1. Escriba la clave pública VAPID en el campo **[!UICONTROL VAPID Public Key]**.

![Imagen que muestra la configuración de las notificaciones push mediante la extensión de etiquetas Web SDK](../assets/push-notifications.png)

Los campos disponibles son los siguientes:

## [!UICONTROL VAPID public key]

La clave pública VAPID utilizada para las suscripciones push. Es una cadena codificada en Base64.

## [!UICONTROL Application ID]

ID de aplicación asociado con la clave pública VAPID.

## [!UICONTROL Tracking dataset ID]

ID del conjunto de datos para el seguimiento y el análisis de notificaciones push.

## Notificaciones push con la biblioteca de JavaScript

Esta sección es el equivalente de etiqueta de [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) al configurar la biblioteca JavaScript. La página vinculada también proporciona información sobre los requisitos previos y la generación de una clave pública VAPID.
