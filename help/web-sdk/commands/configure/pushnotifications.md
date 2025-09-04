---
title: pushNotifications
description: Configure las notificaciones push para Web SDK para habilitar la mensajería push basada en el explorador.
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Las notificaciones push para Web SDK se encuentran actualmente en **beta**. La funcionalidad y la documentación pueden cambiar.

La propiedad `pushNotifications` le permite configurar notificaciones push para aplicaciones web. Esta función permite que la aplicación web reciba mensajes insertados desde un servidor, incluso cuando el sitio web no está cargado actualmente en el explorador o incluso cuando el explorador no se está ejecutando.

## Requisitos previos {#prerequisites}

Antes de configurar las notificaciones push, asegúrese de lo siguiente:

1. **Permiso de usuario**: los usuarios deben conceder permiso de forma explícita para las notificaciones
2. **Trabajador de servicio**: Se requiere un trabajador de servicio registrado para que funcionen las notificaciones push
3. **Claves VAPID**: genere claves VAPID (identificación voluntaria del servidor de aplicaciones) para la comunicación segura

## Generación de claves VAPID {#generate-vapid-keys}

Para generar claves VAPID, instale el paquete NPM `web-push` y ejecute:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Esto genera un par de claves pública y privada. Utilice la clave pública en la configuración de Web SDK y almacene la clave privada dentro del canal de notificaciones push de Adobe Journey Optimizer.

## Configuración de notificaciones push mediante la extensión de etiquetas Web SDK {#configure-push-notifications-tag-extension}

Siga estos pasos para habilitar y configurar las notificaciones push:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]** y, a continuación, haga clic en **[!UICONTROL Configurar]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. **Habilitar notificaciones push** desde la sección &quot;Componentes de compilación personalizados&quot;.
1. Desplácese hacia abajo para localizar la sección [!UICONTROL Notificaciones push].
1. Escriba su clave pública VAPID en el campo **[!UICONTROL Clave pública VAPID]**.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

>[!NOTE]
>
> Las notificaciones push deben habilitarse explícitamente en la configuración de la extensión de etiqueta. La función está desactivada de forma predeterminada.

## Configuración de notificaciones push mediante la biblioteca JavaScript de Web SDK {#configure-push-notifications-javascript}

Establezca el objeto `pushNotifications` al ejecutar el comando `configure`:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
  },
});
```

## Propiedades {#properties}

| Propiedad | Tipo | Requerido | Descripción |
| ------ | ------ | -------- | ----- |
| `vapidPublicKey` | Cadena | Sí | La clave pública VAPID utilizada para la suscripción push. Debe ser una cadena codificada en Base64. |

## Consideraciones importantes {#important-considerations}

- **Seguridad**: las suscripciones push están vinculadas a la clave pública VAPID específica utilizada durante la suscripción. Si cambia las claves VAPID, las suscripciones existentes se cancelan automáticamente y se vuelven a crear con la nueva clave.
- **Almacenamiento en caché**: Web SDK administra automáticamente las actualizaciones de suscripción comparando el ECID y los detalles de suscripción actuales con los valores almacenados en caché. Los datos de suscripción solo se envían cuando se detectan cambios.
- **Requisito de service worker**: las notificaciones push requieren un service worker registrado. Asegúrese de que el service worker esté configurado correctamente para gestionar eventos push.

## Próximos pasos {#next-steps}

Después de configurar las notificaciones push, utilice el comando [`sendPushSubscription`](../sendPushSubscription.md) para registrar las suscripciones push en Adobe Experience Platform.
