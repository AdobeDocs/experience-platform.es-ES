---
title: Vista de depuración push
description: Esta guía detalla información sobre la vista de depuración push en Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# Vista de depuración push

La vista de depuración push dentro de Adobe Experience Platform Assurance permite validar la configuración de push para la aplicación y enviar un mensaje de prueba al dispositivo.

## Clientes

![Insertar clientes](./images/push-debug-view/clients.png)

La lista desplegable cliente tiene una lista de cada cliente único que se ha conectado a esta sesión de seguro. Un cliente es un dispositivo único o una instalación de aplicación única para un dispositivo. Por ejemplo, si se han conectado a la sesión un dispositivo Android y un dispositivo iOS, esos clientes aparecerán en la lista desplegable Clientes .

Después de reinstalar y volver a conectar la aplicación en un dispositivo, aparecerá otro cliente. Si ya existía un dispositivo con ese nombre, la nueva lista desplegable adjuntará el número 2 al nombre.

Esta vista solo está habilitada para un cliente único, por lo que seleccionar un cliente diferente cambiará los detalles de la pantalla.

## Validar configuración

La variable **[!UICONTROL Validar configuración]** valida y proporciona detalles adicionales sobre la configuración push de la aplicación. Existen tres paneles que realizan validaciones. Mostrarán una marca de verificación verde si todas las validaciones son correctas. Si hay tres marcas de verificación verdes, la aplicación se ha configurado correctamente para la mensajería push, está escribiendo tokens push en el perfil del usuario y tiene una superficie de aplicación asociada configurada.

Si algo no funciona como se espera, habrá una alerta con detalles sobre cómo solucionar ese problema:

![Estado no válido](./images/push-debug-view/invalid-state.png)

### Detalles del cliente

Este panel comprueba si el dispositivo está configurado correctamente. Esto incluye configurar la extensión en la interfaz de usuario de recopilación de datos, inicializar la extensión y sus requisitos previos en la aplicación y capturar el token push desde el dispositivo.

Si es válido, el panel mostrará el ECID para el dispositivo, el token push, el nombre y el tipo del Simulador para pruebas de Edge.

### Detalles del perfil

Una vez que el cliente esté correctamente configurado, este panel comprobará si el dispositivo está escribiendo en el perfil. También valida que el token push del perfil coincide con el del dispositivo.

Si es válido, el panel mostrará el ECID del dispositivo, el token push, el ID de la aplicación, la plataforma de mensajería y si el token push se ha incluido en la lista de denegados. El token se puede denegar en la lista por varios motivos, como que el usuario ha desinstalado la aplicación o que el usuario ha desactivado la mensajería push para la aplicación.

![Bloqueado](./images/push-debug-view/deny-list-blocked.png)

Finalmente, en la parte inferior del panel hay un vínculo que abrirá este perfil específico en una nueva pestaña.

### Credenciales y configuración de App Store

Este panel valida que el ID de aplicación y la plataforma de mensajería que se guardó en el perfil tengan una superficie de aplicación coincidente creada. En una superficie de aplicación se cargan las credenciales push para la aplicación.

Si es válido, el perfil mostrará el nombre de la superficie de la aplicación, el ID de la aplicación y el nombre del servicio de mensajería.

Finalmente, en la parte inferior del panel hay un vínculo que abrirá esta superficie de aplicación específica en una nueva pestaña.

## Enviar push de prueba

La variable **[!UICONTROL Enviar push de prueba]** se puede utilizar para enviar un mensaje de prueba a su dispositivo.

Hay varios paneles que se pueden configurar para probar distintas funciones push de iOS y Android. Una vez configurada, seleccione **[!UICONTROL Enviar notificación push de prueba]** para enviar el mensaje.

![Enviar push](./images/push-debug-view/send.png)

### Mensaje

En el **[!UICONTROL Mensaje]** , puede proporcionar un título y un cuerpo para el mensaje. La función de notificación silenciosa también se puede habilitar aquí.

![Panel de mensajes](./images/push-debug-view/message-pane.png)

### Destino push

La variable **[!UICONTROL Destino push]** permite personalizar el token push y la superficie de la aplicación que se utilizará al enviar el mensaje push.

Esta información se proporciona de forma predeterminada si la variable **[!UICONTROL Validar configuración]** muestra tres marcas de verificación verdes. Sin embargo, puede proporcionar su propio token push y su propia superficie de aplicación, aunque la aplicación no esté completamente configurada.

![Panel de destino](./images/push-debug-view/target-pane.png)

### Comportamiento de los clics

En el **[!UICONTROL Comportamiento de los clics]** , puede elegir cuál debe ser el comportamiento cuando se hace clic en la notificación push en el dispositivo. De forma predeterminada, la aplicación se abre, pero puede abrir un vínculo profundo o una página web.

Si elige usar un vínculo profundo, el desarrollador de la aplicación debe crearlo por usted.

![Panel Comportamiento](./images/push-debug-view/click-behavior.png)

### Medios enriquecidos

La variable **[!UICONTROL Medios enriquecidos]** permite agregar medios adicionales al mensaje como una imagen, un vídeo o un GIF. El desarrollador de la aplicación debe agregar código a la aplicación para habilitar esta función.

![Panel enriquecido](./images/push-debug-view/rich-pane.png)

### Botones

La variable **[!UICONTROL Botones]** permite agregar botones adicionales a la notificación push. Cada botón puede abrir la aplicación, abrir un vínculo profundo en la aplicación o abrir una página web.

El desarrollador de la aplicación debe agregar código a la aplicación para habilitar esta función.

![Panel Botones](./images/push-debug-view/buttons-pane.png)

### Datos personalizados

La variable **[!UICONTROL Datos personalizados]** permite agregar datos personalizados a la notificación push. Cada par clave/valor se envía como metadatos junto con el mensaje y los desarrolladores pueden utilizarlo para crear experiencias potentes y añadir un seguimiento adicional.

![Panel personalizado](./images/push-debug-view/custom-pane.png)

## Resultados de la prueba

Una vez que haya enviado un mensaje, la variable **[!UICONTROL Resultados de la prueba]** recibe datos de los servicios push del mensaje. Aquí puede ver si el mensaje llegó a los servicios de mensajería de Google/iOS:

![Resultados de la prueba](./images/push-debug-view/test-results.png)

Si se ha producido algún problema, se muestran aquí:

![Error de resultados de prueba](./images/push-debug-view/test-error.png)

## Avanzadas

### Ver carga útil de mensaje

Al lado de la variable **[!UICONTROL Enviar notificación push de prueba]** es un conjunto de elipsis con un menú emergente. Desde aquí puede ver la carga útil del mensaje. Esto le permite ver el mensaje exacto que se enviará al servicio de mensajería remota. Puede revisar esta carga útil o incluso copiarla y pegarla en una herramienta de prueba push de escritorio.

![Panel personalizado](./images/push-debug-view/message-payload.png)
