---
title: Enviar suscripción push
description: Registre, envíe y recopile datos para suscripciones push de explorador.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# Enviar suscripción push

>[!AVAILABILITY]
>
>Las notificaciones push para Web SDK se encuentran actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

La acción **[!UICONTROL Send push subscription]** registra las suscripciones de notificaciones push con Adobe Experience Platform. Gestiona la recuperación de los detalles de la suscripción push desde el explorador y los envía al conjunto de datos configurado. Está disponible en las versiones 2.32.0 o posteriores de la extensión de Web SDK.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send push subscription]**.

La acción no tiene ninguna configuración aparte de seleccionar una instancia de SDK.

Asegúrese de establecer una clave pública [VAPID](../configure/push-notifications.md) válida al configurar la extensión antes de usar este comando.

Esta acción es la extensión de etiqueta equivalente al comando [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md). Consulte la página vinculada para obtener información sobre los requisitos previos, la frecuencia de ejecución recomendada, el funcionamiento del comando y la gestión de errores.

>[!MORELIKETHIS]
>
>* [Configuración de notificaciones push](../configure/push-notifications.md)
>* [Especificación de la API de Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [API de Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
