---
title: pushNotifications
description: Configure las notificaciones push para Web SDK para habilitar la mensajería push basada en el explorador.
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>Las notificaciones push para Web SDK se encuentran actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

La propiedad `pushNotifications` le permite configurar las notificaciones push para las aplicaciones web. Esta función permite que la aplicación web reciba mensajes insertados desde un servidor, incluso cuando el sitio web no está cargado actualmente en el explorador.

## Requisitos previos {#prerequisites}

Antes de configurar las notificaciones push, asegúrese de lo siguiente:

1. **Permiso de usuario**: los usuarios deben conceder permiso de forma explícita para las notificaciones
2. **Trabajador de servicio**: Se requiere un trabajador de servicio registrado para que funcionen las notificaciones push
3. **Claves VAPID**: genere claves VAPID (identificación voluntaria del servidor de aplicaciones) para la comunicación segura
4. **ID de aplicación**: ID de aplicación utilizado al guardar las claves VAPID en Adobe Journey Optimizer -> Canales -> Configuración de push -> Credenciales de push
5. **ID del conjunto de datos de seguimiento**: El ID del conjunto de datos del sistema con el nombre &quot;Conjunto de datos de evento de experiencia de seguimiento push de AJO&quot;. Obtener esto de Adobe Journey Optimizer -> Conjuntos de datos

## Generación de claves VAPID {#generate-vapid-keys}

Para generar claves VAPID, instale el paquete NPM `web-push` y ejecute:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Esta acción genera un par de claves pública y privada. Utilice la clave pública en la configuración de Web SDK y almacene la clave privada dentro del canal de notificaciones push de Adobe Journey Optimizer.

## Instalación del service worker

El código de trabajador de servicio debe proporcionarse desde el mismo dominio que el sitio web. Descargue el código de trabajador de servicio de la CDN de Adobe y aloje el archivo JavaScript desde su propio servidor. El código de trabajo del servicio Web SDK está disponible mediante la siguiente estructura de dirección URL:

- **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

A continuación se muestra un ejemplo de cómo instalar el service worker:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Implementación

Establezca el objeto `pushNotifications` al ejecutar el comando `configure`:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Propiedades {#properties}

| Propiedad | Tipo | Requerido | Descripción |
|---|---|---|---|
| **`vapidPublicKey`** | Cadena | Sí | La clave pública VAPID utilizada para las suscripciones push. Debe ser una cadena codificada en Base64. |
| **`applicationId`** | Cadena | Sí | ID de aplicación asociado con la clave pública VAPID. |
| **`trackingDatasetId`** | Cadena | Sí | ID del conjunto de datos del sistema utilizado para el seguimiento de notificaciones push. |

## Consideraciones importantes {#important-considerations}

- **Seguridad**: las suscripciones push están vinculadas a la clave pública VAPID específica utilizada durante la suscripción. Si cambia las claves VAPID, las suscripciones existentes se cancelan automáticamente y se vuelven a crear con la nueva clave.
- **Almacenamiento en caché**: Web SDK administra automáticamente las actualizaciones de suscripción comparando el ECID y los detalles de suscripción actuales con los valores almacenados en caché. Los datos de suscripción solo se envían cuando se detectan cambios.
- **Requisito de service worker**: las notificaciones push requieren un service worker registrado. Asegúrese de que el service worker esté configurado correctamente para gestionar eventos push.

## Configuración de notificaciones push mediante la extensión de etiquetas Web SDK {#configure-push-notifications-tag-extension}

La extensión de etiquetas Web SDK equivalente a esta propiedad es la sección [[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) al configurar la extensión.

## Próximos pasos {#next-steps}

Después de configurar las notificaciones push, use el comando [sendPushSubscription](../sendpushsubscription.md) para registrar las suscripciones push en Adobe Experience Platform.
