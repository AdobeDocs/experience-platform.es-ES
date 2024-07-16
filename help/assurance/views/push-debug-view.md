---
title: Vista de depuración push
description: Esta guía detalla información acerca de la vista Depurar push en Adobe Experience Platform Assurance.
exl-id: a9558ee2-2e80-4b0d-ab45-2020be85e634
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 100%

---

# Vista Depurar push

La vista Depurar push, dentro de Adobe Experience Platform Assurance, permite validar la configuración push de la aplicación y enviar un mensaje de prueba al dispositivo.

## Clientes 

![Clientes push](./images/push-debug-view/clients.png)

El menú desplegable de clientes muestra la lista de todos los clientes que se han conectado a esta sesión de Assurance. Un cliente es un dispositivo único o una instalación de aplicación única para un dispositivo. Por ejemplo, si se han conectado un dispositivo Android y un dispositivo iOS a la sesión, esos clientes aparecerían en la lista desplegable Clientes.

Después de reinstalar y volver a conectar la aplicación en un dispositivo, aparecerá otro cliente. Si ya existe un dispositivo con ese nombre, la nueva lista desplegable anexará un #2 al nombre.

Esta vista solo está habilitada para un único cliente, por lo que al seleccionar un cliente diferente cambian los detalles en la pantalla.

## Validar configuración

La pestaña **[!UICONTROL Validar configuración]** valida y proporciona detalles adicionales acerca de la configuración push de la aplicación. Existen tres paneles que ejecutan validaciones. Muestran una marca de verificación verde si todas las validaciones son correctas. Si hay tres marcas de verificación verdes, la aplicación se ha configurado correctamente para la mensajería push, escribe tokens push en el perfil de usuario y tiene una superficie de aplicación asociada configurada.

Si algo no funciona como se espera, aparece una alerta con detalles sobre cómo solucionar ese problema:

![Estado no válido](./images/push-debug-view/invalid-state.png)

### Detalles del cliente

Este panel comprueba si el dispositivo está configurado correctamente. Esto incluye configurar la extensión en la IU de recopilación de datos, inicializarla con sus requisitos previos en la aplicación y capturar el token push desde el dispositivo.

Si es válido, el panel mostrará el ECID del dispositivo, el token push y el nombre y tipo de la zona protegida de Edge.

### Detalles del perfil

Una vez que el cliente esté configurado correctamente, este panel comprobará si el dispositivo está escribiendo en el perfil. También valida que el token push del perfil coincida con el del dispositivo.

Si es válido, el panel mostrará el ECID del dispositivo, el token push, el ID de aplicación de su aplicación, la plataforma de mensajería y si el token push se ha incluido en la lista de denegados. El token se puede incluir en la lista de denegados por varios motivos, como que el usuario haya desinstalado la aplicación o que haya desactivado la mensajería push para esta.

![Bloqueado](./images/push-debug-view/deny-list-blocked.png)

Por último, en la parte inferior del panel se encuentra un vínculo que abrirá este perfil específico en una nueva pestaña.

### Credenciales y configuración de la AppStore

Este panel valida que el ID de aplicación y la plataforma de mensajería guardada en el perfil tengan una superficie de aplicación coincidente creada. Una superficie de aplicación es donde se cargan las credenciales push de la aplicación.

Si es válida, el perfil muestra el nombre de la superficie de la aplicación, el ID de la aplicación y el nombre del servicio de mensajería.

Por último, en la parte inferior del panel hay un vínculo que abre esta superficie específica de la aplicación en una pestaña nueva.

## Enviar push de prueba

La pestaña **[!UICONTROL Enviar push de prueba]** se puede usar para mandar un mensaje de prueba al dispositivo.

Existen varios paneles que se pueden configurar para probar las distintas funciones push de iOS y Android. Una vez configurado, seleccione **[!UICONTROL Enviar notificación push de prueba]** para mandar el mensaje.

![Enviar push](./images/push-debug-view/send.png)

### Mensaje

En el panel **[!UICONTROL Mensaje]**, puede proporcionar un título y un cuerpo para el mensaje. La función de notificación silenciosa también se puede habilitar aquí.

![Panel de mensajes](./images/push-debug-view/message-pane.png)

### Destinatario push

El panel **[!UICONTROL Destinatario push]** le permite personalizar qué superficie de aplicación y token push utilizar al enviar el mensaje push.

Esta información se proporciona de forma predeterminada si la pestaña **[!UICONTROL Validar configuración]** muestra tres marcas de verificación verdes. Sin embargo, puede proporcionar su propio token push y su superficie de aplicación, aunque la aplicación no esté completamente configurada.

![Panel Destinatario](./images/push-debug-view/target-pane.png)

### Comportamiento del clic

Desde el panel **[!UICONTROL Comportamiento dek clic]**, puede elegir cuál debe ser el comportamiento cuando se haga clic en la notificación push en el dispositivo. De forma predeterminada, abre la aplicación, pero puede abrir un vínculo profundo o una página web.

Si decide utilizar un vínculo profundo, el desarrollador de la aplicación debe crearlo por usted.

![Panel Comportamiento](./images/push-debug-view/click-behavior.png)

### Medios enriquecidos

El panel **[!UICONTROL Medios enriquecidos]** le permite añadir medios adicionales al mensaje, como una imagen, un vídeo o un GIF. El desarrollador de aplicaciones debe añadir código a la aplicación para habilitar esta función.

![Panel enriquecido](./images/push-debug-view/rich-pane.png)

### Botones

El panel **[!UICONTROL Botones]** permite añadir botones adicionales a la notificación push. Cada botón puede abrir la aplicación, un vínculo profundo en ella o una página web.

El desarrollador de aplicaciones debe añadir código a la aplicación para habilitar esta función.

![Panel Botones](./images/push-debug-view/buttons-pane.png)

### Datos personalizados

El panel **[!UICONTROL Datos personalizados]** le permite añadir datos personalizados a la notificación push. Cada par clave/valor se envía como metadatos junto con el mensaje y los desarrolladores pueden utilizarlo para crear experiencias útiles y agregar un seguimiento adicional.

![Panel personalizado](./images/push-debug-view/custom-pane.png)

## Resultados de la prueba

Una vez enviado un mensaje, la sección **[!UICONTROL Resultados de prueba]** recibe datos de los servicios push del mensaje. Aquí puede ver si el mensaje llegó a los servicios de mensajería de Google/iOS:

![Resultados de la prueba](./images/push-debug-view/test-results.png)

Si se produjo algún problema, se muestra aquí:

![Error de resultados de prueba](./images/push-debug-view/test-error.png)

## Avanzadas

### Vista de carga útil del mensaje

Junto al botón **[!UICONTROL Enviar notificación push de prueba]**, hay un conjunto de puntos suspensivos con un menú emergente. Desde aquí puede ver la carga útil del mensaje. Esto le permite ver el mensaje exacto que se enviará al servicio de mensajería remota. Puede revisar esta carga útil o incluso copiarla y pegarla en una herramienta de prueba push de escritorio.

![Panel personalizado](./images/push-debug-view/message-payload.png)
