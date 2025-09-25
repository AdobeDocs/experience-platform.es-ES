---
title: pushNotifications
description: Configure las notificaciones push para Web SDK para habilitar la mensajería push basada en el explorador.
source-git-commit: 7c2afd6d823ebb2db0fabb4cc16ef30bcbfeef13
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Las notificaciones push para Web SDK se encuentran actualmente en **beta**. La funcionalidad y la documentación pueden cambiar.

La propiedad `pushNotifications` le permite configurar notificaciones push para aplicaciones web. Esta función permite que la aplicación web reciba mensajes insertados desde un servidor, incluso cuando el sitio web no está cargado actualmente en el explorador.

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

Esto genera un par de claves pública y privada. Utilice la clave pública en la configuración de Web SDK y almacene la clave privada dentro del canal de notificaciones push de Adobe Journey Optimizer.

## Instalación de JavaScript del service worker

El código de trabajo de servicio debe proporcionarse desde el mismo dominio que el sitio web. Descargue el código de trabajador de servicio de la CDN de Adobe y, a continuación, aloje el archivo JavaScript desde su propio servidor. El código de trabajo del servicio Web SDK está disponible mediante la siguiente estructura de dirección URL:

- **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

A continuación se muestra un ejemplo de cómo instalar el service worker:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Configuración de notificaciones push mediante la extensión de etiquetas Web SDK {#configure-push-notifications-tag-extension}

Siga estos pasos para habilitar y configurar las notificaciones push:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]** y, a continuación, haga clic en **[!UICONTROL Configurar]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. En la sección **[!UICONTROL Componentes de compilación personalizados]**, habilite **[!UICONTROL Notificaciones push]**.
1. Desplácese hacia abajo para localizar la sección [!UICONTROL Notificaciones push].
1. Escriba su clave pública VAPID en el campo **[!UICONTROL Clave pública VAPID]**.
1. Escriba su id. de aplicación en el campo **[!UICONTROL id. de aplicación]**.
1. Introduzca su ID del conjunto de datos de seguimiento en el campo **[!UICONTROL ID del conjunto de datos de seguimiento]**.
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
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Propiedades {#properties}

| Propiedad | Tipo | Requerido | Descripción |
|---------|----|---------|-----------|
| `vapidPublicKey` | Cadena | Sí | La clave pública VAPID utilizada para la suscripción push. Debe ser una cadena codificada en Base64. |
| `applicationId` | Cadena | Sí | ID de aplicación asociado con esta clave pública VAPID. |
| `trackingDatasetId` | Cadena | Sí | ID del conjunto de datos del sistema utilizado para el seguimiento de notificaciones push. |

## Consideraciones importantes {#important-considerations}

- **Seguridad**: las suscripciones push están vinculadas a la clave pública VAPID específica utilizada durante la suscripción. Si cambia las claves VAPID, las suscripciones existentes se cancelan automáticamente y se vuelven a crear con la nueva clave.
- **Almacenamiento en caché**: Web SDK administra automáticamente las actualizaciones de suscripción comparando el ECID y los detalles de suscripción actuales con los valores almacenados en caché. Los datos de suscripción solo se envían cuando se detectan cambios.
- **Requisito de service worker**: las notificaciones push requieren un service worker registrado. Asegúrese de que el service worker esté configurado correctamente para gestionar eventos push.

## Próximos pasos {#next-steps}

Después de configurar las notificaciones push, utilice el comando [`sendPushSubscription`](../sendPushSubscription.md) para registrar las suscripciones push en Adobe Experience Platform.
