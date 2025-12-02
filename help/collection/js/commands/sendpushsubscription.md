---
title: sendPushSubscription
description: Registre suscripciones de notificaciones push con Adobe Experience Platform.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
>Las notificaciones push para Web SDK se encuentran actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

El comando `sendPushSubscription` registra las suscripciones de notificaciones push en Adobe Experience Platform. Este comando administra la recuperación de los detalles de la suscripción push desde el explorador y los envía al conjunto de datos configurado. Está disponible en las versiones 2.29.0 o posteriores de Web SDK.

## Requisitos previos {#prerequisites}

Antes de usar `sendPushSubscription`, asegúrese de que dispone de lo siguiente:

1. **Notificaciones push configuradas**: configure la propiedad de configuración [`pushNotifications`](configure/pushnotifications.md) con la clave pública VAPID
2. **Permiso de usuario**: los usuarios deben tener concedido permiso de notificación (`Notification.permission === "granted"`)
3. **Trabajador de servicio**: un trabajador de servicio registrado debe estar disponible en el sitio
4. **Compatibilidad con Push Manager**: el explorador debe admitir notificaciones push y tener disponible la API de PushManager

Ejecute el comando `sendPushSubscription` al llamar a la instancia configurada de Web SDK. Asegúrese de llamar al comando [`configure`](configure/overview.md) con las notificaciones push configuradas antes de llamar al comando `sendPushSubscription`.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Frecuencia de ejecución recomendada {#recommended-execution-frequency}

Para obtener una funcionalidad óptima de notificaciones push, Adobe recomienda ejecutar el comando `sendPushSubscription` **una vez al día**. Esta frecuencia garantiza lo siguiente:

* Los detalles de la suscripción permanecen actualizados en Adobe Experience Platform
* Se capturan todos los cambios en los tokens push o en el estado de suscripción
* El perfil del usuario permanece actualizado con las preferencias de notificaciones push más recientes

Puede implementar esto con un enfoque similar al siguiente:

```js
// Check if subscription data was sent today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Funcionamiento {#how-it-works}

El comando `sendPushSubscription` realiza las siguientes acciones:

1. **Valida los requisitos previos**: Comprueba que las notificaciones push estén configuradas y que se haya concedido el permiso de usuario
2. **Espera la identidad**: Espera a que el ECID del usuario esté disponible
3. **Recupera la suscripción**: obtiene la suscripción push activa del trabajador de servicio mediante la clave VAPID configurada
4. **Comprueba cambios**: compara los detalles de la suscripción actual con los valores almacenados en caché (ECID + detalles de la suscripción). Si los detalles de la suscripción no han cambiado, el comando registra un mensaje de información y vuelve sin realizar una solicitud de red
5. **Envía al conjunto de datos**: Si se detectan cambios, transmite los datos de suscripción al conjunto de datos configurado de Adobe Experience Platform
6. **Actualiza la caché**: Almacena los nuevos detalles de suscripción para futuras comparaciones

## Control de errores {#error-handling}

Condiciones de error comunes y sus mensajes:

| Error | Causa |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | Falta la configuración de pushNotifications o no es válida |
| `"Service workers are not supported in this browser."` | El explorador no admite trabajadores de servicio |
| `"Push notifications are not supported in this browser."` | El explorador no admite notificaciones push ni API de notificaciones |
| `"The user has not given permission to send push notifications."` | El usuario no ha concedido permiso de notificación (`Notification.permission === "granted"`) |
| `"No service worker registration was found."` | No hay ningún trabajador de servicio registrado para el origen actual |
| `"No VAPID public key was provided."` | Falta la clave pública VAPID en la configuración |

## Carga útil de datos {#data-payload}

El comando envía los datos de las notificaciones push en el siguiente formato:

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Registro de suscripciones push mediante la extensión de etiquetas Web SDK {#register-push-subscription-tag-extension}

La extensión de etiquetas Web SDK equivalente a este campo utiliza la acción [[!UICONTROL Send Push Subscription]](/help/tags/extensions/client/web-sdk/actions/send-push-subscription.md) dentro de una regla de etiquetas.

>[!MORELIKETHIS]
>
>* [Configuración de notificaciones push](configure/pushnotifications.md)
>* [Especificación de la API de Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [API de Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
